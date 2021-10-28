This is a common ret2libc problem where the goal is to get root on the server by eventually running the function `system("/bin/sh")`.

First notice that we have a very simple buffer overflow using the `gets` function meaning we can return anywhere.

Also after running `checksec` we see that PIE is disabled. This means that function addresses used in the program will always stay the same.
Finally ASLR is enabled which means that the address space will be randomized between runs of the program.

The process of ret2libc usually involves two parts:
- Leak libc
- Call system

Libc is the C standard library that holds all the code used for every function in C.
With ASLR on, the libc addresses are always random so we will somehow have to leak it in order to find the location of system and binsh.
When the binary process starts it creates a PLT and GOT which allow the program to lookup libc addresses for functions used in the program.
The PLT and GOT entires for functions are not randomized because PIE is disabled so we can know exactly where they are.

A little info will now be given (although I don't know much about this) to summarize how the PLT and GOT work.

The PLT, aka the procedure linkage table is a way for the program to lookup and call various functions in libc.
It does this by using the GOT, which holds the global offset for various libc functions.
When we call a function like puts, we are actually calling the PLT entry for puts which looks up the address for the real puts function in libc.

Our goal will be to use the buffer overflow to leak a libc address and then calculate the offset to a more important libc function like system.
We can do this by calling puts on the puts GOT entry. This means that since the libc address for puts is stored in its GOT entry, we will be printing out the address.
After this happens we can callback to main through 32 bit stack nonsense.

With a libc address in hand and its corresponding function we can find the offset to other functions like system and an address pointing to "/bin/sh".
It is important to figure out the correct libc version on the server, since they may differ remotely and locally. By running our exploit on the server we can find, with the leak, what libc version it uses.

With the offsets in hand, and a callback to main, we can simply use the buffer overflow to return directly to the libc system function with argument "/bin/sh", giving us shell.
We can `cat flag.txt` on the server and get the flag.

For more info on the PLT and GOT you can refer to the following: https://www.technovelty.org/linux/plt-and-got-the-key-to-code-sharing-and-dynamic-libraries.html
For more info on ret2libc exploits you can refer to the following: https://youtu.be/m17mV24TgwY
A more detailed video writeup is available here: (not yet available)

Flag: `gnsCTF{r34d_m0r3_b00ks_1n_th3_l1br4ry}`

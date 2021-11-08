This challenge is a common tcache poisoning challenge by abusing a double free vulnerability.

Notice that this challenge is working on libc version 2.27, which uses the tcache for storing free chunks.

First, I will give some background info on how the heap works. The heap is a large amount of space that can be allocated and freed in the program.
This helps with managing large amounts of memory and optimizing memory consumption.
The basic idea is that when you allocate new data on the heap, you do so from a list of already free data in chunks.
Say we allocate a chunk of size 100 (bytes), then we will search for a freed chunk of 100 bytes or more (which will result in splitting the larger chunk size n into 2 chunks of size 100 and n - 100) to give to the program.
When we are done with some memory, we mark it as freed and put it back in the tcache for use later.

The tcache in particular stores chunks by size for easy access. These collections of chunks are called bins.
Each bin can be thought of as a stack with LIFO order so that freeing a chunk and immediately allocating a chunk of the same size will result in the same chunk being allocated.
There are two types of chunks, used and freed.

Used chunk example:
SOME METADATA (16 bytes)
CHUNK DATA

```
00000001 10000001
AAAAAAAA AAAAAAAA
AAAAAAAA AAAAAAAA
AAAAAAAA AAAAAAAA
```

Freed chunk example:
SOME METADATA (16 bytes)
NEXT CHUNK POINTER (8 bytes)
UNUSED DATA

```
00000001 10000001
7f37f120 AAAAAAAA
AAAAAAAA AAAAAAAA
AAAAAAAA AAAAAAAA
```

As you can see, the metadata in a freed chunk is essentialy the linked list part of the tcache. Overwriting this metadata would mean changing where the next chunk will be allocated.
And so that is what we will do with the double free.

So the main issue in the program is that the same chunk can be `free`ed twice. The reason this is an issue is because of the following. Imagine the tcache bin empty.

```
TCACHE:
0x0
```

Ok now we will free one chunk.

```
TCACHE:
0x7f51f040 -> 0x0
```

Ok so it is on the tcache and since there was nothing already on the tcache it points to nothing. Next we will free the same exact chunk.

```
TCACHE:
0x7f51f040 -> 0x7f51f040 -> 0x0
```

Ok now we will allocate a chunk of the same size and as a result we will get the first chunk in the bin, and we can edit it. Let's give it a name of AAAA. Our tcache now looks like this.

```
TCACHE:
0x7f51f040 -> 0x41414141 -> ???
```

That may have been unexpected, the thing that happened here is that we overwrote the data of the chunk and our new chunk ended up as something like this:

```
00000001 10000001
AAAAAAAA 00000000
00000000 00000000
00000000 00000000
```

But notice that even after allocating this chunk, the same chunk still exists in a duplicate entry on the tcache bin.
This means the glibc heap still thinks that this chunk is freed and looks at the first 8 bytes in the chunk to determine the next chunk address. But now those first 8 bytes have been overwritten with AAAA.

Ok so why is this useful? Well imagine we overwrote this with something useful instead of AAAA. In this case it would try making a chunk at that address which would be usable in our program.
Now since our program thinks that we have a valid chunk at this address, we will be able to use our program to read and write to this chunk. This essentially gives us arbitrary read/write. 
In combination with only partial RELRO and no PIE, this means we could theoretically overwrite a GOT address without leaking anything and pointing it to some useful function like load_flag.

The final exploit does pretty much just that.

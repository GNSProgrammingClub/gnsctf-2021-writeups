This challenge gives us some ciphertext and tells us that it is secure and we cannot get the flag from it.
The title is a pretty big hint that this has been encrypted with an xor key.
It also gives us a very big hint about using the flag format.
Indeed, most flags start with gnsCTF{ and xor (^) is its own inverse so we can derive the following:

I. flag ^ key = ciphertext
II. ciphertext ^ flag = key
III. ciphertext ^ key = flag

Also the challenge mentions that the key is repeated which means that a key like `key` will be xored against every 3 characters in the flag (so like `keykeykeykeykeykeyke...`).

Since most flags start with "gnsCTF{" we can use II to xor that against the start of our ciphertext to get the start of the key.
This turns out to be `notsecr` (notice both have 7 chars) and we can guess the rest of the key to be `notsecret`.

Now we use III to xor ciphertext and the key (`notsecretnotsecretnotsecret...`) to get our flag.

Flag: `gnsCTF{us3_s3cur3_k3y5_pl5}`

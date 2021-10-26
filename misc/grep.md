We are given a really large zip file with a lot of folders and files in it and we need to find the flag. The title of the challenge is a pretty big hint as we can use grep on linux to quickly find text in some file or folder.
Since there are lots of nested folders we will need to do a recursive search.
First unzip the file with `unzip grep.zip`.
Then we grep for the flag with `grep -r gnsCTF{ ./`. The -r flag does a recursive search.

Flag: `gnsCTF{gr3p_f0r_n33dl3s_1n_4_h4yst4ck}`

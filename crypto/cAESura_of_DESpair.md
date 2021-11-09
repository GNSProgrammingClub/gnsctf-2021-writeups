# Caesura of Despair

The first hint prompted for the usage of a software known as `OpenSSL` ([find it here](https://www.openssl.org/))

As the challenge text says `AES(DES)`, this means while encrypting, DES is used first, then AES is used around it. Thus, to decrypt, we reverse these steps. Additionally, the challenge text also specifies AES-256 for AES and CBC mode for both ciphers.

Our first command is:

`openssl enc -aes-256-cbc -d -in out.enc -out part.enc -k IRyS`

`aes-256-cbc` - cipher type

`-d` - Tells openssl that we are decrypting<br>

`-in` - Our input file

`-out` - Our output file

`-k` - Gives the password `IRyS` (provided by problem text)

Our second command is identical except for the change in cipher type (DES).

`openssl enc -des-cbc -d -in part.enc -out des.txt -k IRyS`

This produces the flag in the file `des.txt`: `gnsCTF{d4rkn355_w1ll_f4d3_away_l1ght_w1ll_gu1d3_y0ur_w4y_h0p3_has_descended_and_y0u_are_n0t_al0ne}`

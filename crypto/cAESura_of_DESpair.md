# Caesura of Despair

This challenge prompted for the usage of a software known as `openssl` ([find it here](https://www.openssl.org/)
<br>^This was revealed by one of the hints.

Next we have to identify the following:
- Password
- Encryption methods

Reading from the top to bottom:
AES -> DES

and that both are CBC.

Next we are provided the password which just makes this challenge free.

So next our second hint tells us there we are going to be using 2 commands. This will be in accordance with the problem's encryption.

This leads to our first command being somewhat like the following:

`openssl enc -aes-256-cbc -d -salt -in out.enc -out aes.enc -k IRyS`

`aes-256-cbc` - our first step of the decryption as provided by the challenge description<br>
`-d` - Tells openssl that we are decrypting<br>
`-salt` - See [here](https://stackoverflow.com/a/17297740/14501343)<br>
`-in` - Our input file
`-out` - Our output file
`-k` - Gives the password which is `IRyS`

After this you might get an error or some kind of warning message but this will be ignored, which then we will forward to the next command:

`openssl enc -des-cbc -d -salt -in aes.enc -out des.enc -k IRyS`

The main different is that we are now decrypting the AES file in DES.

This would produce the flag in the file `des.enc` of: `gnsCTF{d4rkn355_w1ll_f4d3_away_l1ght_w1ll_gu1d3_y0ur_w4y_h0p3_has_descended_and_y0u_are_n0t_al0ne}`

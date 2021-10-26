This is a base conversion challenge where we have to convert something back to our flag.

We are given an output of:

> 12101002032322121110311321110031100021133210232021133201202222332313333122310321131003313003131221222323231

The description gives a pretty big hint about how to do the conversions: 256, 10, 4.
Also since the output is in base 4 (numbers from 0 to 3 only), we can assume that our first conversion will be from base 4 to some other base.

256 stands for ascii, 10 stands for decimal, 4 stands for base 4.

So we convert from base 4 to base 10 and get `10311011567847012311272951094811451955510452110951155111851110125`.

If you know ascii and decimal you might realize these are the concatanated ascii codes in decimal.
We unconcatanate them by hand (anything starting with 1 is 3 digits, anything else is 2 digits) and get `103 110 115 67 84 70 123 112 72 95 109 48 114 51 95 55 104 52 110 95 115 51 118 51 110 125`.

And then we convert these ascii decimal codes to ascii characters to get the flag.

Flag: `gnsCTF{pH_m0r3_7h4n_s3v3n}`

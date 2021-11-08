# Monochrome Butterfly

This was an image steg. problem. 

The first thing you would've tried is to put it through an online image steg. solver, however this lead to really
nothing.

The second choice was to use a specialized tool like `file` or `xxd` or `exiftool` to check the informations within the file to make sure the flag is not hidden
within the file itself.

However these tools returned nothing.

The next thing was to try and match the colored squares with the non-colored ones to see if they are in binary, however this also lead to literally nothing.

However the hint revealed an RGB code, this code might be able to give you a "hint" that it involves changing the color of the image.

Using a tool like [StegSolve](https://github.com/exoad-archive/gnsctf2021/raw/main/apps/stegsolve.jar) you easily alter between the spectrums and find a qr code like
pattern throughout the different spectrums.

When these codes are pieced together you get something like this:
![](https://github.com/exoad-archive/gnsctf2021/blob/main/assets/butterfly_qr.png?raw=true)

When scanned it gave us the flag of:
`gnsCTF{h1dd3n_b3tw33n_th3_b1t_pl4n3s}`

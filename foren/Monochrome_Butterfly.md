<h1 id="monochrome-butterfly">Monochrome Butterfly</h1>
<p>This was an image steg. problem. </p>
<p>The first thing you would&#39;ve tried is to put it through an online image steg. solver, however this lead to really
nothing.</p>
<p>The second choice was to use a specialized tool like <code>file</code> or <code>xxd</code> or <code>exiftool</code> to check the informations within the file to make sure the flag is not hidden
within the file itself.</p>
<p>However these tools returned nothing.</p>
<p>The next thing was to try and match the colored squares with the non-colored ones to see if they are in binary, however this also lead to literally nothing.</p>
<p>However the hint revealed an RGB code, this code might be able to give you a &quot;hint&quot; that it involves changing the color of the image.</p>
<p>Using a tool like <a href="https://github.com/exoad-archive/gnsctf2021/raw/main/apps/stegsolve.jar">StegSolve</a> you easily alter between the spectrums and find a qr code like
pattern throughout the different spectrums.</p>
<p>When these codes are pieced together you get something like this:
<img src="https://github.com/exoad-archive/gnsctf2021/blob/main/assets/butterfly_qr.png?raw=true" alt=""></p>
<p>When scanned it gave us the flag of:
<code>gnsCTF{h1dd3n_b3tw33n_th3_b1t_pl4n3s}</code></p>

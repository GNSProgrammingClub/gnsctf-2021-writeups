<h1 id="pwner">Pwner</h1>
<p>The hex chars presented as the &quot;password&quot; in the source code:</p>
<p><code>\x45\x49\x04\x84\x05\x84\x23\x02\x99\x32\x03\n</code></p>
<p>you should easily recognize that these are non-printable characters. So the easiest way (ignoring the hint about pwnlibs which should be considered to be kinda &quot;overboard&quot;)
was to basically use a bash command to easily print out these hex chars.</p>
<p>Knowing that there are some ways to print stuffs to IO using bash, the approach we are using is using <code>printf</code> in bash.</p>
<p>Then we can easily bundle this command with the netcat port:</p>
<pre><code class="lang-sh">(printf "<span class="hljs-symbol">\x</span>45<span class="hljs-symbol">\x</span>49<span class="hljs-symbol">\x</span>04<span class="hljs-symbol">\x</span>84<span class="hljs-symbol">\x</span>05<span class="hljs-symbol">\x</span>84<span class="hljs-symbol">\x</span>23<span class="hljs-symbol">\x</span>02<span class="hljs-symbol">\x</span>99<span class="hljs-symbol">\x</span>32<span class="hljs-symbol">\x</span>03<span class="hljs-symbol">\n</span>") | nc gnsctf.ml 4010
</code></pre>
<p>which gives us the flag:
<code>gnsCTF{r34lly_b1g_k3yb04rd_y0u_g0t_th3r3}</code></p>

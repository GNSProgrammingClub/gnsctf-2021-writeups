<h1 id="my-world">My World</h1>
<p>Basically since the hint said &quot;The flag is built somewhere,&quot; it is easily assumed that the flag is a structure built somewhere within the world.
This means that you must teleport <code>/tp</code> to this structure&#39;s location.</p>
<p>The hint tells us that we must look through the region files which were the <code>.mca</code> files. These files could be viewed through a parser like 
<code>NBTExplorer</code>. However NBTExplorer does not let you look into the world, it only tells you the &quot;coordinates&quot; of where the loaded chunks are, and this
is very time consuming if you are just going to teleport to all the loaded coordinates throughout the world. (This is still a feasible option)</p>
<p>The second option, which might be the most helpful and efficient is to use a world viewer, such as <a href="https://github.com/Jupisoft111/Minecraft-Overworld-Viewer/releases">this</a>.
Loading the world save file, it will render out all of the files into pictures from a birds eye view. </p>
<p>Rendering the files out, we can examine them as <code>.png</code> files. We now just have to spot for anomlies within the world, which one of them was:
<img src="https://github.com/exoad-archive/gnsctf2021/blob/main/assets/r.4167.27747.png?raw=true" alt=""></p>
<p>From the world viewer, we can see this area was loaded in the coordinates of X,Z: <code>2133779, 14206976</code> respectively.</p>
<p>When we teleport to this location in the Minecraft World using the command <code>/tp 2133779 ~ 14206976</code> we get a clearer view of the flag:
<img src="https://github.com/exoad-archive/gnsctf2021/blob/main/assets/my_world_flag.png?raw=true" alt=""></p>

# My World

Basically since the hint said "The flag is built somewhere," it is easily assumed that the flag is a structure built somewhere within the world.
This means that you must teleport `/tp` to this structure's location.

The hint tells us that we must look through the region files which were the `.mca` files. These files could be viewed through a parser like 
`NBTExplorer`. However NBTExplorer does not let you look into the world, it only tells you the "coordinates" of where the loaded chunks are, and this
is very time consuming if you are just going to teleport to all the loaded coordinates throughout the world. (This is still a feasible option)

The second option, which might be the most helpful and efficient is to use a world viewer, such as [this](https://github.com/Jupisoft111/Minecraft-Overworld-Viewer/releases).
Loading the world save file, it will render out all of the files into pictures from a birds eye view. 

Rendering the files out, we can examine them as `.png` files. We now just have to spot for anomlies within the world, which one of them was:
![](https://github.com/exoad-archive/gnsctf2021/blob/main/assets/r.4167.27747.png?raw=true)

From the world viewer, we can see this area was loaded in the coordinates of X,Z: `2133779, 14206976` respectively.

When we teleport to this location in the Minecraft World using the command `/tp 2133779 ~ 14206976` we get a clearer view of the flag:
![](https://github.com/exoad-archive/gnsctf2021/blob/main/assets/my_world_flag.png?raw=true)


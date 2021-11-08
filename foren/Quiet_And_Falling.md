# Quiet and Falling

In order to get the first part of this challenge, the first hint tells us that we must solve Inspector Lyunks which means you should instantly open up
inspect element and hover over the `...` in the problem description to reveal the following:
![](https://github.com/exoad-archive/gnsctf2021/blob/main/assets/quiet_and_falling_inspector.png?raw=true)

However if we try to run anything like the commands `file` or try to view the hexdump or `xxd` the file, there will be nothing anomalous that will lead us
to the flag. We must now move onto the second hint

The second hint tells us that we must watch YouTube, which gives the following:
1. The flag is in a comment
2. The flag is in a Video Description
3. The MP3 file is a download of a video from YouTube which contains the Flag as a video somewhere throughout the video's duration

However we cannot rule out any of the possibilities or that if these are all of the possibilities.

So let's first identify the music/song being played. Simply you could've just taken the Challenge's name and plugged it into YouTube and have gotten something similar.
However the instrument or the means of producing that sound could've not been the same, this leads us to the second part of this solve which is to identify the instrument
used in order to produce this music.

If you are careful enough you could hear it as a music box. 

After we have gotten the song name and the instrument, plugging it into the YouTube search box: `music box quiet and falling` we get a few videos,
clicking through them we are then trying to match the sounds with what we hear in the MP3. [This video](https://www.youtube.com/watch?v=l4FXoiD2EvI&t=155s) then
seemed the most promising.

Now going back to our possibilities for a YouTube video:
- Reading through the video description revealed no anomalies
- Watching the entire video also reveals no anomalies

<b>However, reading through the comments and scrolling through them we see a comment made:</b>
![](https://github.com/exoad-archive/gnsctf2021/blob/main/assets/comment.png?raw=true)

Which is also made by a person on gnsCTF, along with the comment being in the format of a flag.

Now this is not the flag itself, there is still a small extra step. This step is to then take the first letter of each word in order to make it "valid" of a flag:
which gives us the flag of 

`gnsCTF{it's_quiet_down_here}`

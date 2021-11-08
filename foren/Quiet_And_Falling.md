<h1 id="quiet-and-falling">Quiet and Falling</h1>
<p>In order to get the first part of this challenge, the first hint tells us that we must solve Inspector Lyunks which means you should instantly open up
inspect element and hover over the <code>...</code> in the problem description to reveal the following:
<img src="https://github.com/exoad-archive/gnsctf2021/blob/main/assets/quiet_and_falling_inspector.png?raw=true" alt=""></p>
<p>However if we try to run anything like the commands <code>file</code> or try to view the hexdump or <code>xxd</code> the file, there will be nothing anomalous that will lead us
to the flag. We must now move onto the second hint</p>
<p>The second hint tells us that we must watch YouTube, which gives the following:</p>
<ol>
<li>The flag is in a comment</li>
<li>The flag is in a Video Description</li>
<li>The MP3 file is a download of a video from YouTube which contains the Flag as a video somewhere throughout the video&#39;s duration</li>
</ol>
<p>However we cannot rule out any of the possibilities or that if these are all of the possibilities.</p>
<p>So let&#39;s first identify the music/song being played. Simply you could&#39;ve just taken the Challenge&#39;s name and plugged it into YouTube and have gotten something similar.
However the instrument or the means of producing that sound could&#39;ve not been the same, this leads us to the second part of this solve which is to identify the instrument
used in order to produce this music.</p>
<p>If you are careful enough you could hear it as a music box. </p>
<p>After we have gotten the song name and the instrument, plugging it into the YouTube search box: <code>music box quiet and falling</code> we get a few videos,
clicking through them we are then trying to match the sounds with what we hear in the MP3. <a href="https://www.youtube.com/watch?v=l4FXoiD2EvI&amp;t=155s">This video</a> then
seemed the most promising.</p>
<p>Now going back to our possibilities for a YouTube video:</p>
<ul>
<li>Reading through the video description revealed no anomalies</li>
<li>Watching the entire video also reveals no anomalies</li>
</ul>
<p><b>However, reading through the comments and scrolling through them we see a comment made:</b>
<img src="https://github.com/exoad-archive/gnsctf2021/blob/main/assets/comment.png?raw=true" alt=""></p>
<p>Which is also made by a person on gnsCTF, along with the comment being in the format of a flag.</p>
<p>Now this is not the flag itself, there is still a small extra step. This step is to then take the first letter of each word in order to make it &quot;valid&quot; of a flag:
which gives us the flag of </p>
<p><code>gnsCTF{it&#39;s_quiet_down_here}</code></p>

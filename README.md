# Plex-Skip-Button-Instructions
How to alter the settings for Plex's forward and backwards skip button

Looking through Skuggomann's excellent work at `https://github.com/Skuggomann/Plex-Skip-Button-Patcher` I manually fixed my Plex Media Server. Their download didn't work because it couldn't find the files where they were expected

To do this, there are two files needing editing. 

-----------------------------------------------------------

The first file is `main-`somethingsomethingsomething`.js`. There are a few edits to make. I used vim to search and replace, but Notepad, sed, awk etc should all work fine. One of these was different that Skuggomann. The following edits will change forward skip to 10 seconds and keep backwards skip at 10 seconds.

| Old Text                   | New Text                   |
|----------------------------|----------------------------|
| ,i=10,s=30,                | ,i=10,s=10,                | 
| ,s=30,a=10,                | ,s=10,a=10,                |
| Skip Back 10 Seconds       | Skip Back 10 Seconds       |
| Skip Forward 30 Seconds    | Skip Forward 10 Seconds    |
| Seek Back (10 Seconds)     | Seek Back (10 Seconds)     |
| Seek Forward (30 Seconds)  | Seek Forward (10 Seconds)  |

-----------------------------------------------------------

The second file is the index.html file. Mine is located at `C:\Program Files\Plex\Plex Media Server\Resources\Plug-ins-f737b826c\WebClient.bundle\Contents\Resources\index.html` and is 30KB. It's the only `index.html` file in my entire Plex folder.

Line 42 of this file, or the fourth line from the bottom starts as:

`<script src="/web/js/main-`somethingsomethingseomthing`.js" integrity="`

Chang it to:

`<script src="/web/js/main-`somethingsomethingseomthing`.js NOthatsabadplex="`

This is needed because the new javascript file has a different checksum.

-----------------------------------------------------------

This fix only worked when I accessed my server directly, at `127.0.0.1`. When I used `app.plex.tv`, I had the regular skip and seek timings. My FireTV and android phone were also not effected.

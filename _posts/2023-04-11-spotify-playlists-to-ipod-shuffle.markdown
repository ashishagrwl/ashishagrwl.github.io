---
layout: post
title:  "How I sync my Spotify playlists to my iPod Shuffle"
categories: music how-to
---

I have an iPod Shuffle 4th gen from 2014. It still works and is handy for listening to podcasts and music.

![iPod Shuffle 4th gen][ipod-shuffle]

But who downloads music anymore? I use Spotify and have curated a few playlists there. I wanted to sync them to my iPod Shuffle. Here's how I did it.

Requirements:

* Spotify
* Youtube Music Premium
* iTunes on Windows
* [spotdl][spotdl]

The following steps are written for Ubuntu on WSL but should work on other platforms with slight changes.

1. (For higher quality downloads, optional) Download cookies.txt for Youtube Music using a browser extension like this one - <https://chrome.google.com/webstore/detail/get-cookiestxt-locally/cclelndahbckbenkjhflpdbgdldlbecc>

2. Download spotdl using pip and download ffmpeg.
```
pip install spotdl
spotdl --download-ffmpeg
```

3. Create a folder inside Music called `spotdl` and place the cookies.txt file inside it.

4. Create a subfolder for each playlist you want to sync. For example, I have a folder called `spotdl/pop` and another called `spotdl/classical`.

5. (For higher quality downloads, optional) Edit `~/.spotdl/config.json` and:
    * update "bitrate" to "auto". This will download the highest quality available.
    * update "cookie_file" to the path of the cookies.txt file downloaded in step 1.
    * update format to m4a.

5. Run spotdl synnc inside the subfolder with the playlist URL. E.g.
`spotdl sync https://open.spotify.com/playlist/1FVwLROwulS08mWDkHBViQ?si=44d6bfb36f184932 --save-file sync.spotdl`

6. Open iTunes and drag and drop the files from the subfolder to a corresponding playlist in iTunes.

7. Sync the iTunes playlists to iPod shuffle.

8. I also created a file called sync.sh in the spotdl folder with the following contents:
`find . -type f -name "*.spotdl" -execdir spotdl sync sync.spotdl \;`
This recursively syncs all playlists in each sub-folder.

9. Profit!

Next steps:

* Automate the sync process using a cron job or a task in Task Scheduler which is triggered when iPod is connected to the computer.


[ipod-shuffle]: /assets/images/ipod-shuffle-4th-gen.jpg
[spotdl]: https://github.com/spotDL/spotify-downloader
# youtube-cli

Search and play tracks, videos and playlists from YouTube and SoundCloud

Depends on `youtube-dl` and `mplayer`

Reuses previous search results if query hasn't changed

```sh
$ youtube vulfpeck
1 - VULFPECK // Back Pocket [music video]
2 - VULFPECK // 1612
3 - VULFPECK // Dean Town
4 - VULFPECK // Aunt Leslie
$ youtube vulfpeck --play 2-4a,1v
VULFPECK // 1612
VULFPECK // Dean Town
VULFPECK // Aunt Leslie
VULFPECK // Back Pocket [music video] (with video)
```

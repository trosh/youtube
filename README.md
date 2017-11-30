youtube-cli
===========

Search and play tracks, videos and playlists from YouTube

Depends on `youtube-dl` and `mplayer`

Reuses previous search results if query hasn't changed

Two tools are provided:

* `yt` searches for videos or playlists

  Arguments are coalesced into the search query.

  The output is human readable if output is a tty,
  otherwise the webpage URLs are returned.

* `yu` transforms video/playlist URLs into the corresponding stream URLs

  It takes a single positional argument:
  a pattern describing which lines from its input to use
  (`-` to describe a range, `,` to separate values or ranges),
  and whether to fetch video or audio stream for each
  (add `a` or `v` after a single value or continuous range).
  Playlist URLs play its first 10 elements by default
  but a subpattern (`plist`) can be used to specify which elements
  to play.

  The default media type is audio, unless explicitely overridden
  with optional argument `-a` or `-v`.

  Output is a list of stream URLs which can be given to a media player.

Example usage
-------------

```sh
$ yt vulfpeck
1 - VULFPECK // Back Pocket [music video]
2 - VULFPECK // 1612
3 - VULFPECK // Dean Town
4 - VULFPECK // Aunt Leslie
$ yt vufpeck | yu 2-4a,1v | mplayer -playlist -
# Warning, mplayer doesn't get stdin input
VULFPECK // 1612
VULFPECK // Dean Town
VULFPECK // Aunt Leslie
VULFPECK // Back Pocket [music video] (with video)
$ mplayer $(yt vulfpeck | yu 2-4a,1v)
VULFPECK // 1612
VULFPECK // Dean Town
VULFPECK // Aunt Leslie
VULFPECK // Back Pocket [music video] (with video)
$ yt ted talks
1 - TED - An interview with Mauritius's first female president | Ameenah Gurib-Fakim
2 - TED - Why wildfires have gotten worse -- and what we can do about it | Paul Hessburg
3 - TED - Why women stay silent after sexual assault (with English subtitles) | Inés Hercovich
4 - TED - For the love of birds | Washington Wachira
5 - TED - The global learning crisis -- and what to do about it | Amel Karboul
6 - TED - The surprisingly charming science of your gut | Giulia Enders
$ mplayer `!! | yu -v 6,3,2`
...
```

To do
-----

* SoundCloud support
* Speed up searching (coalesce requests ?)
* Better thread resiliency ?

<div align="center">
  <img src="assets/app_icon.ico" alt="logo" width=150 height=150>
</div>
<div align="center">
  <a href="https://deepwiki.com/Empty-57/ZeroBit-Player"><img src="https://deepwiki.com/badge.svg" alt="Ask DeepWiki"></a>
</div>

<p align="center">LogoSource: Alibaba Vector Graphics Library</p>

# ZeroBit Player
一A Material-style local music player based on Flutter and Rust.

![show](screenshot/7.png)

## Installation/Quick Start

### Installation

[Click here to install](https://github.com/Empty-57/ZeroBit-Player/releases/latest)

### Quick Start

- Install Rust environment
- Install Flutter SDK 3.7.2
- Install Flutter 3.32.6
- Install Dart 3.8.1

### Install dependencies
```
flutter pub get
```

### Start a project
```
flutter run
```

### Notice
After compilation, the 64-bit version of the BASS library needs to be included:
 - `bass.dll`
 - `bassalac.dll`
 - `bassape.dll`
 - `bassdsd.dll`
 - `bassflac.dll`
 - `bassmidi.dll`
 - `bassopus.dll`
 - `basswasapi.dll`
 - `basswebm.dll`
 - `basswv.dll`
 - `bass_fx.dll`

Copy it to the `BASSDLL` folder in the software directory.

To support desktop lyrics, copy the compiled content of [`Zerobit Player Desktop Lyrics`](https://github.com/Empty-57/zerobit_player_desktop_lyrics) to the `desktop_lyrics` folder in the software directory.

## Features

- Supports custom playlists
- Supports reading and writing (partial) metadata
- Supports reading embedded lyrics (partial)
- Supports reading local lyrics files
- Supports multiple audio formats
- Supports equalizer functionality
- Supports retrieving lyrics data from the network
- Supports categorization by artist, album, and folder
- Uses Material 3 style
- Supports custom theme colors and fonts
- Supports dynamic theme colors
- Supports SMTC
- Supports audio visualization
- Supports desktop lyrics

## Supported audio formats
- aac
- ape
- aiff
- aif
- flac
- mp3
- mp4 m4a m4b m4p m4v
- mpc
- opus
- ogg
- oga
- spx
- wav
- wv

## Supported lyrics formats
- qrc
- yrc
- 逐行lrc 
- 逐字Lrc
- 增强型Lrc

## Supported metadata formats for reading and writing
| audio format       | Metadata format                        |
|------------|------------------------------|
| AAC (ADTS) | `ID3v2`, `ID3v1`             |
| Ape        | `APE`, `ID3v2`\*, `ID3v1`    |
| AIFF       | `ID3v2`, `Text Chunks`       |
| FLAC       | `Vorbis Comments`, `ID3v2`\* |
| MP3        | `ID3v2`, `ID3v1`, `APE`      |
| MP4        | `iTunes-style ilst`          |
| MPC        | `APE`, `ID3v2`\*, `ID3v1`\*  |
| Opus       | `Vorbis Comments`            |
| Ogg Vorbis | `Vorbis Comments`            |
| Speex      | `Vorbis Comments`            |
| WAV        | `ID3v2`, `RIFF INFO`         |
| WavPack    | `APE`, `ID3v1`               |

\* Due to a lack of official support, this tag will be **read-only**.

## About Lyrics
By default, the player prioritizes finding a lyrics file with the same name in the same directory as the audio, and then looks for a `.lrc` file with the same name to serve as translation data. It prioritizes word-by-word lyrics formats. For example, for audio `a.flac`, it will first look for `a.qrc` as the lyrics data, and `a.lrc` will be used as translation data (if it exists).
If none exist, it will scan for embedded lyrics.</br>
If those also don't exist, you need to manually select lyrics from the network or write embedded lyrics.</br>
If "Automatically download selected lyrics" is enabled, after selecting lyrics, the original and translation files (if available) will be automatically created in the directory of the audio file.</br>

If you select lyrics in `.lrc` format, the following scenarios apply:</br>
If it contains phonetic guides (Ruby text), for lyric lines with the same timestamp, the first line is treated as the phonetic guide, the second line as the original text, and the third line as the translation.</br>
For example:</br>
```
[00:24.212]qi  yo to ma ga sa xi ta n da         这一行将会作为注音
[00:24.212]ちょっと魔がさしたんだ                  这一行将会作为原文
[00:24.212]我是有点鬼迷心窍了                      这一行将会作为翻译
```

If it does not contain phonetic guides, for lyric lines with the same timestamp, the first line is treated as the original text, and the second line as the translation.</br>
For example:</br>
```
[00:24.212]ちょっと魔がさしたんだ                   这一行将会作为原文
[00:24.212]我是有点鬼迷心窍了                      这一行将会作为翻译
```

If there is only one line, the lyric line will be split by ` / `. The text before ` / ` is treated as the original, and the text after ` / ` is treated as the translation.</br>
For example:</br>
```
[00:24.21]ちょっと魔がさしたんだ / 我是有点鬼迷心窍了     / 前面将会作为原文 / 后面将会作为翻译
```
If using [LDDC](https://github.com/chenmozhijin/LDDC) to match local lyrics and saving the lyrics file to the song directory, the player will still prioritize `.qrc` or `.yrc` format files as the original text. Please delete files in those two formats first to use [LDDC](https://github.com/chenmozhijin/LDDC) lyrics.

When using [LDDC](https://github.com/chenmozhijin/LDDC) to match local lyrics, you can choose to `Save to song tag` or `Save to song folder`. For the lyrics filename, please choose `Same as song filename`.

When using [LDDC](https://github.com/chenmozhijin/LDDC), in order to be compatible with the rendering of Romaji, Original, and Translation, please go to `Settings` -> `Lyrics Settings` -> `Order` tab in [LDDC](https://github.com/chenmozhijin/LDDC) and select: Romaji -> Original -> Translation.

To search for lyrics, please enter song information to search for more precise lyrics:</br>

![search](screenshot/5.png)

Manually write embedded lyrics:</br>

![editLyrics](screenshot/11.png)

## About Album Art
You can choose a local image as the cover, or click `Network Cover` to set the cover.</br>
If you use `Network Cover` to set the cover, it will match the cover using the currently configured API source. Please fill in the metadata (Title, Artist, Album) as correctly as possible to improve matching accuracy.</br>
![show](screenshot/10.png)

## Submitting Bugs or PRs
- If submitting a BUG, please create a new issue, describe the reproduction steps as much as possible, and provide screenshots.
- If submitting a PR, please check the code for potential hazards and try to make optimizations.

## Notice
If a serious error occurs in the software, you can try deleting all configuration files with the `.hive` suffix and the corresponding `.lock` suffix in the directory `C:\Users\<Username>\Documents`.

1.4. In later versions, the location of the configuration file will be changed from `C:\Users\<Username>\Documents` to `C:\Users\<Username>\Documents\zerobit_config`

## grateful
[coriander_player](https://github.com/Ferry-200/coriander_player)： UI design was referenced</br>
[BASS](https://www.un4seen.com/)： Player core</br>
[Lofty](https://crates.io/crates/lofty)： Read audio metadata

## Desktop lyrics display
![show](screenshot/12.png)
![show](screenshot/13.png)
![show](screenshot/14.png)

## Software screenshot
![show](screenshot/1.png)
![show](screenshot/2.png)
![show](screenshot/3.png)
![show](screenshot/4.png)
![show](screenshot/5.png)
![show](screenshot/6.png)
![show](screenshot/7.png)
![show](screenshot/8.png)
![show](screenshot/9.png)
![show](screenshot/10.png)
# Glomatico's Apple Music Downloader

A command-line tool for downloading Apple Music songs, music videos, and post videos with high quality and rich metadata.

**Join our Discord Server:** <https://discord.gg/aBjMEZ9tnq>

## ✨ Features

- 🎵 **High-Quality Songs** - Download songs in AAC 256kbps and other codecs
- 🎬 **High-Quality Music Videos** - Download music videos in resolutions up to 4K
- 📝 **Synced Lyrics** - Download synced lyrics in LRC, SRT, or TTML formats
- 🎤 **Artist Support** - Download all albums or music videos from an artist
- ⚙️ **Highly Customizable** - Extensive configuration options for advanced users

## 📋 Prerequisites

### Required

- **Python 3.10 or higher**
- **Apple Music Cookies** - Export your browser cookies in Netscape format while logged in with an active subscription:
  - **Firefox**: [Export Cookies](https://addons.mozilla.org/addon/export-cookies-txt)
  - **Chromium**: [Get cookies.txt LOCALLY](https://chromewebstore.google.com/detail/get-cookiestxt-locally/cclelndahbckbenkjhflpdbgdldlbecc)
- **FFmpeg** - Must be in your system PATH
  - **Windows**: [AnimMouse's FFmpeg Builds](https://github.com/AnimMouse/ffmpeg-stable-autobuild/releases)
  - **Linux**: [John Van Sickle's FFmpeg Builds](https://johnvansickle.com/ffmpeg/)

### Optional

Add these tools to your system PATH or specify their paths via command-line arguments:

- **[mp4decrypt](https://www.bento4.com/downloads/)** - Required for `mp4box` remux mode, music videos, and experimental codecs
- **[MP4Box](https://gpac.io/downloads/gpac-nightly-builds/)** - Required for `mp4box` remux mode
- **[N_m3u8DL-RE](https://github.com/nilaoda/N_m3u8DL-RE/releases/latest)** - Required for `nm3u8dlre` download mode

## 📦 Installation

```bash
pip install gamdl
```

**Setup cookies:**

1. Place your cookies file in the working directory as `cookies.txt`, or
2. Specify the path using `--cookies-path` or in the config file

## 🚀 Usage

```bash
gamdl [OPTIONS] URLS...
```

### Supported URL Types

- Songs
- Albums (Public/Library)
- Playlists (Public/Library)
- Music Videos
- Artists
- Post Videos

### Examples

**Download a song:**

```bash
gamdl "https://music.apple.com/us/album/never-gonna-give-you-up-2022-remaster/1624945511?i=1624945512"
```

**Download an album:**

```bash
gamdl "https://music.apple.com/us/album/whenever-you-need-somebody-2022-remaster/1624945511"
```

**Download from an artist:**

```bash
gamdl "https://music.apple.com/us/artist/rick-astley/669771"
```

### Interactive Prompt Controls

| Key            | Action            |
| -------------- | ----------------- |
| **Arrow keys** | Move selection    |
| **Space**      | Toggle selection  |
| **Ctrl + A**   | Select all        |
| **Enter**      | Confirm selection |

## ⚙️ Configuration

Configure gamdl using command-line arguments or a config file.

**Config file location:**

- Linux: `~/.gamdl/config.ini`
- Windows: `%USERPROFILE%\.gamdl\config.ini`

The file is created automatically on first run. Command-line arguments override config values.

### 📝 Configuration Options

| Option                          | Description                              | Default                                        |
| ------------------------------- | ---------------------------------------- | ---------------------------------------------- |
| **General Options**             |                                          |                                                |
| `--read-urls-as-txt`, `-r`      | Read URLs from text files                | `false`                                        |
| `--config-path`                 | Path to config file                      | `<home>/.gamdl/config.ini`                     |
| `--log-level`                   | Logging level (DEBUG/INFO/WARNING/ERROR) | `INFO`                                         |
| `--log-file`                    | Path to log file                         | -                                              |
| `--no-exceptions`               | Don't print exceptions                   | `false`                                        |
| **Apple Music Options**         |                                          |                                                |
| `--cookies-path`, `-c`          | Path to cookies file                     | `./cookies.txt`                                |
| `--language`, `-l`              | Metadata language (ISO-2A code)          | `en-US`                                        |
| **Output Options**              |                                          |                                                |
| `--output-path`, `-o`           | Output directory                         | `./Apple Music`                                |
| `--temp-path`                   | Temporary directory                      | `.`                                            |
| `--overwrite`                   | Overwrite existing files                 | `false`                                        |
| `--save-cover`, `-s`            | Save cover as separate file              | `false`                                        |
| `--save-playlist`               | Save M3U8 playlist file                  | `false`                                        |
| **Download Options**            |                                          |                                                |
| `--download-mode`               | Download mode (`ytdlp`/`nm3u8dlre`)      | `ytdlp`                                        |
| `--remux-mode`                  | Remux mode (`ffmpeg`/`mp4box`)           | `ffmpeg`                                       |
| `--cover-format`                | Cover format (`jpg`/`png`/`raw`)         | `jpg`                                          |
| `--cover-size`                  | Cover size in pixels                     | `1200`                                         |
| `--truncate`                    | Max filename length                      | -                                              |
| **Binary Paths**                |                                          |                                                |
| `--nm3u8dlre-path`              | Path to N_m3u8DL-RE                      | `N_m3u8DL-RE`                                  |
| `--mp4decrypt-path`             | Path to mp4decrypt                       | `mp4decrypt`                                   |
| `--ffmpeg-path`                 | Path to FFmpeg                           | `ffmpeg`                                       |
| `--mp4box-path`                 | Path to MP4Box                           | `MP4Box`                                       |
| `--wvd-path`                    | Path to .wvd file                        | -                                              |
| **Template Options**            |                                          |                                                |
| `--album-folder-template`       | Album folder template                    | `{album_artist}/{album}`                       |
| `--compilation-folder-template` | Compilation folder template              | `Compilations/{album}`                         |
| `--single-disc-folder-template` | Single disc template                     | `{track:02d} {title}`                          |
| `--multi-disc-folder-template`  | Multi disc template                      | `{disc}-{track:02d} {title}`                   |
| `--no-album-folder-template`    | No album folder template                 | `{artist}/Unknown Album`                       |
| `--no-album-file-template`      | No album file template                   | `{title}`                                      |
| `--playlist-file-template`      | Playlist template                        | `Playlists/{playlist_artist}/{playlist_title}` |
| `--date-tag-template`           | Date format template                     | `%Y-%m-%dT%H:%M:%SZ`                           |
| `--exclude-tags`                | Comma-separated tags to exclude          | -                                              |
| **Song Options**                |                                          |                                                |
| `--codec-song`                  | Song codec (see below)                   | `aac-legacy`                                   |
| `--synced-lyrics-format`        | Lyrics format (`lrc`/`srt`/`ttml`)       | `lrc`                                          |
| `--no-synced-lyrics`            | Don't download synced lyrics             | `false`                                        |
| `--synced-lyrics-only`          | Download only synced lyrics              | `false`                                        |
| **Music Video Options**         |                                          |                                                |
| `--music-video-codec-priority`  | Codec priority (comma-separated)         | `h265,h264`                                    |
| `--music-video-remux-format`    | Remux format (`m4v`/`mp4`)               | `m4v`                                          |
| `--music-video-resolution`      | Max resolution (see below)               | `1080p`                                        |
| **Post Video Options**          |                                          |                                                |
| `--uploaded-video-quality`      | Quality (`best`/`ask`)                   | `best`                                         |

### 🏷️ Template Variables

Use these variables in folder/file templates or `--exclude-tags`:

| Variable                                                                     | Description                                   |
| ---------------------------------------------------------------------------- | --------------------------------------------- |
| `{album}`, `{album_artist}`, `{album_id}`, `{album_sort}`                    | Album info                                    |
| `{artist}`, `{artist_id}`, `{artist_sort}`                                   | Artist info                                   |
| `{title}`, `{title_id}`, `{title_sort}`                                      | Title info                                    |
| `{composer}`, `{composer_id}`, `{composer_sort}`                             | Composer info                                 |
| `{track}`, `{track_total}`, `{disc}`, `{disc_total}`                         | Track numbers                                 |
| `{genre}`, `{genre_id}`                                                      | Genre info                                    |
| `{date}`                                                                     | Release date (supports strftime: `{date:%Y}`) |
| `{playlist_artist}`, `{playlist_id}`, `{playlist_title}`, `{playlist_track}` | Playlist info                                 |
| `{compilation}`, `{gapless}`, `{rating}`                                     | Media properties                              |
| `{comment}`, `{copyright}`, `{lyrics}`, `{cover}`                            | Additional metadata                           |
| `{media_type}`, `{storefront}`, `{xid}`                                      | Technical info                                |
| `all`                                                                        | Special: Skip all tagging                     |

### 🎵 Song Codecs

**Stable:**

- `aac-legacy` - AAC 256kbps 44.1kHz
- `aac-he-legacy` - AAC-HE 64kbps 44.1kHz

**Experimental** (may not work due to API limitations):

- `aac` - AAC 256kbps up to 48kHz
- `aac-he` - AAC-HE 64kbps up to 48kHz
- `aac-binaural` - AAC 256kbps binaural
- `aac-downmix` - AAC 256kbps downmix
- `aac-he-binaural` - AAC-HE 64kbps binaural
- `aac-he-downmix` - AAC-HE 64kbps downmix
- `atmos` - Dolby Atmos 768kbps
- `ac3` - AC3 640kbps
- `alac` - ALAC up to 24-bit/192kHz
- `ask` - Prompt to choose codec

### 🎬 Music Video Options

**Codecs:**

- `h264`, `h265`, `ask`

**Resolutions:**

- H.264: `240p`, `360p`, `480p`, `540p`, `720p`, `1080p`
- H.265 only: `1440p`, `2160p`

**Formats:**

- `m4v` (default), `mp4`

### 📺 Post Video Quality

- `best` - Up to 1080p with AAC 256kbps
- `ask` - Interactive quality selection

## 🐍 Embedding

Use gamdl as a library in your Python projects:

```python
import asyncio
from gamdl.api import AppleMusicApi
from gamdl.downloader import (
    AppleMusicBaseDownloader,
    AppleMusicDownloader,
    AppleMusicMusicVideoDownloader,
    AppleMusicSongDownloader,
    AppleMusicUploadedVideoDownloader,
)


async def main():
    # Initialize API
    api = AppleMusicApi.from_netscape_cookies(cookies_path="cookies.txt")
    await api.setup()

    # Initialize downloaders
    base_downloader = AppleMusicBaseDownloader(apple_music_api=api)
    base_downloader.setup()

    song_downloader = AppleMusicSongDownloader(base_downloader)
    song_downloader.setup()

    music_video_downloader = AppleMusicMusicVideoDownloader(base_downloader)
    music_video_downloader.setup()

    uploaded_video_downloader = AppleMusicUploadedVideoDownloader(base_downloader)
    uploaded_video_downloader.setup()

    # Create main downloader
    downloader = AppleMusicDownloader(
        base_downloader,
        song_downloader,
        music_video_downloader,
        uploaded_video_downloader,
    )

    # Download a song
    url_info = downloader.get_url_info(
        "https://music.apple.com/us/album/never-gonna-give-you-up-2022-remaster/1624945511?i=1624945512"
    )

    if url_info:
        download_queue = await downloader.get_download_queue(url_info)
        if download_queue:
            for download_item in download_queue:
                await downloader.download(download_item)


if __name__ == "__main__":
    asyncio.run(main())
```

## 📄 License

MIT License - see [LICENSE](LICENSE) file for details

## 🤝 Contributing

Contributions are welcome! Feel free to open issues or submit pull requests.

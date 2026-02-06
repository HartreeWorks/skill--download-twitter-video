---
name: download-twitter-video
description: This skill should be used when the user asks to "download twitter video", "download tweet video", "dl twitter", "save twitter video", "download this tweet", or provides a Twitter/X URL with intent to download a video. Handles video downloads from x.com and twitter.com using yt-dlp.
---

# Download Twitter video

Download videos from Twitter/X posts using yt-dlp.

## Prerequisites

Ensure yt-dlp is installed:

```bash
brew install yt-dlp
```

## Workflow

### Step 1: Validate the URL

Accept URLs in these formats:
- `https://x.com/username/status/1234567890`
- `https://twitter.com/username/status/1234567890`

Extract the tweet ID (the numeric portion after `/status/`).

### Step 2: Create output directory

```bash
mkdir -p ~/.claude/skills/download-twitter-video/videos
```

### Step 3: Download the video

Use yt-dlp to download the video:

```bash
yt-dlp -f "best[ext=mp4]/best" \
  -o "$HOME/.claude/skills/download-twitter-video/videos/%(id)s.%(ext)s" \
  "<TWITTER_URL>"
```

The video will be saved as `<tweet-id>.mp4` in the videos directory.

### Step 4: Report results

After download, report:
- Full path to the downloaded file
- File size (use `ls -lh`)
- Confirmation message

Example output:
```
Downloaded: ~/.claude/skills/download-twitter-video/videos/1774403827548242333.mp4
Size: 12.5 MB
```

## Troubleshooting

If yt-dlp fails, check available formats:

```bash
yt-dlp --list-formats "<TWITTER_URL>"
```

If authentication is required, yt-dlp may need cookies. Export cookies from browser:

```bash
yt-dlp --cookies-from-browser chrome "<TWITTER_URL>"
```

## Output location

All videos are saved to:
```
~/.claude/skills/download-twitter-video/videos/
```

## Update check

This skill is managed by [skills.sh](https://skills.sh). To check for updates, run `npx skills update`.

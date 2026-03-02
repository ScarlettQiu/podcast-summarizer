# podcast-summarizer
podcast-summarizer/
├── .github/workflows/summarize.yml   # runs daily at 8am UTC
├── src/
│   ├── main.py          # orchestrator: fetch → download → transcribe → summarize
│   ├── feed_finder.py   # converts Apple Podcasts URL → RSS feed
│   ├── feed_parser.py   # parses RSS, returns new episodes with audio URLs
│   ├── downloader.py    # downloads + compresses audio to <25MB via ffmpeg
│   ├── transcriber.py   # Whisper API transcription
│   ├── summarizer.py    # Claude summarization (macro or default style)
│   └── db.py            # SQLite-based deduplication (skip already-processed episodes)
├── summaries/            # output .md files committed by the workflow
├── podcasts.json         # your list of podcasts to track
├── requirements.txt
└── .gitignore

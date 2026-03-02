# podcast-summarizer
Automatically fetch new podcast episodes, transcribe them, and generate markdown summaries on a schedule.

---

### Features

- **Automated workflow**: End‑to‑end pipeline from feed to summaries.
- **Daily schedule**: Runs via GitHub Actions (configured for 08:00 UTC).
- **Smart deduplication**: Skips episodes that have already been processed.
- **Compact audio downloads**: Compresses audio files to under 25 MB.
- **Markdown output**: Stores human‑readable summaries as `.md` files.

---

### Project Structure

`podcast-summarizer/`
- **`.github/workflows/summarize.yml`** – runs daily at 8am UTC
- **`src/`**
  - **`main.py`** – orchestrator: fetch → download → transcribe → summarize
  - **`feed_finder.py`** – converts Apple Podcasts URL → RSS feed
  - **`feed_parser.py`** – parses RSS, returns new episodes with audio URLs
  - **`downloader.py`** – downloads + compresses audio to <25MB via ffmpeg
  - **`transcriber.py`** – Whisper API transcription
  - **`summarizer.py`** – Claude summarization (macro or default style)
  - **`db.py`** – SQLite-based deduplication (skips already-processed episodes)
- **`summaries/`** – output `.md` files committed by the workflow
- **`podcasts.json`** – your list of podcasts to track
- **`requirements.txt`**
- **`.gitignore`**

---

### Setup (local)

- **Python**: Make sure you have a recent version of Python installed.
- **Dependencies**: Install dependencies with:

```bash
pip install -r requirements.txt
```

---

### Configuration

- **Podcasts list**: Edit `podcasts.json` to define which shows and feeds you want to track.
- **Summaries**: Generated markdown files will appear under `summaries/`.

---

### Running

Depending on how you wire up `main.py`, you can:

- **Run once locally**:

```bash
python src/main.py
```

- **Run on a schedule**:
  - Use the provided GitHub Actions workflow (`.github/workflows/summarize.yml`) to execute the pipeline on a daily cadence.

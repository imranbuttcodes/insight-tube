# InsightTube 

AI-powered YouTube comment analyzer. Paste a video link, get back a full report — sentiment breakdown, what people liked, what they hated, feature requests, and business recommendations.

Built this because scrolling through hundreds of comments manually to figure out "what do people actually think" is a waste of time. This does it in one click.

## What it does

1. You paste a YouTube video URL
2. It pulls up to 100 top-level comments using the YouTube Data API
3. Comments get passed to an LLM (Llama 3.3 70B via Groq) with a structured prompt
4. You get back a proper report: sentiment %, discussion themes, complaints, urgent issues, and even suggested business actions

The report format is built like something you'd actually hand to a business owner or content creator — not just a vibe check, an actual structured breakdown.

## Stack

- **Streamlit** — UI
- **Groq (Llama 3.3 70B)** — analysis
- **LangChain** — prompt template + chain
- **YouTube Data API v3** — pulling comments

## Setup

You'll need two API keys:

- `YOUTUBE_API_KEY` — from Google Cloud Console (enable YouTube Data API v3)
- `GROQ_API_KEY` — free from console.groq.com

Drop them in a `.env` file:

```
YOUTUBE_API_KEY=your_key_here
GROQ_API_KEY=your_key_here
```

Install deps:

```bash
pip install streamlit langchain langchain-groq python-dotenv requests
```

Run it:

```bash
streamlit run app.py
```

## Supported URL formats

- `youtube.com/watch?v=VIDEO_ID`
- `www.youtube.com/watch?v=VIDEO_ID`
- `youtu.be/VIDEO_ID`

## Notes / limitations

- Pulls top-level comments only (no reply threads) — capped at 100 per run to keep things fast and stay well within API + token limits
- Videos with comments disabled or very few comments obviously won't give a useful report
- The report is only as good as the comments available — a video with 5 comments isn't going to produce a meaningful sentiment breakdown

## Why I built this

Wanted something that actually goes past "here's the sentiment score" and gives real, actionable output — the kind of thing you'd use before deciding what to fix in your next video or product update.
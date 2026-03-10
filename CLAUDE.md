# Aviz Museum — Project Instructions

## About This Project
Virtual museum of Avraham Yitzchak Maeir (Aviz)'s 17-year Facebook journey (2009–2026).
Live site: https://aviz85.github.io/aviz-museum/
GitHub: https://github.com/aviz85/aviz-museum

## Files
- `index.html` — Main museum (6 eras, Hebrew RTL)
- `cycle.html` — Deep appendix: hypomania cycle documentation
- `images/era1.jpg` – `era6.jpg` — Era images
- `music/ambient.mp3` — Background ambient music

## Agents
- **fb-post-finder** (`.claude/agents/fb-post-finder.md`) — Finds the exact Facebook permalink for any quote. Run it whenever adding a new quote to verify the link.

## Biographical Knowledge
Full biographical data: `~/sb/notes/me/aviz-biography.md`
Research synthesis: `~/sb/notes/aviz-facebook-synthesis-portrait.md`
Research insights: `~/sb/notes/aviz-fb-research-insights.md`

## Data Files (in this repo)

| File | Contents |
|------|----------|
| `data/posts-lookup.json` | Timestamps + Drive file IDs of key biographical posts. Includes memoir (ts=1419993120), 2015 crisis (ts=1436427188), Rothschild/Tisha B'Av posts. Also contains Drive file IDs for the raw export JSONs. |
| `data/README.md` | How to download & decode Facebook export data (latin-1 triple-encode fix) |

**Facebook Export Location (Google Drive):**
- File: `your_posts__check_ins__photos_and_videos_1.json` → Drive ID: `1UhV7m_BqrJhwqB4pX7AP6O5RTuEYZiIa`
- Total posts in file 1: 10,000 (range: 2009–2026)
- Decode: `s.encode('latin-1').decode('utf-8').encode('latin-1').decode('utf-8')`
- Fields: `timestamp`, `data[].post`, `attachments`, `title` — **NO post IDs or URLs in export**

## Rules
1. Every quote added to the site → run fb-post-finder agent → add real Facebook link
2. Hebrew RTL throughout — `dir="rtl"` on all Hebrew text blocks
3. No visual changes without explicit request — keep the dark museum aesthetic
4. After every change → `git add . && git commit -m "..." && git push`

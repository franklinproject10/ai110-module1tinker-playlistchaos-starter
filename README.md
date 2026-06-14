# Playlist Chaos — AI110 Tinker Activity

An AI-generated Streamlit app that groups songs into mood-based playlists: **Hype**, **Chill**, and **Mixed**.

This project was debugged and refactored as part of the AI110 course Tinker activity.

---

## 🚀 How to Run

```bash
pip install -r requirements.txt
streamlit run app.py
```

---

## 🐛 Bugs Fixed

### Bug #1 — Search Partial Match (playlist_logic.py)
- **Problem:** Search only worked with exact full artist name. Typing `ac` never found `ac/dc`.
- **Cause:** `value in q` was backwards — checking if the artist was inside the query instead of the other way around.
- **Fix:** Changed to `q in value` for correct partial, case-insensitive matching.

### Bug #2 — Hype Ratio Always 1.00 (playlist_logic.py)
- **Problem:** Stats always showed Hype Ratio = 1.00 regardless of actual playlist counts.
- **Cause:** `total = len(hype)` used Hype count as denominator instead of total songs.
- **Fix:** Changed to `total_songs = len(all_songs)` as the correct denominator.

### Bug #3 — Average Energy Was Wrong (playlist_logic.py)
- **Problem:** Average energy only reflected Hype songs, not all songs.
- **Cause:** Energy was summed from `hype` list but divided by total songs — mismatched math.
- **Fix:** Changed to sum energy from `all_songs` for accurate average.

---

## 🔧 Refactor

Extracted inline keyword checks in `classify_song` into two named helper functions:
- `contains_hype_keyword(genre)` — checks if genre contains rock, punk, or party
- `contains_chill_keyword(title)` — checks if title contains lofi, ambient, or sleep

Same behavior, clearer intent, easier to maintain and reuse.

---

## 📝 Git History

| Commit | Description |
|--------|-------------|
| `87d0cdc` | refactor: extracted keyword checks into helper functions |
| `2d5c500` | fix: corrected hype_ratio and avg_energy calculations |
| `c60d787` | fix: resolved case-insensitive partial match bug in search |

---

## 🛠 Tech Stack
- Python
- Streamlit
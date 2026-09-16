# 🎵 Suno Song Prompt Creator

A web app for crafting perfect [Suno AI](https://suno.ai) prompts, built from the wisdom of the **SUNO-Bible** ([xerohour/SUNO-Bible](https://github.com/xerohour/SUNO-Bible)).

## ✨ Features

### 🎯 Style Builder
Build style prompts using the Universal Prompt Formula:
```
decade, genre, subgenre, country, vocalist info, style + mood + instruments
```
- Dropdowns for decade, genre, vocalist, tempo
- Mood & instrument pickers
- **Pop Gravity Well protection** — one-click exclusions (`no pop`, `no polished hooks`, etc.)
- Live character count (Suno limit: 1000)
- Randomize for inspiration

### 🏗️ Song Structure Builder
- Proper SUNO tags: `[Intro]`, `[Verse]`, `[Pre-Chorus]`, `[Chorus]`, `[Bridge]`, `[Solo]`, `[Interlude]`, `[Break]`, `[Outro]`, `[End]`
- Modifiers: `[Haunting Whispered Pre-Chorus]`, `[Dreamy Slow Intro]`
- Lyric expression tips: `...` slows, `!` emphasizes, `(parenthesis)` = call-response, `ooooh` = vocalizations
- Template loader + full tagged lyrics output (5000 char count)

### 🎤 Artist Library
- Searchable database from SUNO-Bible's `artist-database.json`
- 40+ artist emulation prompts (Beatles, Pink Floyd, Queen, etc.)
- One-click "Use this prompt"

### 📖 Bible Guide
Quick reference for Style-Mesh Theory, Gravity Wells, Sacred Strategies.

## 🚀 Use

Just open `index.html` in a browser — no build step. Or deploy to GitHub Pages:

1. Push to GitHub
2. Settings → Pages → Deploy from branch → `main` / `/ (root)`
3. Your app is live!

## 📚 Source Wisdom

Built from:
- `SUNO_BIBLE.md` — Complete grimoire (style-mesh theory, strategies)
- `SUNO_SYNTAX.md` — Tag syntax & modifiers
- `CHEATSHEET.md` — Quick reference & formulas
- `artist-database.json` — 40+ artist prompts

See the [SUNO-Bible](https://github.com/xerohour/SUNO-Bible) for the full grimoire.

## 📄 License
MIT

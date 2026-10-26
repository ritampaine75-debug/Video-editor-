# Coordinate Motion Studio

**AI-Directed Procedural Motion Graphics, Timeline Editing & Video Rendering Platform**

> Text model generates *instructions* → Browser renderer generates *pixels*. No paid AI API, no cloud encoding required.

![License: MIT](https://img.shields.io/badge/License-MIT-cyan.svg)
![Version](https://img.shields.io/badge/version-1.0.0-blue)
![Protocol](https://img.shields.io/badge/protocol-coordinate--motion--v1-purple)

---

## ✨ Live Demo

**Website:** `https://ritampaine75-debug.github.io/Video-editor-/`

> After pushing to `main`, GitHub Pages serves `index.html` directly. No build step.

Local: just open `index.html` in a browser.

---

## 🎯 Problem Solved

Professional motion graphics usually need After Effects or heavy SaaS. Coordinate Motion Studio lets **any LLM** (ChatGPT, Gemini, Grok, DeepSeek, Claude) generate an editable animation *project* as JSON, which a local-first browser editor previews and exports — mobile-ready, deterministic, open-source.

---

## 🧭 Architecture Diagram

```
[User Script/Concept]
        ↓ (paste CUSTOM_PROMPT.md into AI)
[LLM] → generates coordinate-motion-v1 JSON (scenes, tracks, objects, keyframes, effects)
        ↓ (Paste/Upload JSON into Studio)
[Parser + Validator] → [Project State (single source)] → [Interpolation Engine + Canvas2D Renderer]
        ↓                                              → [Timeline Editor ↔ Properties ↔ Keyframe Editor]
        ↓                                              → [Preview Canvas (play/pause/scrub)]
        ↓                                              → [Export: MediaRecorder (WebM) / PNG Frame]
```

*No eval, no external font assumption, no giant frame buffer.*

---

## 🔄 AI → JSON → Animation Workflow

1. **Choose Preset** on site: *Vertical Short* (1080×1920, 9:16) or *YouTube Full* (1920×1080, 16:9). Configures composition, FPS (30 default, 60 optional), safe areas.
2. **Get AI Instructions**: *Download Custom Prompt*, *Copy Prompt*, *Download Skill*, or *Share* via Web Share API (with fallback).
3. **Share with AI**: Paste `CUSTOM_PROMPT.md` into ChatGPT/Gemini/etc. AI asks: "What kind of video would you like to create?"
4. **Describe video** → AI returns `project.json` or JSON code block (complete, valid).
5. **Import** in Studio: *Import → Paste / Upload / Drag-Drop* → validates, builds timeline, renders preview.
6. **Edit** directly: change props, keyframes, tracks, scenes — single authoritative state, live preview.
7. **Export**: `MediaRecorder` WebM (checked MIME) or PNG sequence; audio mux noted if unsupported.

> The AI never generates frames, only animation instructions and keyframes evaluated per timestamp.

---

## 📁 Project Structure

```
coordinate-motion-studio/
├── index.html                          # Single-file app (HTML+CSS+JS)
├── CUSTOM_PROMPT.md                    # AI instruction (28 sections)
├── SKILL.md                            # Skill definition
├── PROTOCOL.md                         # coordinate-motion-v1 spec
├── SECURITY.md                         # Security policy
├── README.md, LICENSE, CONTRIBUTING.md, CHANGELOG.md
├── data/
│   ├── motion-graphics-catalog.json    # 110 effects catalog
│   ├── transitions.json
│   ├── typography-effects.json
│   ├── logo-animations.json
│   ├── particles.json
│   ├── ui-animations.json
│   ├── compositing-effects.json
│   └── easing-presets.json
├── schemas/coordinate-motion-v1.schema.json
├── examples/ (6 projects)
└── docs/ (architecture, animation-system, timeline-editor, etc.)
```

---

## 🚀 Quick Start

### Use Hosted Version
1. Visit `https://ritampaine75-debug.github.io/Video-editor-/`
2. Click **Vertical Short** or **YouTube Video** to set preset.
3. Click **Download Custom Prompt** → share with your AI.
4. Import returned JSON → Edit → Export.

### Run Locally
```bash
git clone https://github.com/ritampaine75-debug/Video-editor-.git
cd Video-editor-
# No npm install needed — open directly:
open index.html
# or serve:
python -m http.server 8000
# then http://localhost:8000
```

### GitHub Pages Deploy
1. Push to `main` (already configured)
2. Repo Settings → Pages → Source: Deploy from branch → `main` / `/ (root)` → Save
3. Wait ~1 min → site live at `https://<user>.github.io/<repo>/`

---

## 🤖 Custom Prompt Sharing

Dedicated panel in header:
- **Download CUSTOM_PROMPT.md** (real file via Blob)
- **Download SKILL.md**
- **Copy Custom Prompt** / **Copy Activation Prompt** (short)
- **Share** (Web Share API with `navigator.canShare({files})` check; fallback to download)
- Instructions for manual attach

Does not pretend Share auto-sends to ChatGPT; user picks destination.

---

## 🧠 AI Model Compatibility

Any instruction-following model works. No API keys. Tested conceptual path for ChatGPT, Gemini, Grok, DeepSeek. Fallback: JSON code block if no file attachment.

---

## 📜 JSON Protocol (coordinate-motion-v1)

Key top-level: `protocol`, `metadata`, `composition`, `scenes`, `tracks`, `objects`, `assets`, `audio`, `exportSettings`.

- **Keyframe time = absolute project seconds** (consistent)
- Interpolation with easing, deterministic
- Layer order by track order + object order
- See `PROTOCOL.md` and `schemas/coordinate-motion-v1.schema.json`

Validation: ranges, colors, references, durations, canvas limits. Report identifies scene/track/object/property.

---

## 🎨 Effect Catalog

~110 entries across transitions, motion, typography, logo, particles, UI, compositing, light, distortion, camera, principles, data-viz. Each has id, category, description, complexity, renderer, params schema, status (`implemented`/`experimental`/`planned`), fallback, performance cost.

UI **only lists implemented** by default; toggle to see planned.

Implemented subset: cut, dissolve, fade-to-color, wipe/slide/push, zoom, iris, split/shape reveal, blur, glitch, flash + 20+ motion + typography + particles + compositing.

---

## ⏱ Timeline Editing

- Ruler + playhead + scrub (pointer/touch)
- Zoom (0.5-4x) + horizontal scroll
- Track rows: visibility, lock, mute
- Clip blocks sized by duration
- Keyframe diamonds, add/delete, time/value edit via inspector
- Snapping (Shift)
- Undo/Redo

Mobile: collapsible panels, tab nav, touch-friendly timeline, bottom sheets.

---

## 🎬 Video Export

- **MediaRecorder**: `canvas.captureStream(fps)` + audio mix where supported; MIME checked (`vp9` → `vp8` → `webm`)
- **PNG**: `toDataURL` per current frame
- **Future**: WASM FFmpeg for MP4 (documented, not required)
- Warnings when profile unsupported; no paid API needed

Export settings: dimensions, fps, duration, format, quality, filename.

---

## 📱 Mobile First

- Responsive: desktop 3-panel layout; mobile tab layout
- Touch scrubbing, collapsible editor
- Preview preserves aspect ratio, scales to viewport
- Tested on modern Android Chrome / iOS Safari / Desktop Chrome/Firefox

---

## 🔒 Security

- Imported JSON = untrusted; no eval/Function/innerHTML
- textContent / canvas fillText only
- Color/ranges/refs validated, clamped
- Canvas max 8192, duration 3600s, file 50MB

See `SECURITY.md`.

---

## ⚡ Performance Limits

- Particle count ≤150 (default 60-120)
- Blur radius ≤32
- Tracks ≤20, objects ≤50 recommended
- Preview 0.5x toggle for low-end devices
- Bounded buffers, chunked offline render, cancellation support

---

## 🌐 Supported Browsers

- Chrome 90+, Edge 90+, Firefox 90+ (full MediaRecorder)
- Safari 16+ (preview, PNG; recording may fallback)
- Android Chrome (share sheet supported)
- iOS Safari (download fallback)

Shows compatibility message if `captureStream`/`MediaRecorder` missing.

---

## 🧪 Testing

- Example projects validate against schema
- Interpolation unit checks in console
- Timeline seek/scrub determinism
- Export tested where APIs available
- GitHub Actions: JSON syntax + protocol compliance + catalog size

---

## 🤝 Contributing

See `CONTRIBUTING.md`. Fork → edit `index.html` → test with examples → PR. Tag new effects properly.

---

## 📄 License

MIT © 2025 Coordinate Motion Studio

---

## ❓ Known Limitations

- WebM primary; MP4 requires local FFmpeg/WASM transcoding (not bundled)
- Audio+Video mux varies by browser; manual mux documented
- WebGL effects planned, not all implemented; fallback provided
- No AI video generation — AI generates editable structured data, renderer draws frames

*This distinction is intentional: local-first, editable, reproducible.*

# Architecture

## Overview
Coordinate Motion Studio is a single-file browser app (`index.html`) with zero build step. It implements:

```
Input (JSON / AI) -> Parser -> Validator -> Project State -> Renderer -> Canvas -> Export
                                      \-> Timeline Editor -> Properties -> (mutates State)
```

## Modules inside index.html
- **State Store**: single authoritative `project` object + `history` stacks for undo/redo
- **Parser**: JSON.parse with try/catch, size limit
- **Validator**: schema + reference + range checks, returns report
- **Interpolation Engine**: easing functions, lerp, color lerp, keyframe lookup (binary search)
- **Render Pipeline**:
  1. clear canvas with composition.background or scene background
  2. collect active objects (start <= t < start+duration && track.enabled)
  3. sort by track order
  4. for each object, compute interpolated props at t
  5. apply scene transition alpha/clip if t in transition window
  6. draw (fillText, fillRect, arc, etc.)
  7. post-effects (glow via shadowBlur, dropShadow, chromatic via offscreen copy)
- **Timeline**: DOM-based rows, playhead via requestAnimationFrame, scrub via pointer events, zoom via CSS scale
- **Export**: MediaRecorder from canvas.captureStream(fps) + optional audio mixing; PNG via toDataURL

## Why Single File?
- GitHub Pages can serve raw file
- No npm install for users
- Easy to audit, copy, fork
- Mobile-friendly load (~200KB gzipped)

## Data Flow
User paste JSON -> validator -> if ok, set project + render -> timeline builds DOM -> selection updates inspector -> inspector edits mutate project -> re-render.

## Performance
- Bounded buffers: only current frame kept in memory
- Preview at composition size; optional 0.5x preview mode for low-end devices
- Particle count capped at 150
- Blur radius capped at 32px

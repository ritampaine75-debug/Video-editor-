# Coordinate Motion Protocol v1

## Overview
`coordinate-motion-v1` is a versioned JSON protocol for describing motion graphics as deterministic, editable data that a browser renderer can execute without AI inference.

## Core Principle
> The AI generates *instructions*, the renderer generates *pixels*.

The AI never generates video frames directly. It generates scenes, objects, keyframes, effects, and transitions. The renderer interpolates properties per timestamp.

## Top-Level Structure
```json
{
  "protocol": "coordinate-motion-v1",
  "metadata": { "title": "My Video", "version": 1 },
  "composition": { "width": 1920, "height": 1080, "fps": 30, "duration": 10, "background": "#101018" },
  "scenes": [...],
  "tracks": [...],
  "objects": [...],
  "assets": [...],
  "audio": [...],
  "exportSettings": {...}
}
```

### metadata
- `title` (string, required)
- `version` (integer, default 1)
- `description`, `author`, `created`

### composition
- `width`, `height` (64-8192)
- `fps` (12,15,24,25,30,48,50,60)
- `duration` (0.1-3600 seconds)
- `background` (hex color)

### scenes
Logical sections. Each has `id`, `start`, `duration`, optional `background`, `transitionIn/Out`.
Scenes are for organization; objects are visible if their own time window is active regardless of scene, but scene background is drawn.

### tracks
Layers: `graphics`, `text`, `shape`, `image`, `audio`, `effect`
- `enabled` (visible), `locked` (prevent edits), `muted` (audio only)

### objects
Drawable entities:
- `id`, `type`, `trackId`, `sceneId?`, `start`, `duration`
- `properties`: base visual state (x,y,width,height,radius,fill,stroke,opacity,scaleX/scaleY,rotation,font*,align,content,letterSpacing,etc.)
- `keyframes`: array of `{time, properties, easing}` where `time` is **absolute project time in seconds**
- `effects`: array of `{id, enabled, params}`

#### Keyframe Time Convention
**Absolute project time.** A keyframe at `time: 1.5` means 1.5s from composition start, not object-relative. This allows global scrubbing to be deterministic. If `time` is outside object active window, it is ignored until window overlaps.

#### Interpolation
Between two keyframes, the renderer linearly interpolates with easing:
- Find surrounding keyframes k0 <= t <= k1
- Compute progress `p = (t - k0.time)/(k1.time - k0.time)`
- Apply easing function to p
- Lerp each property: numeric via `lerp`, colors via RGB lerp, etc.

Base `properties` are used when no keyframes affect that property or when before first keyframe.

#### Layer Order
Objects are drawn in `tracks` order (first track = bottom) then by `objects` array order within same track.

### assets
Optional preloaded media: `{id, type, src, name}` - src can be data URL or HTTPS URL.

### audio
`{id, src, start, duration, volume 0-1, trimStart, trimEnd}`

### exportSettings
`{format: webm|mp4|gif|png-sequence, quality, bitrate, filename}`

## Effects
Effect IDs must exist in `data/motion-graphics-catalog.json` with `status: implemented` to guarantee rendering. Planned effects are listed for AI awareness but must have fallback.

## Transitions
Defined per scene: `{type, duration, easing, color, direction}`. Renderer crossfades canvases or slices.

## Validation Rules
- protocol must equal "coordinate-motion-v1"
- All IDs must be kebab/ snake alphanumeric with hyphens/underscores
- trackId must reference existing track
- keyframe times must be >=0 and <= composition.duration
- colors must be #RGB, #RRGGBB, #RRGGBBAA, or rgba()
- Numeric ranges enforced per property
- Canvas area width*height*fps*duration bounded to prevent OOM

## Determinism
- `t` evaluation is pure function of timestamp, not frame count
- Seeded RNG for particles: `seed = hash(project.title + object.id)`
- No Date.now() in render; only composition time

## Example
See `examples/animated-title.json`.

# Timeline Editor

## Features
- Time ruler with ticks (major per second, minor 0.25s)
- Playhead draggable (pointer events)
- Zoom: 0.5x to 4x (CSS transform on inner container)
- Horizontal scroll
- Track rows: name, eye (visible), lock, mute
- Clip blocks: absolute positioned divs, width = duration * pxPerSecond
- Keyframe markers: diamonds on clip, clickable to select
- Snapping: 0.1s grid when holding Shift
- Context: right-click clip -> duplicate/delete/split
- Selection syncs to Properties panel

## Mobile
- Timeline collapses into swipeable track list + large playhead handle
- Touch scrubbing supported
- Clip controls via bottom sheet

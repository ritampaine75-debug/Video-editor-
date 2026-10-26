# Changelog

All notable changes to Coordinate Motion Studio will be documented here.

## [1.0.0] - 2025-10-27
### Added
- Initial release of Coordinate Motion Studio
- coordinate-motion-v1 JSON protocol with full schema
- Browser-based editor with Canvas 2D renderer
- Timeline with scrubbing, zoom, snapping, keyframe editing
- Track management (visibility, lock, mute, reorder)
- Properties inspector with live preview
- Effect catalog (110 entries) with implemented/ planned distinction
- Transitions library (17 implemented transitions)
- Typography presets (16)
- UI animation presets
- Particle emitters
- Compositing effects (drop shadow, glow, gradient mesh, chromatic aberration)
- Easing presets (16)
- MediaRecorder-based WebM export with fallback messaging
- PNG frame export
- Presets for YouTube 16:9 and Vertical 9:16
- Audio track support (import, volume, trim, mute)
- JSON import via paste/upload/drag-drop with validation report
- Undo/Redo system
- Mobile-responsive layout with collapsible panels and touch timeline
- CUSTOM_PROMPT.md and SKILL.md for AI integration
- 6 example projects
- Documentation suite
- GitHub Actions validation workflow
- GitHub Pages deployment ready

### Security
- No eval/Function usage for imported JSON
- Strict validation of colors, ranges, references
- XSS prevention via textContent sanitization

## [Unreleased]
### Planned
- WebGL filter pipeline
- WASM FFmpeg for MP4 transcoding
- Path morphing
- Advanced particle physics

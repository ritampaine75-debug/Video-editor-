# Contributing to Coordinate Motion Studio

## Getting Started
1. Fork the repository
2. Clone locally: `git clone https://github.com/your-fork/Video-editor-.git`
3. Open `index.html` directly in a browser - no build step required
4. Make your changes and test with example projects in `examples/`

## Development Guidelines
- Keep `index.html` self-contained (embedded CSS/JS)
- Document new effects in `data/motion-graphics-catalog.json` with proper `status` field
- Add schema entries for new protocol fields
- Ensure mobile responsive behavior
- Validate with `npm run validate` if available or check browser console

## Adding Effects
Each effect needs:
- Stable ID (kebab-case)
- Category, description, complexity
- Parameter schema with types/ranges/defaults
- Rendering implementation in index.html
- Fallback behavior
- Performance cost rating

Mark as `experimental` if not fully tested, `planned` if not implemented.

## Pull Requests
- Use descriptive titles
- Reference any related issue
- Include before/after screenshots for UI changes
- Ensure no arbitrary code execution from imported JSON

## Code of Conduct
Be respectful, constructive, and inclusive.

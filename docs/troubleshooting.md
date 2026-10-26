# Troubleshooting

## Import fails
- Check JSON is valid (use Validate button)
- Ensure protocol = "coordinate-motion-v1"
- Check required fields: composition.width/height/fps/duration/background
- See validation report for specific object/property

## Preview black
- Check composition.background is valid hex
- Check track.enabled = true
- Check object start/duration includes current time

## Export not working
- Chrome/Edge/Firefox support MediaRecorder; Safari may not
- Check browser console for mimeType support
- Try WebM vp8 if vp9 fails
- Use PNG export as fallback

## Timeline not smooth
- Reduce particle count
- Use 0.5x preview resolution toggle
- Close other tabs

## Mobile layout broken
- Use latest Chrome Android / Safari iOS
- Rotate to landscape for timeline editing

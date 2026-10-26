# Rendering and Export

## Canvas 2D
Primary renderer. All text via `ctx.fillText` after setting font, shadow, etc. Shapes via `fillRect`, `arc`, `ellipse`, `beginPath`.

## WebGL (Optional)
Planned for wave-distort, depth-of-field. Current fallback is skip or CPU approx.

## Export
### MediaRecorder path (preferred)
1. `canvas.captureStream(fps)` -> video track
2. If audio elements exist, capture via Web Audio `MediaStreamDestination` + add to stream (where supported)
3. `new MediaRecorder(stream, {mimeType: checkedType})`
4. `ondataavailable` chunks -> Blob -> URL -> download
5. MIME check: `MediaRecorder.isTypeSupported('video/webm;codecs=vp9')` fallback to vp8 then generic webm

### PNG Sequence path
`canvas.toDataURL('image/png')` per frame via offline loop (not recording, just stepping t and capturing).

### Limitations Documented
- Safari may not support captureStream; message shows alternative (PNG + external FFmpeg)
- Audio+Video muxing not reliable in all browsers; docs explain manualmux with FFmpeg
- MP4 not guaranteed natively; WebM is primary

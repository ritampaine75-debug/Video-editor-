# Effect Authoring

## Adding a New Effect
1. Choose stable ID: `my-effect`
2. Add entry to `data/motion-graphics-catalog.json` with status `implemented` or `experimental`
3. In `index.html`, add to `EFFECTS` registry:
```js
EFFECTS['my-effect'] = {
  params: { intensity: {type:'number', min:0, max:1, default:0.5}},
  apply(ctx, obj, t, params, baseDraw) { // wrap draw
  }
}
```
4. Validator auto-picks up catalog entry
5. Effects browser will list it if supported

## Performance Profile
Tag as low/medium/high. High effects disabled in low-power preview mode.

## Fallback
If effect unsupported on device, renderer logs warning and draws without it; project data preserved.

# Animation System

## Easing
16 presets implemented as pure functions `f(p)` where p in [0,1]:
- linear
- Quad, Cubic, Quart, Quint (in/out/inOut)
- Back (overshoot)
- Bounce, Elastic, Expo

Deterministic; tested via unit console checks.

## Keyframe Evaluation
```js
function getPropAt(obj, prop, t) {
  const kfs = obj.keyframes.filter(k => prop in k.properties).sort((a,b)=>a.time-b.time)
  if (!kfs.length) return obj.properties[prop]
  if (t <= kfs[0].time) return kfs[0].properties[prop]
  if (t >= kfs[kfs.length-1].time) return kfs[kfs.length-1].properties[prop]
  // find segment
  // apply easing
}
```

Supports multiple keyframes per property, different easings per segment.

## Property Types
- number (x,y,opacity,rotation,scale,width,height,letterSpacing)
- color (fill, stroke) - hex/rgba lerp
- string (content, fontFamily) - step (no interpolation)
- boolean - step

## Deterministic RNG
```
seed = cyrb128(title + id)
rand = sfc32(seed)
```
Same project always produces same particle positions.

## Frame Independence
Rendering `t=5.0` does not depend on having rendered 0-4.99. Enables scrubbing and offline rendering in any order.

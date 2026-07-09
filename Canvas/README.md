# Canvas

> 2D drawing on the web. Games, image manipulation, custom charts.

---

## Purpose

Master HTML5 Canvas for high-performance 2D graphics.

## Prerequisites

- [JavaScript/](../JavaScript/).

## Learning Outcome

You can draw shapes, text, and images; handle interaction; and optimize canvas performance.

## Dependencies

- Browser.

## Related Files

- [SVG/](../SVG/) · [WebGL/](../WebGL/) · [ThreeJS/](../ThreeJS/) · [Animations/](../Animations/)

## AI Instructions

When using Canvas:
1. Use Canvas for many objects, frequent redraws, or pixel manipulation.
2. Use SVG for static or simple vector graphics.
3. Use WebGL for 3D or 10k+ objects.
4. Handle `devicePixelRatio` for crisp rendering.
5. Use `requestAnimationFrame`, not `setInterval`.
6. For interactivity, track hit regions or use isPointInPath.

## Human Notes

### Canvas vs SVG vs WebGL
| Need | Use |
|---|---|
| Static icon | SVG |
| Interactive chart, <100 elements | SVG |
| Many shapes, frequent redraw | Canvas |
| 3D | WebGL (Three.js) |
| Image manipulation | Canvas |
| Filter effects | CSS filter / SVG filter / WebGL |

### Setup
```html
<canvas id="c" width="800" height="600"></canvas>
<script>
const canvas = document.getElementById('c');
const ctx = canvas.getContext('2d');

// Handle high-DPI
const dpr = window.devicePixelRatio || 1;
canvas.width = 800 * dpr;
canvas.height = 600 * dpr;
canvas.style.width = '800px';
canvas.style.height = '600px';
ctx.scale(dpr, dpr);
```

### Drawing
```js
// Rect
ctx.fillStyle = 'red';
ctx.fillRect(10, 10, 100, 100);

// Path
ctx.beginPath();
ctx.moveTo(50, 50);
ctx.lineTo(100, 100);
ctx.lineTo(150, 50);
ctx.closePath();
ctx.fill();

// Circle
ctx.beginPath();
ctx.arc(400, 300, 50, 0, Math.PI * 2);
ctx.fill();

// Text
ctx.font = '24px Inter';
ctx.fillStyle = 'black';
ctx.fillText('Hello', 100, 100);

// Image
const img = new Image();
img.onload = () => ctx.drawImage(img, 0, 0);
img.src = '/image.png';
```

### Animation loop
```js
function loop() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);
  // draw
  requestAnimationFrame(loop);
}
requestAnimationFrame(loop);
```

### Hit testing
```js
canvas.addEventListener('click', (e) => {
  const rect = canvas.getBoundingClientRect();
  const x = e.clientX - rect.left;
  const y = e.clientY - rect.top;
  // check if (x, y) is in any object
});
```

### Performance
- Avoid allocations in the loop.
- Batch draw calls.
- Use `OffscreenCanvas` for workers (where supported).
- Don't redraw static parts — use multiple canvases.
- Use `globalAlpha` over `rgba()` for transparency.

### Saving/restoring state
```js
ctx.save();
ctx.translate(100, 100);
ctx.rotate(Math.PI / 4);
// draw
ctx.restore();
```

## Common Mistakes

- ❌ Not handling `devicePixelRatio` (blurry on retina).
- ❌ `setInterval` instead of `requestAnimationFrame`.
- ❌ Allocating in the loop.
- ❌ Not clearing between frames.
- ❌ Pixel-based hit testing for complex shapes.

## Tools

- Konva.js: high-level canvas library. https://konvajs.org/
- PixiJS: 2D WebGL/Canvas library. https://pixijs.com/
- Fabric.js: canvas manipulation. http://fabricjs.com/
- p5.js: creative coding. https://p5js.org/

## References

- MDN Canvas: https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API
- Canvas Tutorial: https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial

## Exercises

1. Draw a smiley face.
2. Animate a bouncing ball.
3. Make a clickable canvas with hit detection.

## Projects

- Build a simple drawing app (lines, colors, save).
- Build a particle system.

---

**Previous:** [SVG/](../SVG/) · **Next:** [WebGL/](../WebGL/) · **Related:** [Animations/](../Animations/)

# WebGL

> GPU-accelerated 3D and 2D graphics in the browser. Shaders, buffers, pipelines.

---

## Purpose

Understand WebGL fundamentals. In practice, you'll use Three.js or another library, but knowing the underlying model makes you effective.

## Prerequisites

- [JavaScript/](../JavaScript/), [Canvas/](../Canvas/), linear algebra basics.

## Learning Outcome

You understand the WebGL pipeline, can write basic shaders, and can debug WebGL apps.

## Dependencies

- Modern browser.

## Related Files

- [ThreeJS/](../ThreeJS/) · [Canvas/](../Canvas/) · [Animations/](../Animations/)

## AI Instructions

When building 3D/complex graphics:
1. **Default to Three.js** (or React Three Fiber). Don't write raw WebGL unless required.
2. **For simple shaders**, use libraries like `glsl-canvas` or OGL.
3. **Profile**: GPU work is expensive. Use `requestAnimationFrame`, not `setInterval`.
4. **Optimize**: instancing, frustum culling, LOD.
5. **Mobile**: WebGL is supported but slow. Test on real devices.

## Human Notes

### The pipeline
1. Vertex shader — transforms vertices.
2. Rasterization — converts triangles to pixels.
3. Fragment shader — colors pixels.
4. Output to framebuffer.

### Shaders (GLSL)
```glsl
// Vertex shader
attribute vec3 position;
uniform mat4 modelView;
uniform mat4 projection;
void main() {
  gl_Position = projection * modelView * vec4(position, 1.0);
}

// Fragment shader
precision mediump float;
uniform vec3 color;
void main() {
  gl_FragColor = vec4(color, 1.0);
}
```

### Buffers
- Vertex positions, normals, UVs, indices.
- Upload once, render many times.

### WebGL2 vs WebGL1
- WebGL2 is widely supported. Use it.
- WebGL2: instancing, transform feedback, 3D textures, etc.

### WebGPU (future)
- Modern API. Replacing WebGL over the next few years.
- Lower-level, more performant.
- Currently in Chrome/Edge/Safari (partial). Firefox in progress.

### When to use WebGL
- 3D scenes (use Three.js).
- Complex particle systems.
- Image filters at scale.
- Data viz with >10k points.
- Games.

### When NOT to use
- Static images (SVG).
- Simple charts (Canvas or chart lib).
- Hover effects (CSS).

## Common Mistakes

- ❌ Writing raw WebGL when Three.js would do.
- ❌ Not handling context loss (`webglcontextlost`).
- ❌ Loading 10MB textures.
- ❌ No mobile testing.
- ❌ Forgetting to resize canvas on viewport change.

## Tools

- Three.js: https://threejs.org/
- React Three Fiber: https://docs.pmnd.rs/react-three-fiber
- Babylon.js: https://www.babylonjs.com/
- PixiJS: https://pixijs.com/ (2D)
- OGL: https://github.com/oframe/ogl (lightweight)
- glsl-canvas: https://github.com/fabrikkation/glsl-canvas

## References

- WebGL Fundamentals: https://webglfundamentals.org/
- The Book of Shaders: https://thebookofshaders.com/
- MDN WebGL: https://developer.mozilla.org/en-US/docs/Web/API/WebGL_API
- Three.js Journey (course): https://threejs-journey.com/

## Further Reading

- *Interactive Computer Graphics* — Edward Angel
- *The Book of Shaders* — Patricio Gonzalez Vivo & Jen Lowe (free)
- *Learn WebGL* — https://learnwebgl.brown37.net/

## Exercises

1. Draw a triangle with raw WebGL.
2. Recreate the triangle in Three.js. Compare code.
3. Write a fragment shader that animates a gradient.

## Projects

- Build a 3D product configurator.
- Build a particle system with shaders.

---

**Previous:** [Canvas/](../Canvas/) · **Next:** [ThreeJS/](../ThreeJS/) · **Related:** [Animations/](../Animations/)

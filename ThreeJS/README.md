# Three.js

> The de-facto 3D library for the web. Built on WebGL.

---

## Purpose

Master Three.js for 3D scenes, models, animations, post-processing.

## Prerequisites

- [JavaScript/](../JavaScript/), [WebGL/](../WebGL/) concepts.

## Learning Outcome

You can build interactive 3D scenes, load models, add lights and shadows, and optimize for production.

## Dependencies

- Three.js (npm).

## Related Files

- [WebGL/](../WebGL/) · [Canvas/](../Canvas/) · [Animations/](../Animations/)

## AI Instructions

When building 3D:
1. Use Three.js (or React Three Fiber for React).
2. Reuse geometries and materials.
3. Use `InstancedMesh` for many similar objects.
4. Compress textures (Basis Universal / KTX2).
5. Use `DRACOLoader` for compressed meshes.
6. Add frustum culling (default in Three.js).
7. Use LOD (Level of Detail) for distant objects.
8. Test on mobile. 3D is heavy.
9. Always provide a poster image / loading state.

## Human Notes

### Scene setup
```js
import * as THREE from 'three';

const scene = new THREE.Scene();
const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
camera.position.z = 5;

const renderer = new THREE.WebGLRenderer({ antialias: true });
renderer.setSize(window.innerWidth, window.innerHeight);
document.body.appendChild(renderer.domElement);

const geometry = new THREE.BoxGeometry();
const material = new THREE.MeshStandardMaterial({ color: 0x00ff00 });
const cube = new THREE.Mesh(geometry, material);
scene.add(cube);

const light = new THREE.DirectionalLight(0xffffff, 1);
light.position.set(1, 1, 1);
scene.add(light);

function animate() {
  requestAnimationFrame(animate);
  cube.rotation.x += 0.01;
  cube.rotation.y += 0.01;
  renderer.render(scene, camera);
}
animate();
```

### React Three Fiber (R3F)
Declarative Three.js for React.
```jsx
import { Canvas } from '@react-three/fiber';

function Box() {
  const ref = useRef();
  useFrame(() => {
    ref.current.rotation.x += 0.01;
  });
  return (
    <mesh ref={ref}>
      <boxGeometry />
      <meshStandardMaterial color="green" />
    </mesh>
  );
}

function App() {
  return (
    <Canvas>
      <Box />
      <ambientLight />
      <directionalLight position={[1, 1, 1]} />
    </Canvas>
  );
}
```

### Loading models
- GLTF/GLB (recommended).
- Use `GLTFLoader`.
- Compress with `DRACOLoader` + Draco compression.
- Convert to GLB for smaller size.

### Textures
- Use KTX2 / Basis Universal for compressed textures.
- Resize to power-of-2 if you need mipmaps (legacy; modern GPUs handle non-POT).
- Use texture atlases for many small textures.

### Performance
- `InstancedMesh` for thousands of similar objects.
- Reuse geometries and materials.
- Use `BufferGeometry` (default).
- LOD for distant objects.
- Frustum culling (default).
- `requestAnimationFrame`, not `setInterval`.
- Pause when off-screen.

### Post-processing
- Bloom, SSAO, DOF, etc.
- Use `EffectComposer`.

### Shaders
- Custom `ShaderMaterial` or `RawShaderMaterial`.
- GLSL.

### Shadows
- Expensive. Use sparingly.
- `PCFSoftShadowMap` for quality.

### Mobile
- Reduce pixel ratio (`renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2))`).
- Fewer lights.
- Smaller textures.
- Simpler shaders.

## Common Mistakes

- ❌ Loading 50MB GLB files.
- ❌ Uncompressed textures.
- ❌ No loading state.
- ❌ No mobile testing.
- ❌ Too many draw calls.
- ❌ Lights everywhere (use baked lighting if possible).
- ❌ Not handling WebGL context loss.

## Tools

- Three.js: https://threejs.org/
- React Three Fiber: https://docs.pmnd.rs/react-three-fiber
- Drei (R3F helpers): https://github.com/pmndrs/drei
- Three.js Editor: https://threejs.org/editor/
- gltf.report: https://gltf.report/
- glTF Transform: https://gltf-transform.donmccurdy.com/
- Draco: https://github.com/google/draco

## References

- Three.js docs: https://threejs.org/docs/
- Three.js examples: https://threejs.org/examples/
- Discover Three.js: https://discoverthreejs.com/
- Three.js Journey (course, paid): https://threejs-journey.com/
- Bruno Simon's portfolio (inspiration): https://bruno-simon.com/

## Further Reading

- *Learn Three.js* — Jos Dirksen
- *Game Development with Three.js* — Jason Canfield

## Exercises

1. Build a rotating cube with lighting.
2. Load a GLB model from Sketchfab and render it.
3. Build an interactive 3D product viewer (rotate + zoom).

## Projects

- Build a 3D portfolio site.
- Build a 3D data viz (globe with bars).
- Build a small 3D game.

---

**Previous:** [WebGL/](../WebGL/) · **Next:** [Performance/](../Performance/) · **Related:** [Animations/](../Animations/)

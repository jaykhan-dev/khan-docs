---
tags:
  - trois js
  - three js
  - 3d graphics
  - webgl
  - vue js
  - animation
  - web 3d
  - canvas
---

# Trois JS

Based on [Three JS](), [Trois]() is made specifically for Vue. This code is a simple setup that displays a [torusKnot]()

## Install

Add to an existing Vue JS project

```bash
npm i three troisjs
```

## `template`

```html
<template>
  <div class="">
    <Renderer ref="renderer" antialias resize="window" orbit-ctrl>
      <Camera :position="{ z: 10 }" />
      <Scene background="#18181B">
        <PointLight :position="{ y: 50, z: 50 }" />
        <TorusKnot
          @pointerOver="onPointerOver"
          ref="torusKnot"
          :rotation="{ y: Math.PI / 4, z: Math.PI / 4 }"
        >
          <LambertMaterial />
        </TorusKnot>
      </Scene>
    </Renderer>
  </div>
</template>
```

## `script`

```html
<script>
  import {
    Renderer,
    Scene,
    Camera,
    Box,
    TorusKnot,
    PointLight,
    LambertMaterial,
  } from "troisjs";

  export default {
    components: {
      Renderer,
      Scene,
      Camera,
      Box,
      TorusKnot,
      PointLight,
      LambertMaterial,
    },
    mounted() {
      //orbitCtrl.enableZoom = false;

      const renderer = this.$refs.renderer;
      const orbitCtrl = this.$refs.renderer.three.cameraCtrl;
      orbitCtrl.enableZoom = false;
      const torusKnot = this.$refs.torusKnot.mesh;
      renderer.onBeforeRender(() => {
        torusKnot.rotation.x += 0.01;
        torusKnot.rotation.y += 0.01;
      });
    },
    created() {
      //orbitCtrl.enableZoom = false;
    },
    methods: {
      onPointerOver(event) {
        event.component.mesh.material.color.set(
          event.over ? 0x05a6cc : 0xf7c863
        );
      },
    },
  };
</script>
```

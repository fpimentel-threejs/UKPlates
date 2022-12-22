<template>
  <Renderer ref="rendererC" antialias :orbit-ctrl="{ enableDamping: true }" resize="window">
    <Camera :position="{ z: 10 }" />
    <Scene :background="0xffffff">
      <AmbientLight :position="{ y: 0, z: 50 }" :intensity="1.5"/>

      <Text
          text="HAI4 ORD"
          font-src="/assets/UKNumberPlate_Regular.json"
          align="center"
          :size="1.5"
          :height=".1"
          :position="{ x: 0, y: 0, z: .08 }"
      >
        <BasicMaterial color="#000000"/>
      </Text>

      <GltfModel
          src="/assets/halford_standard.gltf"
          @load="onReady"
          @progress="onProgress"
          @error="onError"
      />

    </Scene>
  </Renderer>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { Box, Camera, LambertMaterial, PointLight, AmbientLight, Renderer, Scene } from 'troisjs'
import {Text} from 'troisjs'
const rendererC = ref()
//const meshC = ref()
onMounted(() => {
  const renderer = rendererC.value
  //const mesh = meshC.value.mesh
  renderer.onBeforeRender(() => {
    //mesh.rotation.x += 0.01
  })
})

// Set properties to configure:

</script>



<style>
body {
  margin: 0;
}
canvas {
  display: block;
}
</style>
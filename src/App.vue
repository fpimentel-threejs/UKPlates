<script setup>
import { ref, onMounted } from 'vue'
import { Camera, AmbientLight, Renderer, Scene } from 'troisjs'
import { Text } from 'troisjs'

const plateNum = ref('default')
const plateType = 'A';

const rendererC = ref()
//const meshC = ref()
onMounted(() => {

  const renderer = rendererC.value
  //const mesh = meshC.value.mesh
  renderer.onBeforeRender(() => {
    //console.log(this.$refs.licenseNum);
    //mesh.rotation.x += 0.01
  })
})
</script>

<template>
  <Renderer ref="rendererC" antialias :orbit-ctrl="{ enableDamping: true }" resize="window">
    <Camera :position="{ z: 10 }" />
    <Scene :background="0xffffff">
      <AmbientLight :position="{ y: 0, z: 50 }" :intensity="1.5"/>

      <h1>Enter your license plate number:</h1>

      <input autofocus placeholder='plate number' v-model="plateNum" maxlength="8">

      <!--<div>Selected: {{ plateType }}</div>

      <select v-model="plateType">
        <option disabled value="">Please select one</option>
        <option>A</option>
        <option>B</option>
        <option>C</option>
      </select>-->

      <Text ref = "licenseNum"
          :text = plateNum
          font-src="/assets/UKNumberPlate_Regular.json"
          align="center"
          :size="1.5"
          :height=".1"
          :position="{ x: 0, y: 0, z: .08 }"
      >
        <BasicMaterial color="#000000"/>
      </Text>

      <GltfModel
          src="/assets/hex_halford.gltf"
          @load="onReady"
          @progress="onProgress"
          @error="onError"
      />

    </Scene>
  </Renderer>
</template>

<style>
body {
  margin: 0;
}
canvas {
  display: block;
}

h1{
  position: absolute;
  top: 20px;
  left: 100px;
}

input{
  position: absolute;
  top: 100px;
  left: 100px;
}
</style>
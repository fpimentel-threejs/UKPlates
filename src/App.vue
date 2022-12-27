<script setup>
import { ref, onMounted } from 'vue'
import { Camera, AmbientLight, Renderer, Scene, Circle } from 'troisjs'
import { Text } from 'troisjs'

const plateNum = ref('default')
const plateType = ref('standard')

const plateTypes = {
  standard: ref(true),
  hex: ref(false)
}

const rendererC = ref()
onMounted(() => {

  const renderer = rendererC.value
  renderer.onBeforeRender(() => {
    //mesh.rotation.x += 0.01
  })
})
</script>

<template>
  <Renderer ref="rendererC" antialias :orbit-ctrl="{ enableDamping: true }" resize="window">
    <Camera :position="{ z: 10 }" />
    <Scene :background="0xffffff">
      <AmbientLight :position="{ y: 0, z: 50 }" :intensity="1"/>
      <PointLight :position="{ y: 0, z: 5 }" color="#ffffff" :intensity=".5" />
      <PointLight :position="{ y: 0, z: -5 }" color="#ffffff" :intensity=".5" />

      <h1>Enter your license plate number:</h1>

      <input autofocus placeholder='plate number' v-model="plateNum" maxlength="8">

      <div class = 'plateType'>Selected: {{plateType}} </div>

      <select class = 'plateSelect' v-model="plateType">
        <option disabled value="">Please select one</option>
        <option>standard</option>
        <option>hex</option>
      </select>

      <!--<Circle
          ref="circle"
          :rotation="{ x: (Math.PI /180)*270 }"
          :position="{ y: -2.5}"
          :scale="{x: 100, y: 100}"
      >
        <LambertMaterial color="green" />
      </Circle>-->

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

      <Text
            text = "halfords B98 0DE"
            font-src="/assets/UKNumberPlate_Regular.json"
            align="center"
            :size=".15"
            :height=".01"
            :position="{ x: 0, y: -.95, z: .055 }"
      >
        <BasicMaterial color="#000000"/>
      </Text>

      <div v-if="plateType=='standard'">
        <GltfModel
            src="/assets/standard_halford.gltf"
            @load="onReady"
            @progress="onProgress"
            @error="onError"
            :cashshadow="true"
        />
      </div>

      <div v-if="plateType=='hex'">
      <GltfModel
          src="/assets/hex_halford.gltf"
          @load="onReady"
          @progress="onProgress"
          @error="onError"
          :cashshadow="true"
      />
      </div>

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

.plateType{
  position: absolute;
  top: 400px;
  left: 100px;
}

.plateSelect{
  position: absolute;
  top: 450px;
  left: 100px;
}
</style>
<script setup>
import { ref, onMounted } from 'vue'
import { Camera, AmbientLight, Renderer, Scene } from 'troisjs'
import { Text } from 'troisjs'

const plateNum = ref('defa ult')
let plateNumTop = ref('defa')
let plateNumBottom = ref('ult')
const plateType = ref('standard')
const electricSwitch = ref(false)
const borderSwitch = ref(false)
const motorcycleSwitch = ref(false)

const rendererC = ref()
onMounted(() => {

  const renderer = rendererC.value
  renderer.onBeforeRender(() => {
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

      <select class = 'plateSelect' v-model="plateType">
        <option disabled value="">Please select one</option>
        <option>standard</option>
        <option>hex</option>
        <option>square</option>
        <option>oversized</option>
      </select>

      <div v-if="plateType==='standard'">

        <h1>Enter your license plate number:</h1>

        <input autofocus placeholder='plate number' v-model="plateNum" maxlength="8">

        <div class = 'switchtext'>Is the vehicle electric?</div>

        <input class = "switch" v-model="electricSwitch" type="checkbox" name="check" />

        <div class = 'bordertext'>Add a border?</div>

        <input style="top: 85%" class = "switch" v-model="borderSwitch" type="checkbox" name="check" />

        <div class = 'plateType'>Select your plate type: </div>

        <Text ref = "licenseNum"
              :text = plateNum
              font-src="/assets/UKNumberPlate_Regular.json"
              align="center"
              :size="1.5"
              :height=".2"
              :position="{ x: 0, y: 0, z: .15 }"
        >
          <BasicMaterial color="#000000"/>
        </Text>

        <Text
            text = "UTOPIA PLATES DH1 2XJ"
            font-src="/assets/UKNumberPlate_Regular.json"
            align="center"
            :size=".15"
            :height=".01"
            :position="{ x: 0, y: -.95, z: .06 }"
        >
          <BasicMaterial color="#000000"/>
        </Text>

        <Text
            text = "AR BSAU 145E"
            font-src="/assets/UKNumberPlate_Regular.json"
            align="center"
            :size=".15"
            :height=".01"
            :position="{ x: 4.15, y: -.95, z: .06 }"
        >
          <BasicMaterial color="#000000"/>
        </Text>

        <div v-if="!electricSwitch && !borderSwitch">

        <GltfModel
            src="/assets/standard_plate.gltf"
            @load="onReady"
            @progress="onProgress"
            @error="onError"
        />


        </div>

        <div v-if="!electricSwitch && borderSwitch">

          <GltfModel
              src="/assets/standard_bordered_plate.gltf"
              @load="onReady"
              @progress="onProgress"
              @error="onError"
          />
        </div>

        <div v-if="electricSwitch && borderSwitch">

          <GltfModel
              src="/assets/electric_bordered_plate.gltf"
              @load="onReady"
              @progress="onProgress"
              @error="onError"
          />

        </div>

      <div v-if="electricSwitch && !borderSwitch">

        <GltfModel
            src="/assets/electric_plate.gltf"
            @load="onReady"
            @progress="onProgress"
            @error="onError"
        />
      </div>

      </div>


      <div v-if="plateType==='hex'">

        <h1>Enter your license plate number:</h1>

        <input autofocus placeholder='plate number' v-model="plateNum" maxlength="8">

        <div class = 'plateType'>Select your plate type: </div>

        <Text ref = "licenseNum"
              :text = plateNum
              font-src="/assets/UKNumberPlate_Regular.json"
              align="center"
              :size="1.5"
              :height=".2"
              :position="{ x: 0, y: 0, z: .15 }"
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

        <Text
            text = "AR BSAU 145E"
            font-src="/assets/UKNumberPlate_Regular.json"
            align="center"
            :size=".15"
            :height=".01"
            :position="{ x: 4.15, y: -.95, z: .06 }"
        >
          <BasicMaterial color="#000000"/>
        </Text>

      <GltfModel
          src="/assets/hex_plate.gltf"
          @load="onReady"
          @progress="onProgress"
          @error="onError"
      />
      </div>

      <div v-if="plateType==='square'">

        <h1>Enter your license plate number:</h1>

        <input autofocus placeholder='plate number' v-model="plateNumTop" maxlength="4">

        <input class="bottomtext" autofocus placeholder='plate number' v-model="plateNumBottom" maxlength="4">

        <input class = "switch" v-model="motorcycleSwitch" type="checkbox" name="check" />

        <div class = 'bordertext'>Add a border?</div>

        <input style="top: 85%" class = "switch" v-model="borderSwitch" type="checkbox" name="check" />

        <div class = 'plateType'>Select your plate type: </div>

        <Text ref = "licenseNum"
              :text = plateNumTop
              font-src="/assets/UKNumberPlate_Regular.json"
              align="center"
              :size="1.5"
              :height=".2"
              :position="{ x: 0, y: 1, z: .1 }"
        >

          <BasicMaterial color="#000000"/>

        </Text>

        <Text ref = "licenseNum"
              :text = plateNumBottom
              font-src="/assets/UKNumberPlate_Regular.json"
              align="center"
              :size="1.5"
              :height=".2"
              :position="{ x: 0, y: -.75, z: .1 }"
        >
          <BasicMaterial color="#000000"/>
        </Text>

        <Text
            text = "halfords B98 0DE"
            font-src="/assets/UKNumberPlate_Regular.json"
            align="center"
            :size=".15"
            :height=".01"
            :position="{ x: 0, y: -2.35, z: .055 }"
        >
          <BasicMaterial color="#000000"/>
        </Text>

        <Text
            text = "AR BSAU 145E"
            font-src="/assets/UKNumberPlate_Regular.json"
            align="center"
            :size=".15"
            :height=".01"
            :position="{ x: 2.35, y: -2.35, z: .06 }"
        >
          <BasicMaterial color="#000000"/>
        </Text>

        <div class = 'switchtext'>Is the vehicle a motorcycle?</div>

        <div v-if="!motorcycleSwitch && !borderSwitch">

          <GltfModel
            src="/assets/square_plate.gltf"
            @load="onReady"
            @progress="onProgress"
            @error="onError"
          />
        </div>

        <div v-if="!motorcycleSwitch && borderSwitch">

          <GltfModel
              src="/assets/square_bordered_plate.gltf"
              @load="onReady"
              @progress="onProgress"
              @error="onError"
          />
        </div>

      <div v-if="motorcycleSwitch && !borderSwitch">

        <GltfModel
            src="/assets/motorcycle_plate.gltf"
            @load="onReady"
            @progress="onProgress"
            @error="onError"
        />
      </div>

      <div v-if="motorcycleSwitch && borderSwitch">

        <GltfModel
            src="/assets/motorcycle_bordered_plate.gltf"
            @load="onReady"
            @progress="onProgress"
            @error="onError"
        />
      </div>

      </div>

      <div v-if="plateType==='oversized'">

        <h1>Enter your license plate number:</h1>

        <input autofocus placeholder='plate number' v-model="plateNum" maxlength="8">

        <div class = 'bordertext'>Add a border?</div>

        <input style="top: 85%" class = "switch" v-model="borderSwitch" type="checkbox" name="check" />

        <div class = 'plateType'>Select your plate type: </div>

        <Text ref = "licenseNum"
              :text = plateNum
              font-src="/assets/UKNumberPlate_Regular.json"
              align="center"
              :size="1.5"
              :height=".2"
              :position="{ x: 0, y: 0, z: .15 }"
        >

          <BasicMaterial color="#000000"/>

        </Text>

        <Text
            text = "halfords B98 0DE"
            font-src="/assets/UKNumberPlate_Regular.json"
            align="center"
            :size=".15"
            :height=".01"
            :position="{ x: 0, y: -1.33, z: .055 }"
        >
          <BasicMaterial color="#000000"/>
        </Text>

        <Text
            text = "AR BSAU 145E"
            font-src="/assets/UKNumberPlate_Regular.json"
            align="center"
            :size=".15"
            :height=".01"
            :position="{ x: 4.2, y: -1.33, z: .06 }"
        >
          <BasicMaterial color="#000000"/>

        </Text>

        <div v-if="!borderSwitch">
          <GltfModel
              src="/assets/oversized_plate.gltf"
              @load="onReady"
              @progress="onProgress"
              @error="onError"
          />
        </div>

        <div v-if="borderSwitch">
          <GltfModel
              src="/assets/oversized_bordered_plate.gltf"
              @load="onReady"
              @progress="onProgress"
              @error="onError"
          />
        </div>

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
  top: 5%;
  left: 10%;
}

input{
  position: absolute;
  top: 15%;
  left: 10%;
}

.bottomtext{
  top: 20%;
}

.plateType{
  position: absolute;
  top: 80%;
  left: 20%;
}

.plateSelect{
  position: absolute;
  top: 85%;
  left: 20%;
}

.switch{
  position: absolute;
  left: 55%;
  top: 80%;
}

.switchtext{
  position: absolute;
  left: 60%;
  top: 80%;
}

.bordertext{
  position: absolute;
  left: 60%;
  top: 85%;
}
</style>
<script>
export default {
  props: ['num']
}

import { Text } from 'troisjs'

</script>

<template>
  <Text
        text= "adfs"
        font-src="/assets/UKNumberPlate_Regular.json"
        align="center"
        :size="1.5"
        :height=".1"
        :position="{ x: 0, y: 0, z: .08 }"
  >
    <BasicMaterial color="#000000"/>
  </Text>
</template>
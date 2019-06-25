<template lang="pug">
  div
    Scene
      Box(:position="[0, 0, 5]")
        Material(diffuse="#843",alpha="0.5")
      Ground(:src="background")
    //- Sphere
    //-   Material
    //-     Texture(type="emissive" :src="background")
    p This is the 3D object.
</template>

<script>
import Vue from 'vue'
import vb from 'vue-babylonjs'
import Background from '~/assets/image/background.png'
Vue.use(vb)
export default {
  components: {
  },
  data () {
    return {
      background: Background
    }
  }
}
</script>

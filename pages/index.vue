<template lang="pug">
  div
    Scene
      Box(:position="[0, 0, 5]")
    p This is the 3D object.
</template>

<script>
import Vue from 'vue'
import vb from 'vue-babylonjs'
Vue.use(vb)
export default {
  components: {
  }
}
</script>

<template>
   <canvas id="canvas" ref="canvas"></canvas>
</template>


<script>
import * as BABYLON from 'babylonjs'

export default {
  components: {},
  data() {
    return {
      engine: null,
      canvas: null,
      scene: null,
      light1: null,
      light2: null,
    }
  },
  mounted: function() {
    this.init()
  },
  methods: {
    init: function() {
      const _this = this
      this.canvas = this.$refs.canvas
      this.engine = new BABYLON.Engine(this.canvas, true)
      this.scene = this.createScene()

      this.engine.runRenderLoop(function () {
        _this.scene.render()
      })
      window.addEventListener('resize', function() {
        _this.engine.resize()
      })        
    },
    createScene: function () {
      const scene = new BABYLON.Scene(this.engine)
      const camera = new BABYLON.ArcRotateCamera("Camera", Math.PI / 2, Math.PI / 2, 2, new BABYLON.Vector3(0, 0, 5), this.scene)
      camera.attachControl(this.canvas, true)

      this.light1 = new BABYLON.HemisphericLight("light1", new BABYLON.Vector3(1, 1, 0), this.scene)
      this.light2 = new BABYLON.PointLight("light2", new BABYLON.Vector3(0, 1, -1), this.scene)

      BABYLON.MeshBuilder.CreateSphere("sphere", {diameter:2}, this.scene)
      return scene
    },
  }
}
</script>
<style>
#canvas {
    width: 100%;
    height: 100%;
    touch-action: none;
}
</style>
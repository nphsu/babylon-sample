<template>
   <canvas id="canvas" ref="canvas"></canvas>
</template>


<script>
import * as BABYLON from 'babylonjs'
import SkyImg from '~/assets/image/TropicalSunnyDay'
import SandImg from '~/assets/image/sand.jpg'
import { WaterMaterial } from 'babylonjs-materials';

export default {
  components: {},
  data() {
    return {
      engine: null,
      canvas: null,
      scene: null,
      light1: null,
      light2: null,
      skyImg: SkyImg,
      sandImg: SandImg,
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
      this.createScene()
 
      this.engine.runRenderLoop(function () {
        _this.scene.render()
      })
      window.addEventListener('resize', function() {
        _this.engine.resize()
      })        
    },
    createScene: function () {
      this.scene = new BABYLON.Scene(this.engine)
      // this.scene.usedelayedtextureloading = true
      const camera = new BABYLON.ArcRotateCamera("Camera", Math.PI / 2, Math.PI / 2, 2, new BABYLON.Vector3(0, 2, 5), this.scene)
      camera.attachControl(this.canvas, true)

      this.light1 = new BABYLON.HemisphericLight("light1", new BABYLON.Vector3(1, 1, 0), this.scene)
      this.light2 = new BABYLON.PointLight("light2", new BABYLON.Vector3(0, 1, -1), this.scene)

      BABYLON.MeshBuilder.CreateSphere("sphere", {diameter:2}, this.scene)
      this.createGround()
      // this.createSkybox()
      this.createWater()
    },

    createGround: function () {
      const groundTexture = new BABYLON.Texture(this.sandImg, this.scene)

      const groundMaterial = new BABYLON.StandardMaterial("groundMaterial", this.scene)
      groundMaterial.diffuseTexture = groundTexture

      const ground = BABYLON.Mesh.CreateGround("ground", 512, 512, 32, this.scene)
      ground.material = groundMaterial
    },
    createWater: function () {
      const waterMesh = BABYLON.Mesh.CreateGround("waterMesh", 512, 512, 32, this.scene, false)
      const water = new WaterMaterial("water", this.scene, new BABYLON.Vector2(1024, 1024))
      waterMesh.material = water
    }
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
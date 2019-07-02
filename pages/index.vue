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
      mainCamera: null,
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
      this.scene = new BABYLON.Scene(this.engine)
      this.mainCamera = new BABYLON.ArcRotateCamera(
        "ArcRotateCamera",
        1.5,
        1.3,
        20,
        BABYLON.Vector3.Zero(),
        this.scene
      )
      this.mainLight = new BABYLON.HemisphericLight(
        'light1',
        new BABYLON.Vector3(0,1,0),
        this.scene
      )
      this.engine.runRenderLoop(function () {
        _this.scene.render()
      })
      window.addEventListener('resize', function() {
        _this.engine.resize()
      })

      // const groundTexture = new BABYLON.Texture("assets/image/sand.jpg", this.scene)
      // groundTexture.vScale = groundTexture.uScale = 4.0

      // const groundMaterial = new BABYLON.StandardMaterial("groundMaterial", this.scene)
      // groundMaterial.diffuseTexture = groundMaterial

      // const ground = BABYLON.Mesh.CreateGround("ground", 512, 512, 32, this.scene, false)
      // ground.position.y = -1
      // ground.material = groundMaterial

      const sphereMaterial = new BABYLON.StandardMaterial("sphereMaterial", this.scene);
      // sphereMaterial.diffuseTexture = new BABYLON.Texture("/a.jpg", this.scene);
  
      const sphere = BABYLON.Mesh.CreateSphere("sphere", 16, 10, this.scene);
      sphere.position.y = 20;
      sphere.material = sphereMaterial;
        
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
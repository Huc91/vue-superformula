<template>
  <div
    id="app"
    @mousemove="onMouseMove($event)"
    @click="addShape()"
  >
    <h1>Superformula in Vue.js</h1>
    <h2 class="highlight" >Luca Ucciero</h2>
    <SuperFormula
      :mouseX="xPos"
      :mouseY="yPos"
      :deviceOrientation="deviceOrientation"
      :shapeCount="shapeCount"
    />
  </div>
</template>

<script>
/* eslint-disable */
import SuperFormula from './components/SuperFormula.vue'

export default {
  name: 'app',
  components: {
    SuperFormula
  },
  data(){
    return{
      xPos: 0,
      yPos: 0,
      shapeCount: 1,
      deviceOrientation: {
          hasOrientation: false,
          alpha: null,
          beta: null,
          gamma: null,
      }
    }
  },
  methods: {
    onMouseMove( ev ){

        this.xPos = ev.pageX;
        this.yPos = ev.pageY;

    },
    addShape(){
      this.shapeCount++;
      if (this.shapeCount === 6){
        this.shapeCount = 1;
      }
    },
    getDeviceOrientation(ev){
        this.deviceOrientation["hasOrientation"] = true;
        this.deviceOrientation["alpha"] = ev.alpha;
        this.deviceOrientation["beta"] = ev.beta;
        this.deviceOrientation["gamma"] = ev.gamma;
    }
  },
  mounted(){
      window.addEventListener('deviceorientation', this.getDeviceOrientation);
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=IBM+Plex+Mono:300,700');
html, body {
  background-color: #f5f5f5;
}
html{
  padding: 0px;
  margin: 0px;
}
body{
  margin: 0px;
  padding: 32px;
}
#app {
  font-family: 'IBM Plex Mono', monospace;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #212121;
}
h1{
  margin-top: 0px;
  margin-bottom: 0px;
}
h2{
  margin-top: 16px;
}
.highlight{
  background-color: #fff;
}
</style>

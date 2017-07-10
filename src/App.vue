<template>
  <div id="app">
    <!--<img src="./assets/logo.png">-->
    <!--<router-view></router-view>-->
    <div>x:{{val.x}}</div>
    <div>y:{{val.y}}</div>
    <input type="text" v-drag='position' id="input-drag">
    <div v-drag id="hehe"></div>
  </div>
</template>

<script>
export default {
  name: 'app',
  data(){
    return {
      val: '123'
    }
  },
  methods:{
    position(obj){
      this.val = obj;
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#input-drag{
  position: absolute
}
#hehe{
  height: 100px;
  width: 100px;
  background: red;
  position: absolute;
}
</style>

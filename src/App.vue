<template>
  <div id="app">
    <!--<router-view></router-view>-->
    <input type="text" v-drag id="input-drag">
    <div v-drag id="hehe"></div>
    <draggable></draggable>
  </div>
</template>

<script>
import draggable from './components/draggable.vue'
export default {
  name: 'app',
  components:{
    'draggable':draggable
  },
  data(){
    return {
      val: '123'
    }
  },
  methods:{
    
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

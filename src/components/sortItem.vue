<template>
  <div class="item" 
    draggable="true"
    @dragstart="dragStart($event, index)" 
    @dragover.prevent="dragOver($event, index)"
    @dragenter="dragEnter($event, index)" 
    @dragleave="dragLeave($event, index)" 
    @dragend="dragEnd($event, index)" 
    @drop.stop="drop($event, index)" 
    :key='item'
    :class="{gost: item.isGost}">
      <slot></slot>
  </div>
</template>

<script>
import bus from './bus.js'
export default {
  data(){
    return {

    }
  },
  props:['item', 'index'],
  methods:{
    dragStart(event, index){
      bus.$emit('dragStart', event, index)
    },
    dragOver(event, index){
      bus.$emit('dragOver', event, index)
    },
    dragEnter(event, index){
      bus.$emit('dragEnter', event, index)
      console.log('enter')
    },
    dragLeave(event, index){
      bus.$emit('dragLeave', event, index)
      console.log('leave')
    },
    dragEnd(event, index){
      bus.$emit('dragEnd', event, index)
      console.log('end')
    },
    drop(event, index){
      bus.$emit('drop', event, index)
      console.log('drop')
    }
  },
  created(){

  },
  mounted(){
    
  }
}
</script>

<style scoped>

</style>



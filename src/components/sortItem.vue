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
  props:['item', 'index', 'eventId'],
  methods:{
    dragStart(event, index){
      console.log(this.item)
      bus.$emit('dragStart' + this.eventId, event, index, this.item)
    },
    dragOver(event, index){
      bus.$emit('dragOver' + this.eventId, event, index, this.item)
    },
    dragEnter(event, index){
      bus.$emit('dragEnter' + this.eventId, event, index)
      console.log('enter')
    },
    dragLeave(event, index){
      bus.$emit('dragLeave' + this.eventId, event, index)
      console.log('leave')
    },
    dragEnd(event, index){
      bus.$emit('dragEnd' + this.eventId, event, index)
      console.log('end')
    },
    drop(event, index){
      bus.$emit('drop' + this.eventId, event, index)
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



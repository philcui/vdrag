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
      {{item.name}}
  </div>
</template>

<script>
export default {
  data(){
    return {

    }
  },
  props:['item', 'index'],
  methods:{
    dragStart(event, index){
      this.$emit('onDragStart', event, index)
    },
    dragOver(event, index){
      this.$emit('onDragOver', event, index)
    },
    dragEnter(event, index){
      this.$emit('onDragEnter', event, index)
      console.log('enter')
    },
    dragLeave(event, index){
      this.$emit('onDragLeave', event, index)
      console.log('leave')
    },
    dragEnd(event, index){
      this.$emit('onDragEnd', event, index)
      console.log('end')
    },
    drop(event, index){
      this.$emit('onDrop', event, index)
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



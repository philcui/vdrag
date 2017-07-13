<template>
  <div ref='dragItem' draggable="true"  
     @dragstart="dragStart" 
     @dragover.prevent="dragOver"
     @dragenter="dragEnter" 
     @dragleave="dragLeave" 
     @dragend="dragEnd" 
     @drop.stop="drop"
     :class="{overStyle: isDragOver, draggingStyle: isDragging}">
    <slot></slot>
  </div>
</template>

<script>
export default {
  data(){
    return {
      isDragOver: false,
      isDragging: false
    }
  },
  methods:{
    dragStart(event){
      this.isDragging = true
    },
    dragOver(event){
      this.isDragOver = true;
    },
    dragEnter(event){
      
    },
    dragLeave(event){
      this.isDragOver = false;
    },
    dragEnd(event){
      this.isDragging = false;
      this.isDragOver = false;
    },
    drop(event){
      this.isDragging = false;
      this.isDragOver = false;
      console.log('drop')
    }  
  },
  mounted(){
    
  }
}
</script>

<style scoped>
  .overStyle{
    background-color: yellow;
  }
  .draggingStyle{
    opacity: 0.4;
  }
</style>



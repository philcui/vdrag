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
      event.dataTransfer.effectAllowed = 'move';
      event.dataTransfer.setData('text/html', event.currentTarget.innerHTML)
    },
    dragOver(event){
      this.isDragOver = true;
    },
    dragEnter(event){
      console.log('enter')
    },
    dragLeave(event){
      this.isDragOver = false;
      console.log('leave')
    },
    dragEnd(event){
      this.isDragging = false;
      this.isDragOver = false;
      console.log('end')
    },
    drop(event){
      this.isDragging = false;
      this.isDragOver = false;
      event.currentTarget.innerHTML = event.dataTransfer.getData('text/html');
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



<template>
  <div class="item" 
    draggable="true"
    @dragstart="dragStart($event, index)" 
    @dragover.prevent="dragOver($event, index)"
    @dragenter="dragEnter" 
    @dragleave="dragLeave" 
    @dragend="dragEnd" 
    @drop.stop="drop" 
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
    dragEnter(event){
      this.$emit('onDragEnter', event, index)
      console.log('enter')
    },
    dragLeave(event){
      this.$emit('onDragLeave', event, index)
      console.log('leave')
    },
    dragEnd(event){
      this.$emit('onDragEnd', event, index)
      console.log('end')
    },
    drop(event){
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



<template>
  <div 
    @onDragStart='dragStart'
    @onDragOver='dragStart'
    @onDragEnter='dragEnter'
    @onDragLeave='dragLeave'
    @onDrop='drop'>
    <transition-group name="flip-list">
      <slot></slot>
    </transition-group>
  </div>
</template>

<script>
import {draggable} from '../core/draggable.js'
export default {
  data(){
    return {
      dragElement: null,
      isChanging: false,
      dragIndex: null,
      targetIndex: null
    }
  },
  props:['sortList'],
  methods:{
    dragStart(event, index){
      event.dataTransfer.effectAllowed = 'move';
      event.dataTransfer.setData('Text', event.currentTarget.innerHTML)
      this.dragElement = event.currentTarget
      this.dragIndex = index
    },
    dragOver(event, index){
      if(event.currentTarget != this.dragElement && !this.isChanging){
        console.log("gost")
        this.targetIndex = index
        event.dataTransfer.dropEffect = 'move';
        this.change();
      }
    },
    dragEnter(event){
      console.log('enter')
    },
    dragLeave(event){
      console.log('leave')
    },
    dragEnd(event){
      this.sortList.forEach((item, index, arr) => {
        item.isGost = false;  
      });
      console.log('end')
    },
    drop(event){
      console.log('drop')
    },
    change(){
      var dragIndex = this.dragIndex;
      var targetIndex = this.targetIndex;
      this.isChanging = true
      var tmp = this.sortList[dragIndex]
      this.sortList.splice(dragIndex, 1, this.sortList[targetIndex])
      this.sortList.splice(targetIndex, 1 , tmp)
      //todo: mybe use nextTick & animation trigger
      setTimeout(() => this.isChanging = false, 500);
      this.dragIndex = targetIndex
      this.$set(this.sortList[targetIndex], 'isGost', true)
      this.$emit('sort', this.sortList);
    },
    del(){
      this.sortList.pop();
    } 
  },
  created(){

  },
  mounted(){
    
  }
}
</script>

<style scoped>
  .item{
    border: 1px solid #333;
    margin-bottom: 10px;
    border-radius: 5px;
    height: 50px;
    text-align: center;
    line-height: 50px;
    -webkit-user-drag: element;
    -khtml-user-drag: element;
    background: #ccc;
     transition: all 0.3s;  
  }
  .flip-list-move{
    transition: transform 0.3s;
  }
  .gost{
     opacity: 0.4;
  } 
</style>


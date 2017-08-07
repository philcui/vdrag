<template>
  <div ref="haha">
    <transition-group name="flip-list">
      <slot></slot>
    </transition-group>
  </div>
</template>

<script>
/*
  解耦sortItem与sortable的几种方案
  1.new vue 后使用on&emit进行发布与订阅，但是所有的sortable共用了一个bus，导致无法
  区分是哪个组件需要接收消息，或者可以通过创建sortable时，指定一个id，使订阅事件唯一；
  2.将sortItem作为属性传入sortable,内部通过render渲染，不存在事件通知问题；
  3.创建drag类，每个sortable拥有一个drag实例，事件挂接在ref上，在实例中处理。
 */
import {draggable} from '../core/draggable.js'
import bus from './bus.js'
export default {
  model:{
    prop: 'sortList',
    event:'change'
  },
  data(){
    return {
      dragElement: null,
      isChanging: false,
      dragIndex: null,
      targetIndex: null
    }
  },
  props:['sortList', 'eventId'],
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
        //item.isGost = false;
        this.$set(item, 'isGost', false)  
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
      //todo: maybe use nextTick & animation trigger
      setTimeout(() => this.isChanging = false, 500);
      this.dragIndex = targetIndex
      this.$set(this.sortList[targetIndex], 'isGost', true)
      this.$emit('sort', this.sortList);
    }
  },
  created(){

  },
  mounted(){
    bus.$on('dragStart'+ this.eventId, (event, index) => this.dragStart(event, index));
    bus.$on('dragOver'+ this.eventId, (event, index) => this.dragOver(event, index));
    bus.$on('dragEnter'+ this.eventId, (event) => this.dragEnter(event));
    bus.$on('dragLeave'+ this.eventId, (event) => this.dragLeave(event));
    bus.$on('dragEnd'+ this.eventId, (event) => this.dragEnd(event));
    bus.$on('drop'+ this.eventId, (event) => this.drop(event));
  }
}
</script>

<style>
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


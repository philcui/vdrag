<!--<template>
  <div>
    <slot></slot>
  </div>
</template>-->

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
      index = this.getIndex(event.target, event.target.parentNode.childNodes);
      event.dataTransfer.effectAllowed = 'move';
      event.dataTransfer.setData('Text', event.currentTarget.innerHTML)
      this.dragElement = event.target
      this.dragIndex = index
    },
    dragOver(event, index){
      event.preventDefault()
      if(event.target != this.dragElement && this.isDragElement(event.target) && !this.isChanging){
        event.dataTransfer.dropEffect = 'move';
        this.targetIndex = this.getIndex(event.target, event.target.parentNode.childNodes);
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
        this.$set(item, 'isGost', false)  
      });
      console.log('end')
    },
    drop(event){
      event.stopPropagation();
      console.log('drop')
    },
    change(){
      var dragIndex = this.dragIndex;
      var targetIndex = this.targetIndex;
      this.isChanging = true
      console.log("dragindex:"+ dragIndex)
      console.log("targetindex:"+ targetIndex)
      var tmp = this.sortList[dragIndex]
      this.sortList.splice(dragIndex, 1, this.sortList[targetIndex])
      this.sortList.splice(targetIndex, 1 , tmp)
      //todo: maybe use nextTick & animation trigger
      setTimeout(() => this.isChanging = false, 500);
      this.dragIndex = targetIndex
      this.$set(this.sortList[targetIndex], 'isGost', true)
      this.$emit('sort', this.sortList);
    },
    getIndex(item, list){
      return [].indexOf.call(list, item)
    },
    isDragElement(el){
      return el.hasAttribute('draggable')
    }
  },
  created(){
    
  },
  mounted(){
    // var children = this.$el.children[0].children;
    // children = [].slice.call(children)
    // children.forEach((item, index, arr) => {
    //   item.addEventListener('dragstart', (event) => {
    //     this.dragStart(event, index)
    //   })
    //   item.addEventListener('dragover', (event) => {
    //     this.dragOver(event, index)
    //   })
    //   item.addEventListener('dragend', () => {
    //     this.dragEnd(event, index)
    //   })
    //   item.addEventListener('drop', () => {
    //     this.drop(event, index)
    //   })
    // })
  },
  render(h){
    var that = this;
    return h('div',{
      on:{
        dragstart:function(event){
          that.dragStart(event)
        },
        dragover: function(event){
          that.dragOver(event)
        },
        drop: function(event){
          that.drop(event)
        },
        dragend : function(event){
          that.dragEnd(event)
        }
      }
    }, this.$slots.default)
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
     /* transition: all 0.3s;   */
  }
  .flip-list-move{
    transition: transform 0.3s;
  }
  .gost{
     opacity: 0.4;
  } 
</style>


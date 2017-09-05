<template>
  <div id="app">
    <!--<router-view></router-view>-->
    <!-- <input type="text" v-drag id="input-drag" value="拖拽指令实现"> -->
    <!-- <div v-drag id="hehe">拖拽指令实现</div> -->
     <!-- <div class="list">
      <draggable class="dragItem" v-for="dragItem in dragList" :key="dragItem">
        <div>{{dragItem.name}}</div>
      </draggable>
    </div>  -->
    
    <Sortable v-model='dragList' :eventId='eventId1'>
      <transition-group name="flip-list">
        <div class="item" draggable="true" v-for="(item, index) in dragList" :key="item">{{item.name}}</div>    
      </transition-group>
    </Sortable>

    <!-- <Sortable v-model='dragList2' :eventId='eventId2'>
      <div v-for="(item, index) in dragList2" :key="index">{{item.name}}</div>      
    </Sortable> -->
  </div>
</template>

<script>
import draggable from './components/draggable.vue'
import Sortable from './components/sortable.vue'
import SortItem from './components/sortItem.vue'
import SortList from './components/sortList.vue'
import SlotTest from './components/slotTest.vue'
export default {
  name: 'app',
  components:{
    'draggable':draggable,
    'Sortable': Sortable,
    'SortItem': SortItem,
    'SortList': SortList,
    'SlotTest': SlotTest
  },
  data(){
    return {
      dragList:[
        {name: 'cui', isGost: false},
        {name: 'xi', isGost: false},
        {name: 'hang', isGost: false}
      ],
      dragList2: [
        {name: '1', isGost: false},
        {name: '2', isGost: false},
        {name: '3', isGost: false}
      ],
      eventId1: '123',
      eventId2: '234'
    }
  },
  methods:{
    
  },
  created(){

  },
  mounted(){
   
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
.dragItem{
  width: 100px;
  height: 100px;
  background-color: #0dbc79;
  border: 1px solid #000;
  text-align: center;
  line-height: 100px;
  border-radius: 10px;
  color: white;
  user-select: none;
  float: left;
  -webkit-user-drag: element;
  -khtml-user-drag: element;
  transition: all 1s ease;
}
.list{
  overflow: hidden;
  margin-top: 100px;
}
#eh{
  width: 0;
  height: 0;
}
.flip-list-move {
  transition: transform 1s;
}
</style>

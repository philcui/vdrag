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
    <sortlist @sort='listChange' :sortlist='dragList'>
      <sortItem v-for="(item, index) in dragList" :key="item" :item='item' :index='index'>
      </sortItem>      
    </sortlist>
    <div>{{listJson}}</div>
  </div>
</template>

<script>
import draggable from './components/draggable.vue'
import sortlist from './components/sortable.vue'
import sortItem from './components/sortItem.vue'
export default {
  name: 'app',
  components:{
    'draggable':draggable,
    'sortlist': sortlist,
    'sortItem': sortItem
  },
  data(){
    return {
      dragList:[
        {name: 'cui'},
        {name: 'xi'},
        {name: 'hang'}
      ],
      listJson: this.dragList
    }
  },
  methods:{
    listChange(data){
      this.listJson = data; 
    }
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
</style>

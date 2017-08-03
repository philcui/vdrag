<template>
  <div >
    <slot></slot>
    <div v-for="(item, index) in haha" :key="index">
      {{item}}
    </div>
  </div>
</template>

<script>
export default {
  model:{
    prop:'haha',
    event: 'change'
  },
  data(){
    return {

    }
  },
  props:['haha'],
  methods:{

  },
  created(){

  },
  mounted(){
    
  }
}
</script>

<style scoped>

</style>



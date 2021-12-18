<!-- 商品列表组件 -->
<template>
  <div class="goods">
    <good-list-item v-for="item in goods" :goods-item="item"/>
  </div>
</template>

<script>
  import GoodListItem from './GoodListItem.vue'

  export default {
  name:"GoodList",
  props:{
    goods:{
      type:Array,
      default(){
        return []
      }
    }
  },

  components: {
    GoodListItem
  }

  }
</script>

<style  scoped>
  .goods{
    display: flex;
    flex-wrap: wrap;

    justify-content: space-around;
    padding: 2px;
  }
</style>

<!--  -->
<template>
  <div class="recommend">
    <div v-for="item in recommends" class="recommend-item">
      <a :href="item.link">
        <img :src="item.image" alt="">
        <div>{{ item.title }}</div>
      </a>
    </div>
  </div>
</template>

<script>
 export default {
  name: "RecommendView",
  props: {
    recommends: {
      type: Array,
      default() {
        return []
      }
    }
  }
 }
</script>

<style  scoped>
  .recommend {
    display: flex;
    text-align: center;
    font-size: 15px;
    padding: 10px 0px 15px;
    border-bottom: 10px solid #eee;
  }

  .recommend-item {
    flex: 1;
  }

  .recommend-item img {
    /* 设置图片宽度为25vw，实现图片在均等分展开，用%是不能实现这个功能的！ */
    width: 24vw;
    margin-top: 1px ;
    margin-bottom: 3px;
  }
</style>

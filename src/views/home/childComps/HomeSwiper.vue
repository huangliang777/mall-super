<!-- home页面轮播图封装 -->
<template>
  <swiper>
    <swiper-item v-for="item in banners">
        <a :href="item.link">
          <img :src="item.image" alt="">
        </a>
    </swiper-item>
  </swiper>
</template>

<script>
// 导入轮播图组件
import { Swiper, SwiperItem } from 'components/common/swiper'

 export default {
  name:"HomeSwiper",
  props: {
    banners:{
      type: Array,
      default() {
        return []
      }
    }
  },
  components:{
    Swiper,
    SwiperItem
  }
 }
</script>

<style  scoped>

</style>

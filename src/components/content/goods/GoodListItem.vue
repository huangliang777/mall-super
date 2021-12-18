<!-- 商品列表中每一个具体的商品 -->
<template>
  <div class="goods-item">
    <img :src="goodsItem.show.img" alt="">
    <div class="goods-info">
      <p>{{ goodsItem.title }}</p>
      <span class="price">{{ goodsItem.price }}</span>
      <span class="collect">{{ goodsItem.cfav }}</span>
    </div>
  </div>
</template>

<script>
import GoodListVue from './GoodList.vue'
 export default {
  name:"GoodListItem",
  props:{
    goodsItem:{
      type:Object,
      default() {
        return {}
      }
    }
  }
 }
</script>

<style  scoped>
  .goods-item{
    padding-bottom: 40px;
    position: relative;

    width: 48%;
  }
  .goods-item img{
    width: 100%;
    height: 100%;
    border-radius: 5px;
  }
  .goods-info{
    font-size: 12px;
    /* 定位：子绝父相! */
    position: absolute;
    bottom: 5px;
    left: 0;
    right: 0;
    overflow: hidden;
    text-align: center;
  }
  .goods-info p{
    overflow: hidden;
    white-space: nowrap;
    text-overflow: ellipsis;
    margin-bottom: 3px;
  }
  .goods-info .price{
    color: var(--color-high=text);
    margin-right: 30px;
  }
  .goods-info .collect{
    position: relative;
  }
  /* 下面样式设置的是收藏图标，网上有案例解析 */
  .goods-info .collect::before{
    content: '';
    position: absolute;
    left: -15px;
    top: -1px;
    width: 14px;
    height: 14px;
    background: url("~assets/img/common/collect.svg") rgb(250, 249, 249) 0/14px 14px; 
  }
</style>

<!-- Home组件 -->
<template>
  <div id="home">
    <nav-bar class="home-nav"><div slot="center">购物街</div></nav-bar>
    <home-swiper :banners="banners"/>
    <recommend-view :recommends = "recommends"></recommend-view>
    <feature-view></feature-view>
    <tab-control class="tab-control" 
    :titles="['流行','新款' ,'精选']" 
    @tabClick="tabClick"/>
    <good-list :goods="showGoodIndex"></good-list>
  </div>
</template>

<script>
  // 导入页面上端的导航栏
  import NavBar from 'components/common/navbar/NavBar.vue'

  // 导入封装好的轮播图模块
  import HomeSwiper from './childComps/HomeSwiper'

  // 依次导入轮播图下面组件
  import RecommendView from './childComps/RecommendView'
  import FeatureView from './childComps/FeatureView.vue'
  import TabControl from 'components/content/tabControl/TabControl.vue'
  import GoodList from 'components/content/goods/GoodList.vue'

  // 导入封装好的网络模块
  import { getHomeMultidata, getHomeGoods } from 'network/home'

  export default {
    name:"Home",
    components: {
      NavBar,
      HomeSwiper,
      RecommendView,
      FeatureView,
      TabControl,
      GoodList
    },
    data() {
      return {
        banners: [],
        recommends: [],
        goods: {
          'pop':{page:0, list:[]},
          'new':{page:0, list:[]},
          'sell':{page:0, list:[]},
        },
        currentType: 'pop'
      }
    },
    computed:{
      showGoodIndex(){
        return this.goods[this.currentType].list
      }
    },
    created() {
      // 1.请求多个数据
      this.getHomeMultidata()

      // 请求商品数据
      // getHomeGoods('pop', 1).then(res => {console.log(res)})
      this.getHomeGoods('pop')
      this.getHomeGoods('new')
      this.getHomeGoods('sell')
    },
    methods: {
      // 1.网络请求相关方法
      getHomeMultidata(){
        getHomeMultidata().then(res => {
        // 将请求到的数据res保存到上面的data中(原因：res用完就没了+垃圾回收机制)；
        this.banners = res.data.banner.list;
        this.recommends = res.data.recommend.list;
        // console.log(res);
        })
      },
      getHomeGoods(type){
        const page = this.goods[type].page + 1;
        getHomeGoods(type, page).then(res => {
          // 将对应类型 下一页的数据放到 data 中的 goods中
          this.goods[type].list.push(...res.data.list)})
          // 页码+1
          this.goods[type].page += 1
          // console.log(this.goods[type].list)
      },

      // 2.事件监听相关方法
      tabClick(index){
        switch(index){
          case 0:
            this.currentType = 'pop'
            break
          case 1:
            this.currentType = 'new'
            break
          case 2:
            this.currentType = 'sell'
            break
        }
      }
    }
  }
</script>

<style  scoped>
  #home {
    padding-top: 44px;
  }

  .home-nav {
    color: white;
    font-weight: 700;
    /* 通过调用变量名使用之前定义好的样式 */
    background: var(--color-tint);
  }

  .tab-control {
    background-color: #fff;
    /* 粘性粘贴：实现tab-control移动到距离top 44px时不再向上移动 */
    position: sticky;
    top: 44px;

    /* 不设置这个下面图片会覆盖他 */
    z-index: 10;
  }
</style>

<!--  -->
<template>
  <div class="tab-bar-item" @click="itemClick">
    <!-- 插槽之所以用div包住，是为了使我们定义的语法能够生效（包括判断语句，动态绑定类）；
    不在插槽中定义这些语法的原因是：插槽会直接被对应的代码替换掉，从而导致插槽中定义的方法失效；-->
    <div v-if="!isActive"><slot name="item-icon"></slot></div>
    <div v-else><slot name="item-icon-active"></slot></div>
    <div :style="activeStyle"><slot name="item-text"></slot></div>
  </div>
</template>

<script>
 export default {
  name: "TabBarItem",
  // 插槽传值类似于父组件向子组件传值，所以这里会出现props
  props: {
    path: String,
    activeColor: {
      type: String,
      default: 'red'
    }
  },
  data() {
    return {
      // isActive:false
    }
  },
  computed:{
    // 这个函数实现动态改变item的颜色，通过indexOf()来实现；也就是通过活跃状态的path与每个item的path比较；
    // 相同返回1，不同返回-1；再与-1比较，前者返回ture，后者返回false；为ture时会改变颜色；
    isActive() {
      return this.$route.path.indexOf(this.path) !== -1
    },
    // 这里是动态绑定样式的具体内容，具体的样式上面props中的activeColor，而他的值又来自使用插槽时的赋值，默认为red;
    activeStyle() {
      return this.isActive ? {color: this.activeColor} : {}
    }
  },
  methods:{
    itemClick() {
      this.$router.replace(this.path)
    }
  }
 }
</script>

<style  scoped>
  .tab-bar-item {
    flex: 1;
    text-align: center;
    height: 49px;
    font-size: 14;
  }

  .tab-bar-item img {
    width: 24px;
    height: 24px;
    margin-top: 3px;

    /* 去除每张图片下面的三个像素，默认有三个像素的 */
    vertical-align: middle;
  }
</style>

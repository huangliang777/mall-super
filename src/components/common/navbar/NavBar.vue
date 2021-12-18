<!-- 页面最上端导航栏相关 -->
<template>
  <!-- 最外面的div不设置id,因为该组件可能会在一个应用的多个地方使用；tabbar使用id,是因为只用一次 -->
  <div class="nav-bar">
    <div class="left"><slot name="left"></slot></div>
    <div class="center"><slot name="center"></slot></div>
    <div class="right"><slot name="right"></slot></div>
  </div>
</template>

<script>
  export default {
    name: "NavBar"
  }
</script>

// style中有个scoped，意思是以下样式只能作用于当前组件，通过该属性，实现组件之间样式不互相污染；
<style scoped>
  .nav-bar {
    display: flex;
    line-height: 44px;
    box-shadow: 0 1px 1px rgba(100, 100, 100, .1);
    text-align: center;

    /* 让顶部得导航栏固定在顶部，不随页面一起移动 */
    position: fixed;
    top: 0px;
    left: 0px;
    right: 0px;
    z-index: 10;
  }

  .left, .right {
    width: 60px;
  }

  .center {
    flex: 1;

    /* justify-content: center; */
  }
</style>

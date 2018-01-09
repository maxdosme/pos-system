<template>
  <div id="app">
    <leftNav></leftNav>
    <router-view/>
  </div>
</template>

<script>
// 引入侧边栏组件
import leftNav from '@/components/common/leftNav.vue'
export default {
  name: 'app',
  // 注册组件
  components :{
    leftNav
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
</style>

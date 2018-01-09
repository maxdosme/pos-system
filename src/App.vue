<template>
  <div id="app">
    <img src="./assets/logo.png">
    <i class="icon iconfont icon-hanbao"></i>
    <i class="icon iconfont icon-huiyuanqia"></i>
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'app'
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

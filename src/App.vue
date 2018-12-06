<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>
<style lang="less">
  @import './style/common';
  html{
    background-image: url('assets/img/bg.jpg');
    background-repeat: no-repeat;
    background-size: 100% 100%;
  }
</style>

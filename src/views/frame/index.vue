<template lang="pug">
  el-container
    el-header
      nav-menu
    el-main
      .text-wrap
</template>

<script>
import navMenu from "./nav.vue";

export default {
  name: "home",
  components: { navMenu }
};
</script>
<style lang="stylus" scoped>
.el-container
  height 100%
  .el-header
    padding 0
  .el-main
    height calc(100% - 60px)
    background-image url('../../assets/img/background.jpg')
    background-size 100% 100%
    background-repeat no-repeat
    background-position top center
    .text-wrap
      height 100%
      background-image url('../../assets/img/text.png')
      background-repeat no-repeat
      background-position center 20%
      background-size 75% auto
</style>

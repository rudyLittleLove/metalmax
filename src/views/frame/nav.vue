<template lang="pug">
  el-menu( mode="horizontal" class="metalmax-nav-menu-wrap" background-color="#393D49" text-color="rgba(255, 255, 255, .7)" active-text-color="rgba(255, 255, 255, 1)")
    template( v-for="(item, i) in menus")
      el-submenu( v-if="item.children && item.children.length" :index="item.key" @mouseenter.native="mouseenterHandle" @mouseleave.native="activeDom = ''")
        template(slot="title") {{item.label}}
        el-menu-item( v-for="(item2, i2) in item.children" :index="item2.key" ref="menuItem") {{item2.label}}
      el-menu-item( v-else :index="item.key" @mouseenter.native="mouseenterHandle" @mouseleave.native="activeDom = ''" ref="menuItem") {{item.label}}
    span.line( :style="lineStyle")
</template>

<script>
export default {
  name: "nav-menu",
  data() {
    return {
      activeMenu: "activationCode",
      activeDom: "",
      lineRact: "",
      menus: [
        {
          label: "激活码",
          key: "activationCode",
          children: [
            {
              label: "赞助10元激活码",
              key: "10yuan"
            },
            {
              label: "赞助30元激活码",
              key: "30yuan"
            },
            {
              label: "赞助50元激活码",
              key: "50yuan"
            },
            {
              label: "赞助100元激活码",
              key: "100yuan"
            },
            {
              label: "随机礼包激活码",
              key: "randomFift"
            },
            {
              label: "更换电脑激活码",
              key: "replaceComputer"
            }
          ]
        },
        {
          label: "微信公众号",
          key: "weChatOfficialAccount"
        },
        {
          label: "赞助我们",
          key: "sponsorUs"
        },
        {
          label: "赞助奖励",
          key: "sponsorAward"
        },
        {
          label: "QQ群",
          key: "qqGroup"
        },
        {
          label: "留言板",
          key: "messageBoard"
        }
      ]
    };
  },
  computed: {
    lineStyle() {
      if (this.activeDom) {
        return `left: ${this.lineRact.left}px; width: ${
          this.lineRact.width
        }px; opacity: 1`;
      } else {
        return `left: ${this.lineRact.left +
          this.lineRact.width / 2}px; width: 0; opacity: 0`;
      }
    }
  },
  mounted() {
    this.activeDom = (this.$refs.menuItem[0] || {}).$el;
  },
  methods: {
    mouseenterHandle(e) {
      this.activeDom = e.currentTarget;
      this.lineRact = this.activeDom.getBoundingClientRect();
    }
  }
};
</script>
<style lang="stylus">
.metalmax-nav-menu-wrap.el-menu--horizontal
  position relative
  padding-left 20px
  .el-submenu
    position relative
    .el-submenu__icon-arrow
      content ""
      width 0
      height 0
      border-style solid dashed dashed
      border-color #fff transparent transparent
      overflow hidden
      cursor pointer
      transition all .2s
      position absolute
      top 50%
      right 3px
      margin-top -2px
      border-width 6px
      border-top-color rgba(255,255,255,.7)
  .el-submenu.is-opened
    >.el-submenu__title .el-submenu__icon-arrow
      transform rotate(0deg)
      border-style dashed dashed solid
      margin-top -9px
      border-color transparent transparent #ffffff
  >.el-menu-item.is-active
  >.el-submenu.is-active .el-submenu__title
    border-bottom-width 5px
    border-bottom-color #5FB878!important
  >.el-menu-item
  >.el-submenu
  .el-submenu__title
    background-color transparent!important
    position relative
    z-index 2
  .line
    position absolute
    z-index 1
    left 0
    bottom 0
    width 0px
    height 5px
    background-color #5FB878
    transition all .2s,left .2s
</style>

<template>
  <div>
      <div class="header-abs"  v-show="showAbs" @click="backTo">
      <div class="iconfont header-abs-back">&#xe624;</div></div>
    <div class="header-fixed" v-show="!showAbs" :style="opacityStyle">
       <router-link to="/">
        <div class="iconfont header-fixed-back">&#xe624;</div>
      </router-link>
    景点详情</div>
  </div>
</template>

<script>
export default {
  name: 'DetailHeader',
  data () {
    return {
      showAbs: true,
      opacityStyle: 0
    }
  },
  methods: {
    handleScroll () {
      const top = document.documentElement.scrollTop
      if (top > 60) {
        let opacity = top / 140
        opacity = opacity > 1 ? 1 : opacity
        this.opacityStyle = {
          opacity
        }
        this.showAbs = false
      } else {
        this.showAbs = true
      }
    },
    backTo () {
      this.$router.back(-1)
    }
  },
  // activated () {
  //   window.addEventListener('scroll', this.handleScroll)
  // },
  // deactivated () {
  //   window.removeEventListener('scroll', this.handleScroll)
  // }
  created () {
    window.addEventListener('scroll', this.handleScroll)
  },
  destroyed () {
    window.removeEventListener('scroll', this.handleScroll)
  }
}
</script>

<style lang="stylus" scoped>
@import '~style/varibles.styl'
.header-abs
  position absolute
  left .2rem
  top .2rem
  width .8rem
  line-height .8rem
  height .8rem
  border-radius .4rem
  background rgba(0,0,0,.8)
  text-align center
  .header-abs-back
    color #ffffff
    font-size .4rem
.header-fixed
  position fixed
  top 0
  z-index 1
  left 0
  right 0
  height .86rem
  line-height .86rem
  text-align center
  color #fff
  background $bgClolor
  font-size .32rem
  .header-fixed-back
    position absolute
    top 0
    left 0
    width .64rem
    text-align center
    font-size .4rem
    color #fff
</style>

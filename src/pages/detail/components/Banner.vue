<template>
  <div>
    <div class="banner" @click="handleBannerClick">
      <img v-if="bannerImg" class="banner-img" :src="require(`@/assets/image/${bannerImg}`)">
      <div class="banner-info">
        <div class="banner-title">{{sightName}}</div>
        <div class="banner-number">
          <span class="iconfont banner-icon">&#xe692;</span>
          {{gallaryImgs.length}}
        </div>
      </div>
    </div>
    <FadeAnimation>
      <CommonGallary
        :gallaryImgs="gallaryImgs"
        v-show="showGallary"
        @close="handleGallaryClose"
      />
    </FadeAnimation>
  </div>
</template>

<script lang="ts">
import { Component, Vue, Prop } from 'vue-property-decorator'
import CommonGallary from 'common/gallary/Gallary.vue'
import FadeAnimation from 'common/fade/FadeAnimation.vue'
import { SightName, BannerImg, GallaryImgs } from '@/types'

@Component({
  components: {
    CommonGallary,
    FadeAnimation
  }
})
export default class Banner extends Vue {
  @Prop() sightName!: SightName
  @Prop() bannerImg!: BannerImg
  @Prop() gallaryImgs!: Array<GallaryImgs>
  private showGallary: Boolean = false

  handleBannerClick () {
    this.showGallary = true
  }

  handleGallaryClose () {
    this.showGallary = false
  }
}
</script>

<style lang="stylus" scoped>
  .banner
    position relative
    overflow hidden
    height 0
    padding-bottom 62.7%
    .banner-img
      width 100%
    .banner-info
      display flex
      position absolute
      left 0
      right 0
      bottom 0
      line-height .6rem
      color #fff
      background-image linear-gradient(to bottom, rgba(0, 0, 0, 0), rgba(0, 0, 0, .8))
      .banner-title
        flex 1
        font-size .32rem
        padding 0 .2rem
      .banner-number
        padding 0 .4rem
        height .32rem
        margin-top .14rem
        line-height .32rem
        border-radius .2rem
        background rgba(0, 0, 0, .8)
        font-size .24rem
        .banner-icon
          font-size .24rem
</style>

<template>
  <swiper ref="homeSwiper">
    <swiper-item v-for="(item, id) in banners" :key="id">
      <a :href="item.link">
        <img :src="item.image" alt="" @load="imageLoad">
      </a>
    </swiper-item>
  </swiper>
</template>

<script>
  import {Swiper, SwiperItem} from 'components/common/swiper'

  export default {
    name: "HomeSwiper",
    props: {
      banners: {
        type: Array,
        default() {
          return []
        }
      }
    },
    data() {
      return {
        isLoad:false,
        loadImgCount : 0
      }
    },
    components: {
      Swiper,
      SwiperItem
    },
    methods: {
      imageLoad() {
        if(!this.isLoad) {
          this.$emit('swiperImageLoad')
          this.isLoad = true
        }
        if(++this.loadImgCount == this.banners.length) {
          this.loadImgCount -= this.banners.length
          this.$refs.homeSwiper.handleDom()
          this.$refs.homeSwiper.startTimer()
        }
      }
    }
  }
</script>

<style scoped>

</style>

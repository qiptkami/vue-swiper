<template>
  <div class="swiper-container" ref="swiperContainer" v-if="infData.length > 0">
    <div class="swiper-wrapper">
      <div class="swiper-slide" v-for="(item, index) in infData" :key="item.id">
        <slot :item="item" :index="index"></slot>
      </div>
    </div>
    <div ref="swiperButtonPrev" class="swiper-button-prev"></div>
    <div ref="swiperButtonNext" class="swiper-button-next"></div>
  </div>
</template>
<script>
export default {
  props: {
    viewCount: { type: Number, default: 5 }, //一次显示多少张
    slidesPerGroup: { type: Number, default: 1 }, //每次滚动多少张
    autoplay: { type: Boolean, default: false }, //自动播放
    interval: { type: Number, default: 4000 }, //自动播放间隔时长（ms）
    direction: { type: String, default: "left" }, //自动播放滚动方向
    data: [],
    clickId: { type: Number, default: 0 },
  },
  data() {
    return {
      infData: [],
      mySwiper: null,
    };
  },
  created() {
    this.infData = this.data;
  },
  mounted() {
    this.initSwiper();
  },
  methods: {
    initSwiper() {
      this.mySwiper = new window.Swiper(this.$refs.swiperContainer, {
        slidesPerView: "auto",
        slidesPerGroup: this.slidesPerGroup,
        autoplay: this.autoplay,
        delay: this.interval,
        reverseDirection: this.direction === "right",
        spaceBetween: -8,
        navigation: {
          nextEl: ".swiper-button-next",
          prevEl: ".swiper-button-prev",
        },
        initialSlide: this.clickId,
        on: {
          resize: function () {
            this.update(); //窗口变化时，更新Swiper的一些属性，如宽高等
          },
        },
      });
      if (this.viewCount > this.infData.length) {
        const prev = this.$refs.swiperButtonPrev;
        const next = this.$refs.swiperButtonNext;
        prev.parentNode.removeChild(prev);
        next.parentNode.removeChild(next);
      }
    },
  },
};
</script>

<style lang="less" scoped>
.swiper-container {
  width: 100%;
  height: 100%;

  .swiper-slide {
    width: auto;
    height: auto;
  }
  .swiper-button-prev {
    background-image: url("../assets/Vector.png");
    height: 40px;
    width: 40px;
    left: 20px;
    &::after {
      color: #fff;
      font-size: 20px;
    }
  }
  .swiper-button-next {
    background-image: url("../assets/Vector.png");
    height: 40px;
    width: 40px;
    right: 20px;
    &::after {
      color: #fff;
      font-size: 20px;
    }
  }
}
</style>
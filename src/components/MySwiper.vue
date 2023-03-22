<template>
  <div>
    <div class="pagination-container" v-if="pagination">
      <div v-show="!isFirstPage" class="page-prev" @click="toLeft">
        <a-icon type="left" />
      </div>
      <div
        class="swiper-pagination swiper-pagination-clickable swiper-pagination-bullets"
        id="pagination"
      ></div>
      <div v-show="!isLastPage" class="page-next" @click="toRight">
        <a-icon type="right" />
      </div>
    </div>
    <div
      class="swiper-container"
      ref="swiperContainer"
      v-if="infData.length > 0"
    >
      <div class="swiper-wrapper">
        <div
          class="swiper-slide"
          v-for="(item, index) in infData"
          :key="item.id"
        >
          <slot :item="item" :index="index"></slot>
        </div>
      </div>
      <div ref="swiperButtonPrev" class="swiper-button-prev"></div>
      <div ref="swiperButtonNext" class="swiper-button-next"></div>
    </div>
  </div>
</template>
<script>
import { Icon } from "ant-design-vue";

export default {
  components: {
    "a-icon": Icon,
  },
  props: {
    slidesPerGroup: { type: Number, default: 1 }, //每次滚动多少张
    autoplay: { type: Boolean, default: false }, //自动播放
    interval: { type: Number, default: 4000 }, //自动播放间隔时长（ms）
    direction: { type: String, default: "left" }, //自动播放滚动方向
    data: [],
    clickId: { type: Number, default: 0 },
    pagination: { type: Boolean, default: false },
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
  computed: {
    isFirstPage() {
      return this.swiperInstance && this.swiperInstance.activeIndex === 0;
    },
    isLastPage() {
      return (
        this.swiperInstance &&
        this.swiperInstance.activeIndex ===
          this.swiperInstance.slides.length - 1
      );
    },
  },
  methods: {
    initSwiper() {
      const vm = this;
      this.mySwiper = new window.Swiper(this.$refs.swiperContainer, {
        slidesPerView: "auto",
        slidesPerGroup: this.slidesPerGroup,
        autoplay: this.autoplay,
        delay: this.interval,
        reverseDirection: this.direction === "right",
        spaceBetween: -16,
        navigation: {
          nextEl: ".swiper-button-next",
          prevEl: ".swiper-button-prev",
        },
        pagination: {
          el: this.pagination && ".swiper-pagination",
          clickable: true,
          renderBullet: function (index, className) {
            return `<span class="${className}" id=${"item" + index} > ${
              vm.data[index].name
            } </span>`;
          },
        },
        initialSlide: this.clickId,
        on: {
          resize: function () {
            this.update(); //窗口变化时，更新Swiper的一些属性，如宽高等
          },
        },
      });
    },
    toLeft() {
      document.getElementById("pagination").scrollLeft -= 80;
    },
    toRight() {
      document.getElementById("pagination").scrollLeft += 80;
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
    text-align: center;
    /* Center slide text vertically */
    display: -webkit-box;
    display: -ms-flexbox;
    display: -webkit-flex;
    display: flex;
    -webkit-box-pack: center;
    -ms-flex-pack: center;
    -webkit-justify-content: center;
    justify-content: center;
    -webkit-box-align: center;
    -ms-flex-align: center;
    -webkit-align-items: center;
    align-items: center;
  }
  .swiper-button {
    width: 40px;
    height: 40px;
    background-color: rgba(0, 0, 0, 0.2);
    border-radius: 50%;
  }
  .swiper-button-prev:after,
  .swiper-button-next:after {
    font-size: 16px;
    color: #fff;
  }
  .my-button-disabled {
    display: none;
  }
  // .swiper-button-next {
  //   background-image: url("../assets/Vector.png");
  //   height: 40px;
  //   width: 40px;
  //   right: 20px;
  //   &::after {
  //     color: #fff;
  //     font-size: 20px;
  //   }
  // }
}
.pagination-container {
  display: flex;
  justify-content: center;
  align-items: center;
  .page-prev {
    cursor: pointer;
    z-index: 99;
    font-size: 18px;
    margin-right: -20px;
  }
  .page-next {
    cursor: pointer;
    z-index: 99;
    font-size: 18px;
    margin-left: -20px;
  }
  .swiper-pagination {
    display: flex;
    border-radius: 24px;
    height: 39px;
    width: auto;
    max-width: 100%;
    background: #f0f0f4;
    overflow: hidden;
    position: inherit;
    /deep/ .swiper-pagination-bullet {
      display: inline-block;
      width: auto;
      height: 100%;
      border: none;
      padding: 8px 40px;
      margin: 0;
      color: #262626;
      background: #f0f0f4;
      user-select: none;
      font-weight: 500;
      font-size: 16px;
      line-height: 20px;
      white-space: nowrap;
    }
    /deep/ .swiper-pagination-bullet-active {
      display: inline-block;
      color: #329966;
      background: #ffffff;
      border: 1px solid #329966;
      border-radius: 24px;
    }
  }
}
</style>
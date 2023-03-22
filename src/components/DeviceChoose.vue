<template>
  <div>
    <my-swiper
      v-slot="slotProps"
      :viewCount="5"
      :slidesPerGroup="1"
      :data="data"
    >
      <div class="control-container" @click.stop="handleClickInfo(slotProps)">
        <div class="control-content">
          <div v-show="slotProps.item.recommend" class="triangle">
            <div class="triangle-white">
              <div class="triangle-content">
                <a-icon type="star" theme="filled" /> 最佳
              </div>
            </div>
          </div>
          <div class="control-content-header">{{ slotProps.item.name }}</div>
          <slot :item="slotProps.item" name="desc">
            <div class="control-content-desc">{{ slotProps.item.desc }}</div>
          </slot>
          <img class="control-img" src="@/assets/card.png" />
          <div class="box-hover">进一步了解</div>
          <a-radio
            :key="slotProps.item.id"
            :checked="localSelectId == slotProps.item.id"
            @click="handleClickOption($event, slotProps)"
          >
          </a-radio>
        </div>
      </div>
    </my-swiper>
    <modal-info
      :visible="isModalOpen"
      :width="960"
      title="主控详情"
      :onOk="handleOk"
      :onCancel="handleCancel"
      :data="data"
    >
      <my-swiper
        v-slot="slotProps"
        :viewCount="1"
        :slidesPerGroup="1"
        :data="data"
        :clickId="clickId"
        :pagination="true"
      >
        <div class="modal-info-container">
          <div class="modal-info-left">
            <img class="modal-info-img" src="@/assets/card.png" />
            <a-radio
              :key="slotProps.item.id"
              :checked="localSelectId == slotProps.item.id"
              @click="localSelectId = slotProps.item.id"
            >
              {{ localSelectId == slotProps.item.id ? "已选" : "可选"
              }}{{ slotProps.item.name }}
            </a-radio>
          </div>
          <div class="modal-detail">{{ slotProps.item.detail }}</div>
        </div>
      </my-swiper>
    </modal-info>
  </div>
</template>
<script>
import MySwiper from "./MySwiper.vue";
import ModalInfo from "./ModalInfo.vue";

import { Icon, Radio } from "ant-design-vue";
export default {
  components: {
    MySwiper,
    ModalInfo,
    "a-radio": Radio,
    "a-icon": Icon,
  },
  props: {
    data: [],
    title: { type: String },
    selectId: { type: [Number, String], default: -1 },
    maskClosable: {
      type: Boolean,
      default: false,
    },
    destroyOnClose: {
      type: Boolean,
      default: true,
    },
    isRadio: {
      type: Boolean,
      default: true,
    },
  },
  data() {
    return {
      isModalOpen: false,
      clickId: -1,
      localSelectId: this.selectId,
    };
  },
  methods: {
    handleClickOption(event, slotProps) {
      event.stopPropagation();
      this.localSelectId = slotProps.item.id;
      this.$emit("update:selectId", this.localSelectId);
    },
    handleClickInfo(slotProps) {
      this.isModalOpen = true;
      this.clickId = slotProps.index;
    },
    handleOk() {
      this.isModalOpen = false;
    },
    handleCancel() {
      this.isModalOpen = false;
    },
  },
};
</script>

<style lang="less" scoped>
.control-container {
  width: 220px;
  height: 220px;
  background: #fff;
  box-shadow: 3.6px 5.4px 10.8px rgba(0, 0, 0, 0.08);
  border-radius: 7.2px;
  margin: 16px;
  cursor: pointer;
  transform: scale(1);
  &:hover {
    transition: all 0.3s;
    transform: scale(1.05);
  }
  .control-content {
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: space-evenly;
    flex-direction: column;
    align-items: center;
    padding: 16px;
    .triangle {
      position: absolute;
      width: 0;
      height: 0;
      left: 0;
      top: 0;
      border-width: 35px;
      border-style: solid;
      border-color: #ff9d2b transparent transparent #ff9d2b;
      .triangle-white {
        position: absolute;
        left: -35px;
        top: -35px;
        width: 0;
        height: 0;
        border-width: 15px;
        border-style: solid;
        border-color: #fff transparent transparent #fff;
        .triangle-content {
          position: absolute;
          left: -6px;
          top: 0;
          height: 20px;
          width: 40px;
          font-size: 12px;
          transform: rotate(315deg);
          color: #fff;
        }
      }
    }
    .control-content-header {
      font-size: 14px;
      font-weight: 500;
      line-height: 19.6px;
      color: #262626;
    }
    .control-content-desc {
      font-size: 13px;
      font-weight: 400;
      line-height: 18.2px;
      color: #606266;
      padding: 8px 0 20px 0;
    }
    .control-img {
      width: 118px;
      height: 84px;
      padding-bottom: 17px;
    }
    &:hover {
      .box-hover {
        opacity: 1;
      }
    }

    .box-hover {
      opacity: 0;
      position: absolute;
      border-radius: 22px;
      top: 150px;
      padding: 6px 10px;
      color: #262626;
      font-size: 14px;
      font-weight: 400;
      line-height: 19.6px;
      width: 100px;
      height: 32px;
      cursor: pointer;
      background: #f0f0f4;
    }
    .control-radio {
      padding-bottom: 0;
      width: 21px;
      height: 21px;
    }
  }
}

.page-prev {
  content: "<";
  position: absolute;
  margin-top: 7px;
  height: 50px;
  left: 50px;
  width: 50px;
}
.page-next {
  content: ">";
  position: absolute;
  height: 50px;
  width: 50px;
  right: 10px;
  margin-top: 7px;
}
.modal-info-container {
  display: flex;
  height: auto;
  width: 912px;
  padding: 0 64px;
  display: flex;
  .modal-info-left {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-right: 32px;
    .modal-info-img {
      margin-bottom: 30px;
      width: 300px;
      height: 200px;
    }
    .modal-detail {
      font-weight: 400;
      font-size: 14px;
      line-height: 22px;
    }
  }
}
.box-hidden {
  display: none;
}
</style>

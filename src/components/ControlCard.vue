<template>
  <div>
    <my-swiper
      v-slot="slotProps"
      :viewCount="5"
      :slidesPerGroup="1"
      :data="infData"
    >
      <div
        class="control-container"
        @click.stop="handleClickInfo(slotProps)"
        @mouseover="handleHover(slotProps)"
        @mouseout="isHover = false"
      >
        <div class="control-content">
          <div class="triangle">
            <div class="triangle-white">
              <div class="triangle-content">
                <a-icon type="star" theme="filled" /> 最佳
              </div>
            </div>
          </div>
          <div class="control-content-header">{{ slotProps.item.name }}</div>
          <div class="control-content-desc">{{ slotProps.item.desc }}</div>
          <div class="control-img"></div>
          <div
            class="box-hover"
            :class="{
              'box-hidden': !(isHover && hoverId === slotProps.item.id),
            }"
          >
            进一步了解
          </div>
          <a-radio
            class="control-radio"
            :key="slotProps.item.id"
            :checked="selectId == slotProps.item.id"
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
    >
      <my-swiper
        v-slot="slotProps"
        :viewCount="1"
        :slidesPerGroup="1"
        :data="infData"
        :clickId="clickId"
      >
        <div class="modal-info-container">
          <div class="modal-info-left">
            <div class="modal-info-img"></div>
            <a-radio
              :key="slotProps.item.id"
              :checked="selectId == slotProps.item.id"
              @click="handleClickOption($event, slotProps)"
            >
              {{ selectId == slotProps.item.id ? "已选" : "可选"
              }}{{ slotProps.item.name }}
            </a-radio>
          </div>
          <div class="modal-desc">{{ slotProps.item.desc }}</div>
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
  data() {
    return {
      infData: [],
      selectId: 0,
      clickId: 0,
      isModalOpen: false,
      isHover: false,
      hoverId: 0,
    };
  },
  created() {
    this.infData = [
      { id: "1", name: "1-DH7512", desc: "强劲性能，无惧考验" },
      { id: "2", name: "2-DH3208", desc: "强劲性能，无惧考验" },
      { id: "3", name: "3-DH7508", desc: "强劲性能，无惧考验" },
      { id: "4", name: "DH426/HDH756", desc: "强劲性能，无惧考验" },
      { id: "5", name: "5-MRV328", desc: "匠心打造，为效率而生" },
      { id: "6", name: "6-DH75122", desc: "强劲性能，无惧考验" },
      { id: "7", name: "7-DH75123", desc: "强劲性能，无惧考验" },
      { id: "8", name: "8-DH75124", desc: "强劲性能，无惧考验" },
      { id: "9", name: "9-DH75125", desc: "强劲性能，无惧考验" },
      { id: "10", name: "last-DH75125", desc: "强劲性能，无惧考验" },
    ];
  },
  methods: {
    handleClickOption(event, slotProps) {
      event.stopPropagation();
      this.selectId = slotProps.item.id;
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
    handleHover(slotProps) {
      this.hoverId = slotProps.item.id;
      this.isHover = true;
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

  .control-content {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 16px;
    overflow: hidden;
    .triangle {
      margin: 16px;
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
      background: red;
    }
    .box-hidden {
      display: none;
    }
    .box-hover {
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
      padding-top: 18px;
      width: 21px;
      height: 21px;
    }
  }
}

.modal-info-container {
  display: flex;
  align-items: center;
  height: 100%;
  width: 100%;
  margin: 40px 80px;
  .modal-info-left {
    margin-right: 90px;
    .modal-info-img {
      width: 300px;
      height: 200px;
      background: #f0f0f4;
    }
  }
}
</style>

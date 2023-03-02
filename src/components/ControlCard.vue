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
          <div
            class="triangle"
            :class="{
              'box-hidden': !slotProps.item.recommend,
            }"
          >
            <div class="triangle-white">
              <div class="triangle-content">
                <a-icon type="star" theme="filled" /> 最佳
              </div>
            </div>
          </div>
          <div class="control-content-header">{{ slotProps.item.name }}</div>
          <div class="control-content-desc">{{ slotProps.item.desc }}</div>
          <img class="control-img" src="@/assets/card.png" />
          <div
            class="box-hover"
            :class="{
              'box-hidden': !(isHover && hoverId === slotProps.item.id),
            }"
          >
            进一步了解
          </div>
          <a-radio
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
            <img class="modal-info-img" src="@/assets/card.png" />
            <a-radio
              :key="slotProps.item.id"
              :checked="selectId == slotProps.item.id"
              @click="handleClickOption($event, slotProps)"
            >
              {{ selectId == slotProps.item.id ? "已选" : "可选"
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
      {
        id: "1",
        name: "1-DH7512",
        recommend: 1,
        desc: "强劲性能，无惧考验",
        img: "@/assets/card.png",
        detail:
          "色彩管理  3D功能 将显示色域在不同色域间自由实时地切换，使显 配合支持 3D 功能的发送卡，输出 3D 画面。  RGB 独立 Gamma 调节 示屏的色彩呈现更精准。 配合支持 RGB 独立 Gamma 调节的独立主控和 18bit+ 4 倍提升显示灰阶，有效处理低亮时灰度丢失问 NovaLCT(V5.2.0 及以上版本)，通过对“红 题，使图像显示更细腻。 Gamma”、“绿 Gamma”、“蓝 Gamma”分别进行 调节，有效控制显示屏低灰不均匀、白平衡漂移 逐点亮色度校正 等问题，使画面更加真实。 配合诺瓦高精度校正系统，对每个灯点的亮度和 色度进行校正，有效消除亮度差异和色度差异，  画面90°倍数旋转 使整屏的亮色度达到高度一致。 画面以 90°的倍数(0°/90°/180°/270°)进行 旋转。 快速亮暗线调节 调节模组拼接和箱体拼接造成的亮暗线，改善亮 暗线引起的视觉突兀感。调节过程中即时生效， 简单易用。预存画面设置 NovaLCT 需是 V5.2.0 及以上版本。  固件程序回读 自定义开机、网线断开、无视频源信号时显示屏 回读接收卡的固件程序并保存到本地。 的画面。画面90°倍数旋转 使整屏的亮色度达到高度... ",
      },
      {
        id: "2",
        name: "2-DH3208",
        recommend: 0,
        desc: "强劲性能，无惧考验",
        img: "@/assets/card.png",
        detail:
          "色彩管理  3D功能 将显示色域在不同色域间自由实时地切换，使显 配合支持 3D 功能的发送卡，输出 3D 画面。  RGB 独立 Gamma 调节 示屏的色彩呈现更精准。 配合支持 RGB 独立 Gamma 调节的独立主控和 18bit+ 4 倍提升显示灰阶，有效处理低亮时灰度丢失问 NovaLCT(V5.2.0 及以上版本)，通过对“红 题，使图像显示更细腻。 Gamma”、“绿 Gamma”、“蓝 Gamma”分别进行 调节，有效控制显示屏低灰不均匀、白平衡漂移 逐点亮色度校正 等问题，使画面更加真实。 配合诺瓦高精度校正系统，对每个灯点的亮度和 色度进行校正，有效消除亮度差异和色度差异，  画面90°倍数旋转 使整屏的亮色度达到高度一致。 画面以 90°的倍数(0°/90°/180°/270°)进行 旋转。 快速亮暗线调节 调节模组拼接和箱体拼接造成的亮暗线，改善亮 暗线引起的视觉突兀感。调节过程中即时生效， 简单易用。预存画面设置 NovaLCT 需是 V5.2.0 及以上版本。  固件程序回读 自定义开机、网线断开、无视频源信号时显示屏 回读接收卡的固件程序并保存到本地。 的画面。画面90°倍数旋转 使整屏的亮色度达到高度... ",
      },
      {
        id: "3",
        name: "3-DH7508",
        recommend: 0,
        desc: "强劲性能，无惧考验",
        img: "@/assets/card.png",
        detail:
          "色彩管理  3D功能 将显示色域在不同色域间自由实时地切换，使显 配合支持 3D 功能的发送卡，输出 3D 画面。  RGB 独立 Gamma 调节 示屏的色彩呈现更精准。 配合支持 RGB 独立 Gamma 调节的独立主控和 18bit+ 4 倍提升显示灰阶，有效处理低亮时灰度丢失问 NovaLCT(V5.2.0 及以上版本)，通过对“红 题，使图像显示更细腻。 Gamma”、“绿 Gamma”、“蓝 Gamma”分别进行 调节，有效控制显示屏低灰不均匀、白平衡漂移 逐点亮色度校正 等问题，使画面更加真实。 配合诺瓦高精度校正系统，对每个灯点的亮度和 色度进行校正，有效消除亮度差异和色度差异，  画面90°倍数旋转 使整屏的亮色度达到高度一致。 画面以 90°的倍数(0°/90°/180°/270°)进行 旋转。 快速亮暗线调节 调节模组拼接和箱体拼接造成的亮暗线，改善亮 暗线引起的视觉突兀感。调节过程中即时生效， 简单易用。预存画面设置 NovaLCT 需是 V5.2.0 及以上版本。  固件程序回读 自定义开机、网线断开、无视频源信号时显示屏 回读接收卡的固件程序并保存到本地。 的画面。画面90°倍数旋转 使整屏的亮色度达到高度... ",
      },
      {
        id: "4",
        name: "DH426/HDH756",
        recommend: 0,
        desc: "强劲性能，无惧考验",
        img: "@/assets/card.png",
        detail:
          "色彩管理  3D功能 将显示色域在不同色域间自由实时地切换，使显 配合支持 3D 功能的发送卡，输出 3D 画面。  RGB 独立 Gamma 调节 示屏的色彩呈现更精准。 配合支持 RGB 独立 Gamma 调节的独立主控和 18bit+ 4 倍提升显示灰阶，有效处理低亮时灰度丢失问 NovaLCT(V5.2.0 及以上版本)，通过对“红 题，使图像显示更细腻。 Gamma”、“绿 Gamma”、“蓝 Gamma”分别进行 调节，有效控制显示屏低灰不均匀、白平衡漂移 逐点亮色度校正 等问题，使画面更加真实。 配合诺瓦高精度校正系统，对每个灯点的亮度和 色度进行校正，有效消除亮度差异和色度差异，  画面90°倍数旋转 使整屏的亮色度达到高度一致。 画面以 90°的倍数(0°/90°/180°/270°)进行 旋转。 快速亮暗线调节 调节模组拼接和箱体拼接造成的亮暗线，改善亮 暗线引起的视觉突兀感。调节过程中即时生效， 简单易用。预存画面设置 NovaLCT 需是 V5.2.0 及以上版本。  固件程序回读 自定义开机、网线断开、无视频源信号时显示屏 回读接收卡的固件程序并保存到本地。 的画面。画面90°倍数旋转 使整屏的亮色度达到高度... ",
      },
      {
        id: "5",
        name: "5-MRV328",
        recommend: 0,
        desc: "匠心打造，为效率而生",
        img: "@/assets/card.png",
        detail:
          "色彩管理  3D功能 将显示色域在不同色域间自由实时地切换，使显 配合支持 3D 功能的发送卡，输出 3D 画面。  RGB 独立 Gamma 调节 示屏的色彩呈现更精准。 配合支持 RGB 独立 Gamma 调节的独立主控和 18bit+ 4 倍提升显示灰阶，有效处理低亮时灰度丢失问 NovaLCT(V5.2.0 及以上版本)，通过对“红 题，使图像显示更细腻。 Gamma”、“绿 Gamma”、“蓝 Gamma”分别进行 调节，有效控制显示屏低灰不均匀、白平衡漂移 逐点亮色度校正 等问题，使画面更加真实。 配合诺瓦高精度校正系统，对每个灯点的亮度和 色度进行校正，有效消除亮度差异和色度差异，  画面90°倍数旋转 使整屏的亮色度达到高度一致。 画面以 90°的倍数(0°/90°/180°/270°)进行 旋转。 快速亮暗线调节 调节模组拼接和箱体拼接造成的亮暗线，改善亮 暗线引起的视觉突兀感。调节过程中即时生效， 简单易用。预存画面设置 NovaLCT 需是 V5.2.0 及以上版本。  固件程序回读 自定义开机、网线断开、无视频源信号时显示屏 回读接收卡的固件程序并保存到本地。 的画面。画面90°倍数旋转 使整屏的亮色度达到高度... ",
      },
      {
        id: "6",
        name: "6-DH75122",
        recommend: 0,
        desc: "强劲性能，无惧考验",
        img: "@/assets/card.png",
        detail:
          "色彩管理  3D功能 将显示色域在不同色域间自由实时地切换，使显 配合支持 3D 功能的发送卡，输出 3D 画面。  RGB 独立 Gamma 调节 示屏的色彩呈现更精准。 配合支持 RGB 独立 Gamma 调节的独立主控和 18bit+ 4 倍提升显示灰阶，有效处理低亮时灰度丢失问 NovaLCT(V5.2.0 及以上版本)，通过对“红 题，使图像显示更细腻。 Gamma”、“绿 Gamma”、“蓝 Gamma”分别进行 调节，有效控制显示屏低灰不均匀、白平衡漂移 逐点亮色度校正 等问题，使画面更加真实。 配合诺瓦高精度校正系统，对每个灯点的亮度和 色度进行校正，有效消除亮度差异和色度差异，  画面90°倍数旋转 使整屏的亮色度达到高度一致。 画面以 90°的倍数(0°/90°/180°/270°)进行 旋转。 快速亮暗线调节 调节模组拼接和箱体拼接造成的亮暗线，改善亮 暗线引起的视觉突兀感。调节过程中即时生效， 简单易用。预存画面设置 NovaLCT 需是 V5.2.0 及以上版本。  固件程序回读 自定义开机、网线断开、无视频源信号时显示屏 回读接收卡的固件程序并保存到本地。 的画面。画面90°倍数旋转 使整屏的亮色度达到高度... ",
      },
      {
        id: "7",
        name: "7-DH75123",
        recommend: 0,
        desc: "强劲性能，无惧考验",
        img: "@/assets/card.png",
        detail:
          "色彩管理  3D功能 将显示色域在不同色域间自由实时地切换，使显 配合支持 3D 功能的发送卡，输出 3D 画面。  RGB 独立 Gamma 调节 示屏的色彩呈现更精准。 配合支持 RGB 独立 Gamma 调节的独立主控和 18bit+ 4 倍提升显示灰阶，有效处理低亮时灰度丢失问 NovaLCT(V5.2.0 及以上版本)，通过对“红 题，使图像显示更细腻。 Gamma”、“绿 Gamma”、“蓝 Gamma”分别进行 调节，有效控制显示屏低灰不均匀、白平衡漂移 逐点亮色度校正 等问题，使画面更加真实。 配合诺瓦高精度校正系统，对每个灯点的亮度和 色度进行校正，有效消除亮度差异和色度差异，  画面90°倍数旋转 使整屏的亮色度达到高度一致。 画面以 90°的倍数(0°/90°/180°/270°)进行 旋转。 快速亮暗线调节 调节模组拼接和箱体拼接造成的亮暗线，改善亮 暗线引起的视觉突兀感。调节过程中即时生效， 简单易用。预存画面设置 NovaLCT 需是 V5.2.0 及以上版本。  固件程序回读 自定义开机、网线断开、无视频源信号时显示屏 回读接收卡的固件程序并保存到本地。 的画面。画面90°倍数旋转 使整屏的亮色度达到高度... ",
      },
      {
        id: "8",
        name: "8-DH75124",
        recommend: 0,
        desc: "强劲性能，无惧考验",
        img: "@/assets/card.png",
        detail:
          "色彩管理  3D功能 将显示色域在不同色域间自由实时地切换，使显 配合支持 3D 功能的发送卡，输出 3D 画面。  RGB 独立 Gamma 调节 示屏的色彩呈现更精准。 配合支持 RGB 独立 Gamma 调节的独立主控和 18bit+ 4 倍提升显示灰阶，有效处理低亮时灰度丢失问 NovaLCT(V5.2.0 及以上版本)，通过对“红 题，使图像显示更细腻。 Gamma”、“绿 Gamma”、“蓝 Gamma”分别进行 调节，有效控制显示屏低灰不均匀、白平衡漂移 逐点亮色度校正 等问题，使画面更加真实。 配合诺瓦高精度校正系统，对每个灯点的亮度和 色度进行校正，有效消除亮度差异和色度差异，  画面90°倍数旋转 使整屏的亮色度达到高度一致。 画面以 90°的倍数(0°/90°/180°/270°)进行 旋转。 快速亮暗线调节 调节模组拼接和箱体拼接造成的亮暗线，改善亮 暗线引起的视觉突兀感。调节过程中即时生效， 简单易用。预存画面设置 NovaLCT 需是 V5.2.0 及以上版本。  固件程序回读 自定义开机、网线断开、无视频源信号时显示屏 回读接收卡的固件程序并保存到本地。 的画面。画面90°倍数旋转 使整屏的亮色度达到高度... ",
      },
      {
        id: "9",
        name: "9-DH75125",
        recommend: 0,
        desc: "强劲性能，无惧考验",
        img: "src/assets/card.png",
        detail:
          "色彩管理  3D功能 将显示色域在不同色域间自由实时地切换，使显 配合支持 3D 功能的发送卡，输出 3D 画面。  RGB 独立 Gamma 调节 示屏的色彩呈现更精准。 配合支持 RGB 独立 Gamma 调节的独立主控和 18bit+ 4 倍提升显示灰阶，有效处理低亮时灰度丢失问 NovaLCT(V5.2.0 及以上版本)，通过对“红 题，使图像显示更细腻。 Gamma”、“绿 Gamma”、“蓝 Gamma”分别进行 调节，有效控制显示屏低灰不均匀、白平衡漂移 逐点亮色度校正 等问题，使画面更加真实。 配合诺瓦高精度校正系统，对每个灯点的亮度和 色度进行校正，有效消除亮度差异和色度差异，  画面90°倍数旋转 使整屏的亮色度达到高度一致。 画面以 90°的倍数(0°/90°/180°/270°)进行 旋转。 快速亮暗线调节 调节模组拼接和箱体拼接造成的亮暗线，改善亮 暗线引起的视觉突兀感。调节过程中即时生效， 简单易用。预存画面设置 NovaLCT 需是 V5.2.0 及以上版本。  固件程序回读 自定义开机、网线断开、无视频源信号时显示屏 回读接收卡的固件程序并保存到本地。 的画面。画面90°倍数旋转 使整屏的亮色度达到高度... ",
      },
      {
        id: "10",
        name: "last-DH75125",
        recommend: 0,
        desc: "强劲性能，无惧考验",
        img: "@/assets/card.png",
        detail:
          "色彩管理  3D功能 将显示色域在不同色域间自由实时地切换，使显 配合支持 3D 功能的发送卡，输出 3D 画面。  RGB 独立 Gamma 调节 示屏的色彩呈现更精准。 配合支持 RGB 独立 Gamma 调节的独立主控和 18bit+ 4 倍提升显示灰阶，有效处理低亮时灰度丢失问 NovaLCT(V5.2.0 及以上版本)，通过对“红 题，使图像显示更细腻。 Gamma”、“绿 Gamma”、“蓝 Gamma”分别进行 调节，有效控制显示屏低灰不均匀、白平衡漂移 逐点亮色度校正 等问题，使画面更加真实。 配合诺瓦高精度校正系统，对每个灯点的亮度和 色度进行校正，有效消除亮度差异和色度差异，  画面90°倍数旋转 使整屏的亮色度达到高度一致。 画面以 90°的倍数(0°/90°/180°/270°)进行 旋转。 快速亮暗线调节 调节模组拼接和箱体拼接造成的亮暗线，改善亮 暗线引起的视觉突兀感。调节过程中即时生效， 简单易用。预存画面设置 NovaLCT 需是 V5.2.0 及以上版本。  固件程序回读 自定义开机、网线断开、无视频源信号时显示屏 回读接收卡的固件程序并保存到本地。 的画面。画面90°倍数旋转 使整屏的亮色度达到高度... ",
      },
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
  cursor: pointer;
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
      padding-bottom: 17px;
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
    /deep/.ant-radio {
      /deep/ .ant-radio-inner {
        width: 20px;
        height: 20px;
      }
    }
  }
}
.modal-info-container {
  display: flex;
  height: 100%;
  width: 100%;
  padding: 40px 80px;
  .modal-info-left {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-right: 90px;
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

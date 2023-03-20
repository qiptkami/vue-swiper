<template>
  <div>
    <a-modal
      :width="width"
      :title="title"
      :visible="visible"
      :confirm-loading="confirmLoading"
      @ok="onOk"
      @cancel="onCancel"
      destroyOnClose
      :maskClosable="false"
      :keyboard="false"
      cancelText="取消"
      okText="确认"
    >
      <slot></slot>
    </a-modal>
  </div>
</template>
<script>
import Vue from "vue";
import "ant-design-vue/dist/antd.css";
import { Modal } from "ant-design-vue";

Vue.use(Modal);
export default {
  components: {
    "a-modal": Modal,
  },
  props: {
    title: { type: String },
    width: { type: Number },
    visible: { type: Boolean },
    onOk: { type: Function },
    onCancel: { type: Function },
    data: {},
  },
  data() {
    return {
      infoData: {},
      confirmLoading: false,
    };
  },
  created() {},
  methods: {},
};
</script>
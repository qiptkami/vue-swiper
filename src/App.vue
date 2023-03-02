<template>
  <div>
    <div id="app">
      <div class="container">
        <control-card></control-card>
      </div>
    </div>
  </div>
</template>

<script>
import ControlCard from "./components/ControlCard.vue";

export default {
  name: "App",
  components: {
    ControlCard,
  },
  data() {
    return {};
  },
  created() {},
  watch: {},
  methods: {},
};
</script>

<style lang="less" scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  padding-top: 60px;
  display: flex;
  justify-content: center;
  .container {
    width: 1180px;
    height: 252px;
    background: #f0f0f4;
  }
}
</style>

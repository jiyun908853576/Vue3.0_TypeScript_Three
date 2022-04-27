<template>
  <div class="provide"></div>
</template>

<script>
import { reactive,provide } from "vue";
export default {
  name: "provide",
  setup() {
    let car = reactive({
      name: "奥迪",
      price: "100W",
    });
    // 实现祖孙组件间通信,即父组件定义，后面所有子代组件都能用
    provide('car',car);
  },
};
</script>

<style>
</style>
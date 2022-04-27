<template>
  <!-- 碎片 -->
  <div class="Fragment"></div>
  <div class="sun">{{ name }}</div>
  <!-- Teleport能够直接帮助我们将组件渲染后页面中的任意地方 -->
  <teleport to="#main">
      <div class="main">
          乔亚东😂
      </div>
  </teleport>
</template>

<script>
import { toRef } from "vue";
export default {
  name: "Fragment",
  setup() {
    const name = toRef("孙君卓是大佬");
    return {
      name
    };
  },
};
</script>
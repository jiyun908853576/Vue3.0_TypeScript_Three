<template>
  <div class="markRaw"></div>
</template>

<script>
import { reactive, toRaw,markRaw } from "@vue";
export default {
  name: "markRaw",
  setup() {
    const header = reactive({
      title: "北京"
    });
    // 作用：将一个由reactive生成的响应式对象转换为普通对象
    // 场景：用于读取响应式对象对应的普通对象，对于这个普通对象的所有操作，不会引起页面的更新
    const raw_header = toRaw(header);
    console.log(raw_header, "raw_header");
    // 标记一个对象，使其永远不会再成为响应式对象
    const mark_header = markRaw(header);
    console.log(mark_header, "mark_header");
    return {
      raw_header
    };
  },
};
</script>

<style scoped>
</style>
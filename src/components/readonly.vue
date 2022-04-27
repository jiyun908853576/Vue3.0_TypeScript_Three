<template>
  <div class="readonly">
      <p>{{readonly_title}}</p>
      <p>{{shallowReadonly_title}}</p>
  </div>
</template>

<script>
import { readonly,shallowReadonly } from "@vue";
export default {
  name: "readonly",
  setup() {
    // 深只读
    const readonly_title = readonly("北京");
    // 浅只读(第一层数据不不能修改)
    const shallowReadonly_title = shallowReadonly('上海');
    return {
      readonly_title,
      shallowReadonly_title
    };
  },
};
</script>

<style>
</style>
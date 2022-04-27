<template>
  <div class="customRef"></div>
</template>

<script>
import {inject } from "vue";

export default {
  name: "customRef",
  setup() {
    const car = inject("car");
    return {
      car
    };
  },
};
</script>
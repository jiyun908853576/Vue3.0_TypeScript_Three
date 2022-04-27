<template>
  <div class="HelloWorld">
    <div class="Work_points">
      <p>{{ title }}</p>
      <p>{{ fullName }}</p>
      <p>乔亚东--😂</p>
    </div>
  </div>
</template>

<script>
import {defineComponent, watch, computed, reactive, ref, watchEffect,toRefs, shallowReactive } from "vue";
export default defineComponent({
  name: "HelloWorld",
  // 为Vue3.0新注入的API
  setup() {
    const num = ref(0);
    // 不需要指明监视哪个竖向，监视的回调中用到哪个属性，就监视那个属性(注重的是过程,所以不需要写返回值)
    watchEffect(()=>{
      const x1 = num.value;
      console.log(x1,'watchEffect被调用了');
    });
    // 需要指明监视的属性 也要指明监视的回调(注重的是结果,所以必须要有返回值)
    watch(
      num,
      (newVal, oldVal) => {
        console.log(newVal, "newVal");
        console.log(oldVal, "oldVal");
      },
      { immediate: true }
    );
    // 此处无法正确的获得oldVal deep:true 无效
    watch(header, (newVal, oldVal) => {
      console.log(newVal, "newVal");
      console.log(oldVal, "oldVal");
    });
    // 计算属性 作为一个单独的函数需要引入
    let fullName = computed(() => {
      return header.max + header.min;
    });
    let obj = {
      name:'ljh',
      age:24,
      happy:{
        age:30
      }
    }
    // shallowReactive也是只能监听对象的第一层属性(浅响应式)
    let shallowReactiveObj = shallowReactive(obj);
    console.log(shallowReactiveObj,'shallowReactiveObj')
    // Proxy的实例对象
    const header = reactive({
      title: "任务赢工分",
      max: 10,
      min: 1,
    });
    // 返回值为对象 或者是一个渲染函数
    return {
      ...toRefs(header),
      fullName,
    };
  },
});
</script>

<style scoped>
.HelloWorld {
  background-color: #f4bdbd;
  width: 100%;
}
.Work_points {
  background-color: #fff;
  margin: 0 20px;
  border-radius: 8px;
  height: 200px;
}
</style>
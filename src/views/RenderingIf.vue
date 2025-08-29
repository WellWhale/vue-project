<!-- 0829메모장 -->

<template>
  <div>
    <h3>{{ msg }}</h3>
    <p v-if="type == 'a'">A를 선택했습니다</p>
    <p v-else-if="type == 'b'">B를 선택했습니다</p>
    <p v-else>a, b가 아닙니다</p>
  </div>
  <div>
    <p v-if="showItem">v-if 조건을 만족합니다</p>
    <p v-else>v-if 조건을 만족하지 않습니다</p>
    <button v-on:click="changeValue">showItem값을 변경</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      msg: "v-if 수업",
      type: "a",
      showItem: true,
    };
  },
  methods: {
    changeValue() {
      this.showItem = !this.showItem;
    },
  },
};
</script>

<style></style>

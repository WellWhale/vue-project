<!--0901 메모장-->

<template>
  <div class="parent-container">
    {{ msg }} / {{ age }}
    <button v-on:click="toggleDetails">Toggle</button>
    <PageTitle
      v-bind:title="title"
      v-bind:likes="likeCnt"
      v-bind:isOk="OkValue"
      v-bind:memberList="members"
      v-bind:isShow="showDetail"
      v-on:child-clicked="handleChildClick"
    />
  </div>
</template>

<script>
import PageTitle from "../components/PageTitle.vue";
export default {
  components: {
    PageTitle,
  },
  data() {
    return {
      msg: "Parent Component",
      age: 0,
      title: "Dynamic Data from Parent",
      likeCnt: 3,
      OkValue: true,
      showDetail: true,
      members: [
        { name: "father", age: 40 },
        { name: "mother", age: 35 },
        { name: "son", age: 6 },
      ],
    };
  },
  methods: {
    toggleDetails() {
      this.showDetail = !this.showDetail;
    },
    handleChildClick(payload) {
      const { name = "Lee", age = 20 } = payload || {};
      // name, age가 "", 0인 경우까지 커버하려면 아래처럼 강화:
      this.msg = name && name.trim() ? name : "Lee";
      this.age =
        age !== undefined && age !== null && age !== "" ? Number(age) : 20;
    },
  },
  // mounted() {
  //   console.log(this);
  // },
};
</script>

<style>
.parent-container {
  border: 2px solid green;
}
</style>

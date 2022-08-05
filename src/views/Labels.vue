<template>
  <div class="nav-wrapper">
    <div class="content">
      <p>Labels</p>
    </div>
    <Nav />
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import Labels from "@/views/Labels.vue";

export default Vue.extend({});
</script>

<style lang="scss" scoped>
.nav-wrapper {
  border: 1px solid green;
  display: flex;
  flex-direction: column; //上下布局
  height: 100vh;
}
.content {
  overflow: auto;
  flex-grow: 1; //使content尽量占据所有高度
}
</style>

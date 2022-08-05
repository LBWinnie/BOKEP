<template>
  <div class="nav">
    <router-link to="/Money">记账</router-link> |
    <router-link to="/Labels">标签</router-link> |
    <router-link to="/Statistics">统计</router-link>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import Nav from "@/components/Nav.vue";

export default Vue.extend({});
</script>

<style lang="scss" scoped>
.nav {
  border: 1px solid red;
}
</style>

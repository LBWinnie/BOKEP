<template>
  <Layout>
    <Tabs :classPrefix="type" :dataSource="type" :vlaue.sync="typeList" />
    <Tabs
      :classPrefix="interval"
      :dataSource="intervalList"
      :vlaue.sync="interval"
    />
  </Layout>
</template>

<script lang="ts">
import Types from "@/components/Money/Types.vue";
import Vue from "vue";
import { Component } from "vue-property-decorator";
import Tabs from "@/components/Tabs.vue";
@Component({
  components: { Tabs, Types },
})
export default class Statistics extends Vue {
  type = "-";
  interval = "day";
  intervalList = [
    { text: "按天", vlaue: "day" },
    { text: "按周", vlaue: "week" },
    { text: "按月", vlaue: "month" },
  ];
  typeList = [
    { text: "支出", vlaue: "-" },
    { text: "收入", vlaue: "+" },
  ];
}
</script>
<style scoped lang="scss">
::v-deep {
  .type-tabs-item {
    background: #c4c4c4;
    &.selected {
      background: white;
      &::after {
        display: none;
      }
    }
  }
}
</style>

<template>
  <Layout class-prefix="layout">
    <NumberPad :value.sync="record.amount" @submit="saveRecord" />
    <Tabs :data-source="recordTypeList" :value.sync="record.type" />
    <div class="remark">
      <div class="notes">
        <Icon name="notes" />
        <FormItem placeholder="添加备注.." :value.sync="record.notes" />
      </div>
      <div class="createdAt">
        <FormItem
          type="date"
          placeholder="输入日期"
          :value.sync="record.createdAt"
        />
      </div>
    </div>
    <Tags @update:value="record.tags = $event" />
  </Layout>
</template>

<script lang="ts">
import Vue from "vue";
import NumberPad from "@/components/Money/NumberPad.vue";
import FormItem from "@/components/Money/FormItem.vue";
import Tags from "@/components/Money/Tags.vue";
import { Component } from "vue-property-decorator";
import Tabs from "@/components/Tabs.vue";
import recordTypeList from "@/constants/recordTypeList";
import Icon from "@/components/Icon.vue";
@Component({
  components: { Tabs, Tags, FormItem, NumberPad },
})
export default class Money extends Vue {
  get recordList() {
    return this.$store.state.recordList;
  }
  recordTypeList = recordTypeList;
  record: RecordItem = {
    tags: [],
    notes: "",
    type: "-",
    amount: 0,
    createdAt: new Date().toISOString(),
  };
  created() {
    this.$store.commit("fetchRecords");
  }
  onUpdateNotes(value: string) {
    this.record.notes = value;
  }
  saveRecord() {
    if (!this.record.tags || this.record.tags.length === 0) {
      return window.alert("请至少选择一个标签");
    }
    this.$store.commit("createRecord", this.record);
    if (this.$store.state.createRecordError === null) {
      window.alert("已保存");
      this.record.notes = "";
    }
  }
}
</script>

<style lang="scss" scoped>
::v-deep .layout-content {
  display: flex;
  flex-direction: column-reverse;
}
.remark {
  display: flex;
  align-items: center;

  > .createdAt {
    border: 1px solid red;
    width: 40%;
  }
  > .notes {
    border: 1px solid blue;
    width: 60%;
    position: relative;
    > .icon {
      border: 1px solid green;
      position: absolute;
      left: 16px;
      top: 50%;
      transform: translateY(-50%);
    }
  }
}
</style>

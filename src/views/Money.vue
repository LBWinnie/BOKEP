<template>
  <Layout class-prefix="layout">
    <NumberPad :value.sync="record.amount" @submit="saveRecord" />
    <FormItem
      field-name="📝 备注 :"
      placeholder="添加备注.."
      :value.sync="record.notes"
    />

    <Tabs :data-source="recordTypeList" :value.sync="record.type" />
    <div class="remark">
      <div class="createdAt">
        <FormItem
          field-name="⏳ 日期 :"
          type="date"
          placeholder="选择日期"
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
    margin-left: auto;
  }
}
</style>

<template>
  <t-space direction="vertical">
    <p style="margin: 10px">自定义头部、底部及操作按钮的渲染</p>
    <t-transfer :data="list" :operation="['移除', '加入']" class="tdesign-transfer-custom">
      <template v-slot:title="props" :name="123">
        <div>{{ props.type === 'target' ? '目标' : '来源' }}</div>
      </template>
      <template v-slot:operation="props" :name="123">
        {{ props.direction === 'left' ? '移除' : '加入' }}
      </template>
      <template v-slot:footer="props" :name="123">
        <div style="padding: 12px 20px">
          <span v-if="props.type === 'source'">选中并加入</span>
          <span v-else>选中并移除</span>
        </div>
      </template>
    </t-transfer>
    <br />
    <p style="margin: 10px">自定义渲染数据</p>
    <t-transfer
      theme="primary"
      :data="customList"
      v-model="targetValue2"
      :checked-value="checkedValue2"
      :transfer-item="transferItem"
    >
    </t-transfer>
  </t-space>
</template>
<script lang="jsx">
const list = [];
for (let i = 0; i < 20; i++) {
  list.push({
    value: i.toString(),
    label: `内容${i + 1}`,
  });
}

const customList = [];
for (let i = 0; i < 20; i++) {
  customList.push({
    value: i.toString(),
    label: `内容${i + 1}`,
    description: `第${i + 1}段信息`,
  });
}
export default {
  data() {
    return {
      list,
      customList,
      targetValue: [],
      checkedValue: [],
      targetValue2: [],
      checkedValue2: [],
    };
  },
  methods: {
    transferItem(h, { data, index, type }) {
      const sourceLabel = (
        <span class="transfer-item">
          {data.label} - {data.description}
        </span>
      );
      const targetLabel = (
        <span class="transfer-item">
          {index} - {data.label}
        </span>
      );
      return type === 'source' ? sourceLabel : targetLabel;
    },
  },
};
</script>
<style>
.tdesign-transfer-custom .t-button .t-icon {
  display: none;
}
.tdesign-transfer-custom .t-icon + .t-button__text:not(:empty) {
  margin-left: 0;
}
</style>

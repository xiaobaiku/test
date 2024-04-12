<template>
  <p>MyTreeSelect</p>
  <MyTreeSelect
    v-model:value="value"
    v-model:searchValue="searchValue"
    show-search
    style="width: 100%"
    :dropdown-style="{ maxHeight: '400px', overflow: 'auto' }"
    placeholder="Please select"
    allow-clear
    tree-default-expand-all
    :tree-data="treeData"
    tree-node-filter-prop="label"
  >
    <template #title="{ value: val, label }">
      <b v-if="val === 'parent 1-1'" style="color: #08c">sss</b>
      <template v-else>
        <template
          v-for="(fragment, i) in label
            .toString()
            .split(new RegExp(`(?<=${searchValue})|(?=${searchValue})`, 'i'))"
        >
          <span
            v-if="fragment.toLowerCase() === searchValue.toLowerCase()"
            :key="i"
            style="color: #08c"
          >
            {{ fragment }}
          </span>
          <template v-else>{{ fragment }}</template>
        </template>
      </template>
    </template>
  </MyTreeSelect>
  <p>antdv TreeSelect</p>
  <TreeSelect
    v-model:value="value"
    v-model:searchValue="searchValue"
    show-search
    style="width: 100%"
    :dropdown-style="{ maxHeight: '400px', overflow: 'auto' }"
    placeholder="Please select"
    allow-clear
    tree-default-expand-all
    :tree-data="treeData"
    tree-node-filter-prop="label"
  >
    <template #title="{ value: val, label }">
      <b v-if="val === 'parent 1-1'" style="color: #08c">sss</b>
      <template v-else>
        <template
          v-for="(fragment, i) in label
            .toString()
            .split(new RegExp(`(?<=${searchValue})|(?=${searchValue})`, 'i'))"
        >
          <span
            v-if="fragment.toLowerCase() === searchValue.toLowerCase()"
            :key="i"
            style="color: #08c"
          >
            {{ fragment }}
          </span>
          <template v-else>{{ fragment }}</template>
        </template>
      </template>
    </template>
  </TreeSelect>
</template>
<script setup>
import { ref, watch } from 'vue';
import { TreeSelect } from 'ant-design-vue'
import MyTreeSelect from './components/MyTreeSelect.vue';
const value = ref();
const treeData = ref([
  {
    label: 'parent 1',
    value: 'parent 1',
    children: [
      {
        label: 'parent 1-0',
        value: 'parent 1-0',
        children: [
          {
            label: 'parent 1-0-0',
            value: 'parent 1-0-0',
            children: [
              {
                label: 'my leaf',
                value: 'leaf1',
              },
              {
                label: 'your leaf',
                value: 'leaf2',
              },
            ],
          },
          {
            label: 'parent 1-0-1',
            value: 'parent 1-0-1',
          },
        ],
      },
      {
        label: 'parent 1-1',
        value: 'parent 1-1',
      },
    ],
  },
]);
watch(value, () => {
  console.log(value.value);
});
const searchValue = ref('');
</script>
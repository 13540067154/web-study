<template>
      <a-tree v-model:expandedKeys="expandedKeys" v-model:selectedKeys="selectedKeys" v-model:checkedKeys="checkedKeys"
            checkable :tree-data="treeData">
            <template #title="{ title, key }">
                  <span v-if="key === '0-0-1-0'" style="color: #1890ff">{{ title }}</span>
                  <template v-else>{{ title }}</template>
            </template>
      </a-tree>
</template>
<script lang="ts">
import type { TreeProps } from 'ant-design-vue';
import { defineComponent, ref, watch, onMounted } from 'vue';
import CustomDragDrop from '@/utils/CustomDragDrop'

const treeData: TreeProps['treeData'] = [
      {
            title: 'parent 1',
            key: '0-0',
            children: [
                  {
                        title: 'parent 1-0',
                        key: '0-0-0',
                        disabled: true,
                        children: [
                              { title: 'leaf', key: '0-0-0-0', disableCheckbox: true },
                              { title: 'leaf', key: '0-0-0-1' },
                        ],
                  },
                  {
                        title: 'parent 1-1',
                        key: '0-0-1',
                        children: [{ key: '0-0-1-0', title: 'sss' }],
                  },
            ],
      },
];

export default defineComponent({
      setup() {
            const expandedKeys = ref<string[]>(['0-0-0', '0-0-1']);
            const selectedKeys = ref<string[]>(['0-0-0', '0-0-1']);
            const checkedKeys = ref<string[]>(['0-0-0', '0-0-1']);
            watch(expandedKeys, () => {
                  console.log('expandedKeys', expandedKeys);
            });
            watch(selectedKeys, () => {
                  console.log('selectedKeys', selectedKeys);
            });
            watch(checkedKeys, () => {
                  console.log('checkedKeys', checkedKeys);
            });
            onMounted(() => {
                  new CustomDragDrop({
                        el: '.ant-tree-list-holder-inner'
                  })
            })
            return {
                  treeData,
                  expandedKeys,
                  selectedKeys,
                  checkedKeys,
            };
      },
});
</script>
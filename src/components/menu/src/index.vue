<script setup lang="ts">
import { toLine } from '@/utils'
import type { PropType } from 'vue'
import type { MenuItem } from './types'

const props = defineProps({
  // 导航菜单的数据
  data: {
    type: Array as PropType<MenuItem[]>,
    required: true
  },
  // 默认选中菜单
  defaultActive: {
    type: String,
    default: ''
  },
  // 是否是路由模式
  router: {
    type: Boolean,
    default: false
  }
})
</script>

<template>
  <el-menu :defaultActive="defaultActive" :router="router" v-bind="$attrs">
    <template v-for="(item, index) in data" :key="index">
      <el-menu-item v-if="!item.children || !item.children.length" :index="item.index">
        <component v-if="item.icon" :is="`el-icon-${toLine(item.icon)}`"></component>
        <span>{{ item.name }}</span>
      </el-menu-item>
      <el-sub-menu v-if="item.children && item.children.length" :index="item.index">
        <template #title>
          <component v-if="item.icon" :is="`el-icon-${toLine(item.icon)}`"></component>
          <span>{{ item.name }}</span>
        </template>
        <el-menu-item v-for="(item1, index1) in item.children" :key="index1" :index="item1.index">
          <component v-if="item1.icon" :is="`el-icon-${toLine(item1.icon)}`"></component>
          <span>{{ item1.name }}</span>
        </el-menu-item>
      </el-sub-menu>
    </template>
  </el-menu>
</template>

<style lang="scss" scoped>
svg {
  margin-right: 4px;
}
</style>

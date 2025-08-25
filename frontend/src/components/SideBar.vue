<template>
  <!-- 左侧侧边栏 -->
  <n-layout-sider
    bordered
    collapse-mode="width"
    :collapsed-width="64"
    width="200"
    show-trigger
  >
    <div style="padding: 16px; border-bottom: 1px solid #e5e7eb;">
      <h3 style="margin: 0; color: #374151;">IDRAC 控制台</h3>
    </div>
    <n-menu
      v-model:value="activeKey"
      :options="menuOptions"
      :collapsed="false"
    />
  </n-layout-sider>
</template>

<script setup lang="ts">
import { ref, h } from 'vue'
import { NIcon } from 'naive-ui'

// 引入图标（这里我用的是 ionicons，你也可以换）
import { WifiOutline, ListOutline, GlobeOutline, SettingsOutline } from '@vicons/ionicons5'

/**
 * 当前激活的菜单项
 */
const activeKey = ref<string | null>('agent')

/**
 * 渲染菜单图标的方法
 */
const renderIcon = (icon: any) => {
  return () => h(NIcon, null, { default: () => h(icon) })
}

/**
 * 菜单配置
 */
const menuOptions = [
  {
    label: 'Dell',
    key: 'agent',
    icon: renderIcon(WifiOutline)
  },
  {
    label: '华为',
    key: 'subscribe',
    icon: renderIcon(ListOutline)
  },
  {
    label: '浪潮',
    key: 'connect',
    icon: renderIcon(GlobeOutline)
  },
  {
    label: '更新记录',
    key: 'settings',
    icon: renderIcon(SettingsOutline)
  }
]
</script>

<style scoped>
/* 确保侧边栏样式正确 */
:deep(.n-layout-sider) {
  background-color: #fff;
  border-right: 1px solid #e5e7eb;
}

:deep(.n-menu) {
  height: 100%;
}

:deep(.n-menu-item) {
  margin: 4px 8px;
  border-radius: 6px;
}

:deep(.n-menu-item:hover) {
  background-color: #f3f4f6;
}

:deep(.n-menu-item--selected) {
  background-color: #e0f2fe;
  color: #0284c7;
}
</style>

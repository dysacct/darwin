<script setup lang="ts">
import { ref } from 'vue'
import {
  NConfigProvider,
  NCard, NSpace, NInput, NGrid, NGridItem
} from 'naive-ui'

// ipmi填写区域的输入绑定
const ipmiIp = ref('')


// 当前选中的菜单项
const activeMenu = ref('idrac')

// 菜单点击处理
function handleMenuClick(menuKey: string) {
  activeMenu.value = menuKey
}

// 暂时用 alert 做占位，确认事件能触发
function onLaunchJnlp() {
  window.alert('TODO: 这里将来调用 Go/Wails 启动 JNLP')
}
function onFanSpeed() {
  window.alert('TODO: 这里将来打开风扇转速控制面板')
}
function onNfsMount() {
  window.alert('TODO: 这里将来做 NFS 介质挂载操作')
}
</script>

<template>
  <n-config-provider>
    <div class="app-container">
      <!-- 左侧边栏 -->
      <div class="sidebar">
        <!-- 顶部 Logo 区域 -->
        <div class="sidebar-header">
          <div class="logo-container">
            <div class="logo-icon">
              <img src="./assets/images/darwin.svg" alt="Darwin" class="darwin-logo" />
            </div>
            <div class="logo-text">
              <div class="logo-title">IDRAC</div>
              <div class="logo-subtitle">Console</div>
            </div>
          </div>
        </div>

        <!-- 导航菜单 -->
        <div class="sidebar-menu">
          <div class="menu-item" :class="{ active: activeMenu === 'idrac' }" @click="handleMenuClick('idrac')">
            <div class="menu-icon">
              <img src="./assets/images/darwin.svg" alt="Darwin" class="menu-darwin-logo" />
            </div>
            <div class="menu-text">IDRAC</div>
          </div>
          
          <div class="menu-item" :class="{ active: activeMenu === 'dell' }" @click="handleMenuClick('dell')">
            <div class="menu-icon">
              <img src="./assets/images/dell.svg" alt="Dell" class="vendor-logo dell-logo" />
            </div>
            <div class="menu-text">Dell</div>
          </div>
          
          <div class="menu-item" :class="{ active: activeMenu === 'huawei' }" @click="handleMenuClick('huawei')">
            <div class="menu-icon">
              <img src="./assets/images/huawei.svg" alt="华为" class="vendor-logo huawei-logo" />
            </div>
            <div class="menu-text">华为</div>
          </div>
          
          <div class="menu-item" :class="{ active: activeMenu === 'inspur' }" @click="handleMenuClick('inspur')">
            <div class="menu-icon">
              <img src="./assets/images/inspur.svg" alt="浪潮" class="vendor-logo inspur-logo" />
            </div>
            <div class="menu-text">浪潮</div>
          </div>
          
          <div class="menu-item" :class="{ active: activeMenu === 'logs' }" @click="handleMenuClick('logs')">
            <div class="menu-icon">📊</div>
            <div class="menu-text">更新记录</div>
          </div>
        </div>

        <!-- 底部状态区域 -->
        <div class="sidebar-footer">
          <div class="status-item">
            <div class="status-icon">📡</div>
            <div class="status-text">已连接</div>
          </div>
          <div class="status-item">
            <div class="status-icon">⚡</div>
            <div class="status-text">运行中</div>
          </div>
        </div>
      </div>

      <!-- 右侧内容区域 -->
      <div class="main-content">
        <n-space vertical size="large">
          <!-- ① ipmi 填写区域 字体颜色为白色-->
          <n-card title="ipmi填写区域" size="large" class="ipmi-card">
            <n-input 
              v-model:value="ipmiIp" 
              class="ipmi-input"
              type="textarea"
              :autosize="{ minRows: 3, maxRows: 6 }"
              placeholder="请输入IPMI IP地址，每行一个IP，按回车分隔"
            />
          </n-card>

          <!-- ② 操作按钮区 -->
          <n-card size="large">
            <n-space vertical size="large">
              <button class="n-button n-button--quaternary n-button--success" @click="onLaunchJnlp">启动 jnlp</button>
              <button class="n-button n-button--quaternary n-button--info" @click="onFanSpeed">风扇转速</button>
              <button class="n-button n-button--quaternary n-button--warning" @click="onNfsMount">NFS 介质挂载操作</button>
            </n-space>
          </n-card>

          <!-- ③ 状态区：三列 -->
          <n-card size="large">
            <n-grid :cols="3" x-gap="16" y-gap="8">
              <n-grid-item>
                <div class="section-title">状态</div>
              </n-grid-item>
              <n-grid-item>
                <div class="section-title">ipmi</div>
              </n-grid-item>
              <n-grid-item>
                <div class="section-title">消息</div>
              </n-grid-item>
            </n-grid>
          </n-card>
        </n-space>
      </div>
    </div>
  </n-config-provider>
</template>

<style scoped>
.app-container {
  display: flex;
  height: 100vh;
  width: 100%;
  background-color: #1a1a1a;
}

.sidebar {
  width: 240px;
  background-color: #2a2a2a;
  border-right: 1px solid #3a3a3a;
  display: flex;
  flex-direction: column;
  color: #e0e0e0;
}

.sidebar-header {
  padding: 20px 16px;
  border-bottom: 1px solid #3a3a3a;
  background-color: #1f1f1f;
}

.logo-container {
  display: flex;
  align-items: center;
  gap: 12px;
}

.logo-icon {
  font-size: 24px;
  width: 40px;
  height: 40px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  border-radius: 8px;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
}

.darwin-logo {
  width: 32px;
  height: 32px;
  filter: brightness(0) invert(1);
}

.menu-darwin-logo {
  width: 20px;
  height: 20px;
  filter: brightness(0) invert(1);
}

.logo-text {
  display: flex;
  flex-direction: column;
}

.logo-title {
  font-size: 18px;
  font-weight: 700;
  color: #ffffff;
  line-height: 1.2;
}

.logo-subtitle {
  font-size: 12px;
  color: #888888;
  font-weight: 500;
}

.sidebar-menu {
  flex: 1;
  padding: 16px 8px;
}

.menu-item {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 12px 16px;
  margin: 4px 0;
  border-radius: 8px;
  cursor: pointer;
  transition: all 0.2s ease;
  color: #b0b0b0;
}

.menu-item:hover {
  background-color: #3a3a3a;
  color: #ffffff;
}

.menu-item.active {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: #ffffff;
  font-weight: 500;
}

.menu-icon {
  width: 20px;
  height: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 16px;
}

.vendor-logo {
  width: 20px;
  height: 20px;
  filter: brightness(0) invert(1);
}

.dell-logo {
  filter: brightness(0) invert(1); /* Ensure Dell logo is always white on dark background */
}

.huawei-logo {
  filter: brightness(0) invert(1); /* Ensure Huawei logo is always white on dark background */
}

.inspur-logo {
  filter: brightness(0) invert(1); /* Ensure Inspur logo is always white on dark background */
}

.menu-text {
  font-size: 14px;
  font-weight: 500;
}

.sidebar-footer {
  padding: 16px;
  border-top: 1px solid #3a3a3a;
  background-color: #1f1f1f;
}

.status-item {
  display: flex;
  align-items: center;
  gap: 8px;
  padding: 8px 0;
  font-size: 12px;
  color: #888888;
}

.status-icon {
  font-size: 14px;
}

.status-text {
  font-weight: 500;
}

.main-content {
  flex: 1;
  padding: 20px;
  background-color: #1a1a1a;
  overflow-y: auto;
}

.section-title { 
  font-weight: 600; 
  margin-bottom: 6px; 
  text-align: left;
  color: #e0e0e0;
}

/* .placeholder { 
  color: #888; 
  text-align: left;
} */

/* 确保按钮样式正确 */
.n-button {
  margin: 4px;
  padding: 8px 16px;
  border-radius: 6px;
  border: none;
  cursor: pointer;
  font-size: 14px;
  transition: all 0.2s;
  font-weight: 500;
}

.n-button--success {
  background: linear-gradient(135deg, #18a058 0%, #14a855 100%);
  color: white;
}

.n-button--info {
  background: linear-gradient(135deg, #2080f0 0%, #1c7cd6 100%);
  color: white;
}

.n-button--warning {
  background: linear-gradient(135deg, #f0a020 0%, #e69500 100%);
  color: white;
}

.n-button:hover {
  opacity: 0.9;
  transform: translateY(-1px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
}

/* 深色主题卡片样式 */
:deep(.n-card) {
  background-color: #2a2a2a !important;
  border: 1px solid #3a3a3a !important;
  color: #e0e0e0 !important;
}

:deep(.n-card__header) {
  background-color: #1f1f1f !important;
  border-bottom: 1px solid #3a3a3a !important;
  color: #ffffff !important;
}

:deep(.n-input) {
  background-color: #1f1f1f !important;
  border: 1px solid #3a3a3a !important;
  color: #e0e0e0 !important;
}

:deep(.n-input:focus) {
  border-color: #667eea !important;
  box-shadow: 0 0 0 2px rgba(102, 126, 234, 0.2) !important;
}

:deep(.n-input::placeholder) {
  color: #888888 !important;
}

/* IPMI 填写区域专门样式 */
.ipmi-card {
  margin-bottom: 20px;
}

.ipmi-input {
  width: 100% !important;
  min-height: 120px !important;
}

:deep(.ipmi-input .n-input__input-el) {
  color: #ffffff !important;
  font-size: 14px !important;
  line-height: 1.6 !important;
}

:deep(.ipmi-input .n-input__placeholder) {
  color: #888888 !important;
  font-size: 14px !important;
}

:deep(.ipmi-card .n-card__header) {
  color: #ffffff !important;
  font-size: 16px !important;
  font-weight: 600 !important;
}

/* 操作按钮区域专门样式 */
:deep(.n-button) {
  color: #ffffff !important;
  font-weight: 500 !important;
  font-size: 14px !important;
}

:deep(.n-button--success) {
  background: linear-gradient(135deg, #18a058 0%, #14a855 100%) !important;
  color: #ffffff !important;
}

:deep(.n-button--info) {
  background: linear-gradient(135deg, #2080f0 0%, #1c7cd6 100%) !important;
  color: #ffffff !important;
}

:deep(.n-button--warning) {
  background: linear-gradient(135deg, #f0a020 0%, #e69500 100%) !important;
  color: #ffffff !important;
}
</style>

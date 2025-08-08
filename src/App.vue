<script setup lang="ts">
import { RouterView } from 'vue-router'
</script>

<template>
  <RouterView />
</template>

<style>
/* 全局样式 */
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap');

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Inter', system-ui, sans-serif;
  background-color: #f9fafb;
  color: #1D2129;
  line-height: 1.6;
}

#app {
  min-height: 100vh;
}

/* 颜色变量 */
:root {
  --color-primary: #165DFF;
  --color-secondary: #36BFFA;
  --color-accent: #FF7D00;
  --color-success: #00B42A;
  --color-warning: #FF7D00;
  --color-danger: #F53F3F;
  --color-dark: #1D2129;
  --color-dark-2: #4E5969;
  --color-light-1: #F2F3F5;
  --color-light-2: #E5E6EB;
}

/* 工具类 */
.bg-glass {
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(8px);
  -webkit-backdrop-filter: blur(8px);
}

.text-shadow {
  text-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
}

.text-shadow-lg {
  text-shadow: 0 4px 8px rgba(0, 0, 0, 0.5);
}

.transition-transform {
  transition-property: transform;
  transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
  transition-duration: 300ms;
}

/* 响应式工具 */
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 1rem;
}

@media (max-width: 768px) {
  .container {
    padding: 0 0.5rem;
  }
}

/* 滚动行为 */
html {
  scroll-behavior: smooth;
}

/* 移除按钮默认样式 */
button {
  border: none;
  background: none;
  cursor: pointer;
  font-family: inherit;
}

/* 链接样式 */
a {
  text-decoration: none;
  color: inherit;
}

/* 图片响应式 */
img {
  max-width: 100%;
  height: auto;
}
</style>

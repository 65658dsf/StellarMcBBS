<script setup lang="ts">
import { RouterView } from 'vue-router'
</script>

<template>
  <RouterView />
</template>

<style>
/* 全局样式 */
@import url('@/assets/fonts/Inter.css');

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Inter', system-ui, sans-serif;
  background-color: #f9fafb;
  color: #1d2129;
  line-height: 1.6;
  overflow-x: hidden;
}

#app {
  min-height: 100vh;
}

/* 颜色变量 */
:root {
  --color-primary: #165dff;
  --color-secondary: #36bffa;
  --color-accent: #ff7d00;
  --color-success: #00b42a;
  --color-warning: #ff7d00;
  --color-danger: #f53f3f;
  --color-dark: #1d2129;
  --color-dark-2: #4e5969;
  --color-light-1: #f2f3f5;
  --color-light-2: #e5e6eb;
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

/* 自定义工具类 */
@layer utilities {
  .content-auto {
    content-visibility: auto;
  }
  .text-shadow {
    text-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
  }
  .text-shadow-lg {
    text-shadow: 0 4px 8px rgba(0, 0, 0, 0.5);
  }
  .bg-glass {
    background: rgba(255, 255, 255, 0.1);
    backdrop-filter: blur(8px);
    -webkit-backdrop-filter: blur(8px);
  }
  .transition-transform {
    transition-property: transform;
    transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
    transition-duration: 300ms;
  }
}

/* 字体和背景修复 */
.font-sans {
  font-family: 'Inter', system-ui, sans-serif;
}

.bg-gray-50 {
  background-color: #f9fafb;
}

.text-dark {
  color: #1d2129;
}

.overflow-x-hidden {
  overflow-x: hidden;
}

/* 响应式字体修复 */
.text-\[clamp\(2rem\,5vw\,4rem\)\] {
  font-size: clamp(2rem, 5vw, 4rem);
}

.text-\[clamp\(1rem\,2vw\,1\.25rem\)\] {
  font-size: clamp(1rem, 2vw, 1.25rem);
}
</style>

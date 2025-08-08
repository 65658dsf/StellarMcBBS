<template>
  <header id="navbar" class="fixed top-0 left-0 right-0 z-50 transition-all duration-300">
    <nav class="container mx-auto px-4 py-3 flex items-center justify-between bg-glass text-white">
      <div class="flex items-center space-x-2">
        <img
          src="https://picsum.photos/40/40"
          alt="恒星MC社区Logo"
          class="w-10 h-10 rounded-lg"
        />
        <h1 class="text-xl font-bold tracking-tight">恒星MC社区</h1>
      </div>

      <!-- 桌面导航 -->
      <div class="hidden md:flex items-center space-x-8">
        <a href="#servers" class="hover:text-accent transition-colors">服务器列表</a>
        <a href="#stats" class="hover:text-accent transition-colors">社区统计</a>
        <a href="#apply" class="hover:text-accent transition-colors">服务器入驻</a>
        <a href="#contact" class="hover:text-accent transition-colors">联系我们</a>
      </div>

      <!-- 移动端菜单按钮 -->
      <button
        @click="toggleMobileMenu"
        class="md:hidden text-white text-xl"
      >
        <i class="fa fa-bars"></i>
      </button>
    </nav>

    <!-- 移动端导航菜单 -->
    <div
      v-show="isMobileMenuOpen"
      class="md:hidden bg-dark-2 text-white"
    >
      <div class="container mx-auto px-4 py-3 flex flex-col space-y-4">
        <a href="#servers" class="py-2 hover:text-accent transition-colors" @click="closeMobileMenu">服务器列表</a>
        <a href="#stats" class="py-2 hover:text-accent transition-colors" @click="closeMobileMenu">社区统计</a>
        <a href="#apply" class="py-2 hover:text-accent transition-colors" @click="closeMobileMenu">服务器入驻</a>
        <a href="#contact" class="py-2 hover:text-accent transition-colors" @click="closeMobileMenu">联系我们</a>
      </div>
    </div>
  </header>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const isMobileMenuOpen = ref(false)

const toggleMobileMenu = () => {
  isMobileMenuOpen.value = !isMobileMenuOpen.value
}

const closeMobileMenu = () => {
  isMobileMenuOpen.value = false
}
</script>

<style scoped>
.bg-glass {
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(8px);
  -webkit-backdrop-filter: blur(8px);
}
</style>
<template>
  <footer class="bg-dark text-white pt-16 pb-8">
    <div class="max-w-7xl mx-auto px-4">
      <div class="grid grid-cols-1 md:grid-cols-4 gap-8 mb-12">
        <div>
          <div class="flex items-center space-x-2 mb-6">
            <img src="@/assets/favicon.ico" alt="恒星MC社区Logo" class="w-10 h-10 rounded-lg" />
            <h2 class="text-xl font-bold">恒星MC社区</h2>
          </div>
          <p class="text-white/70 mb-6">汇聚优质Minecraft服务器，打造友好的我的世界玩家社区</p>
          <div class="flex space-x-4">
            <a
              href="#"
              class="w-10 h-10 rounded-full bg-white/10 flex items-center justify-center hover:bg-primary transition-colors"
            >
              <i class="fa fa-github"></i>
            </a>
            <a
              href="#"
              class="w-10 h-10 rounded-full bg-white/10 flex items-center justify-center hover:bg-primary transition-colors"
            >
              <i class="fa fa-bilibili"></i>
            </a>
            <a
              href="#"
              class="w-10 h-10 rounded-full bg-white/10 flex items-center justify-center hover:bg-primary transition-colors"
            >
              <i class="fa fa-youtube-play"></i>
            </a>
          </div>
        </div>

        <div>
          <h3 class="text-lg font-semibold mb-6">快速链接</h3>
          <ul class="space-y-3">
            <li>
              <a href="#servers" class="text-white/70 hover:text-white transition-colors"
                >服务器列表</a
              >
            </li>
            <li>
              <a href="#stats" class="text-white/70 hover:text-white transition-colors">社区统计</a>
            </li>
            <li>
              <a href="#apply" class="text-white/70 hover:text-white transition-colors"
                >服务器入驻</a
              >
            </li>
            <li>
              <a href="#contact" class="text-white/70 hover:text-white transition-colors"
                >联系我们</a
              >
            </li>
          </ul>
        </div>

        <div>
          <h3 class="text-lg font-semibold mb-6">资源导航</h3>
          <ul class="space-y-3">
            <li>
              <a href="#" class="text-white/70 hover:text-white transition-colors">游戏下载</a>
            </li>
            <li>
              <a href="#" class="text-white/70 hover:text-white transition-colors">材质包</a>
            </li>
            <li>
              <a href="#" class="text-white/70 hover:text-white transition-colors">模组推荐</a>
            </li>
            <li>
              <a href="#" class="text-white/70 hover:text-white transition-colors">插件资源</a>
            </li>
          </ul>
        </div>

        <div>
          <h3 class="text-lg font-semibold mb-6">法律信息</h3>
          <ul class="space-y-3">
            <li>
              <a href="#" class="text-white/70 hover:text-white transition-colors">服务条款</a>
            </li>
            <li>
              <a href="#" class="text-white/70 hover:text-white transition-colors">隐私政策</a>
            </li>
            <li>
              <a href="#" class="text-white/70 hover:text-white transition-colors">版权声明</a>
            </li>
            <li>
              <a href="#" class="text-white/70 hover:text-white transition-colors">投诉建议</a>
            </li>
          </ul>
        </div>
      </div>

      <div class="border-t border-white/10 pt-8 text-center text-white/50 text-sm">
        <p>© 2023 恒星MC社区 版权所有 | Minecraft 是 Mojang Studios 的注册商标</p>
      </div>
    </div>
  </footer>

  <!-- 回到顶部按钮 -->
  <button
    id="back-to-top"
    class="fixed bottom-8 right-8 w-12 h-12 rounded-full bg-primary text-white shadow-lg flex items-center justify-center opacity-0 invisible transition-all z-50"
  >
    <i class="fa fa-arrow-up"></i>
  </button>
</template>

<script setup lang="ts">
import { onMounted, onUnmounted } from 'vue'

onMounted(() => {
  const backToTopButton = document.getElementById('back-to-top')

  const handleScroll = () => {
    if (backToTopButton) {
      if (window.scrollY > 300) {
        backToTopButton.classList.remove('opacity-0', 'invisible')
        backToTopButton.classList.add('opacity-100', 'visible')
      } else {
        backToTopButton.classList.add('opacity-0', 'invisible')
        backToTopButton.classList.remove('opacity-100', 'visible')
      }
    }
  }

  const scrollToTop = () => {
    window.scrollTo({
      top: 0,
      behavior: 'smooth',
    })
  }

  if (backToTopButton) {
    backToTopButton.addEventListener('click', scrollToTop)
  }

  window.addEventListener('scroll', handleScroll)

  // 清理事件监听器
  onUnmounted(() => {
    if (backToTopButton) {
      backToTopButton.removeEventListener('click', scrollToTop)
    }
    window.removeEventListener('scroll', handleScroll)
  })
})
</script>

<style scoped>
.bg-dark {
  background-color: #1d2129;
}
.text-primary {
  color: #165dff;
}
</style>

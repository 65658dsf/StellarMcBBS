<template>
  <section id="contact" class="py-16 bg-light-1">
    <div class="container mx-auto px-4">
      <div class="max-w-4xl mx-auto">
        <div class="text-center mb-12">
          <h2 class="text-[clamp(1.5rem,3vw,2.5rem)] font-bold text-dark mb-4">联系我们</h2>
          <p class="text-dark-2 max-w-2xl mx-auto">
            加入恒星MC社区交流群，与更多玩家一起交流游戏心得，获取最新服务器资讯
          </p>
        </div>

        <div class="grid md:grid-cols-3 gap-8">
          <!-- 交流群 -->
          <div class="bg-white rounded-xl p-8 text-center shadow-sm hover:shadow-md transition-shadow">
            <div class="w-16 h-16 rounded-full bg-primary/10 flex items-center justify-center mx-auto mb-4">
              <i class="fa fa-users text-primary text-2xl"></i>
            </div>
            <h3 class="text-lg font-semibold text-dark mb-2">官方QQ群</h3>
            <p class="text-dark-2 text-sm mb-4">加入我们的官方QQ群，与更多玩家交流</p>
            <button
              @click="copyToClipboard('123456789')"
              class="px-6 py-2 bg-primary hover:bg-primary/90 text-white rounded-lg transition-colors text-sm"
            >
              复制群号
            </button>
          </div>

          <!-- Discord -->
          <div class="bg-white rounded-xl p-8 text-center shadow-sm hover:shadow-md transition-shadow">
            <div class="w-16 h-16 rounded-full bg-accent/10 flex items-center justify-center mx-auto mb-4">
              <i class="fa fa-comments text-accent text-2xl"></i>
            </div>
            <h3 class="text-lg font-semibold text-dark mb-2">Discord频道</h3>
            <p class="text-dark-2 text-sm mb-4">加入我们的Discord频道，实时交流</p>
            <a
              href="https://discord.gg/starmc"
              target="_blank"
              class="px-6 py-2 bg-accent hover:bg-accent/90 text-white rounded-lg transition-colors text-sm"
            >
              加入Discord
            </a>
          </div>

          <!-- 邮箱 -->
          <div class="bg-white rounded-xl p-8 text-center shadow-sm hover:shadow-md transition-shadow">
            <div class="w-16 h-16 rounded-full bg-success/10 flex items-center justify-center mx-auto mb-4">
              <i class="fa fa-envelope text-success text-2xl"></i>
            </div>
            <h3 class="text-lg font-semibold text-dark mb-2">联系邮箱</h3>
            <p class="text-dark-2 text-sm mb-4">有问题随时发邮件联系我们</p>
            <button
              @click="copyToClipboard('admin@starmc.com')"
              class="px-6 py-2 bg-success hover:bg-success/90 text-white rounded-lg transition-colors text-sm"
            >
              复制邮箱
            </button>
          </div>
        </div>

        <!-- 社交媒体 -->
        <div class="mt-12 bg-white rounded-xl p-8">
          <h3 class="text-xl font-semibold text-dark text-center mb-6">关注我们</h3>
          <div class="flex justify-center gap-6">
            <a
              href="#"
              class="w-12 h-12 rounded-full bg-primary/10 flex items-center justify-center text-primary hover:bg-primary hover:text-white transition-colors"
            >
              <i class="fa fa-weibo text-xl"></i>
            </a>
            <a
              href="#"
              class="w-12 h-12 rounded-full bg-success/10 flex items-center justify-center text-success hover:bg-success hover:text-white transition-colors"
            >
              <i class="fa fa-wechat text-xl"></i>
            </a>
            <a
              href="#"
              class="w-12 h-12 rounded-full bg-dark/10 flex items-center justify-center text-dark hover:bg-dark hover:text-white transition-colors"
            >
              <i class="fa fa-github text-xl"></i>
            </a>
            <a
              href="#"
              class="w-12 h-12 rounded-full bg-danger/10 flex items-center justify-center text-danger hover:bg-danger hover:text-white transition-colors"
            >
              <i class="fa fa-youtube text-xl"></i>
            </a>
          </div>
        </div>

        <!-- 常见问题 -->
        <div class="mt-12 bg-white rounded-xl p-8">
          <h3 class="text-xl font-semibold text-dark mb-6">常见问题</h3>
          <div class="space-y-4">
            <div class="border-b border-light-2 pb-4">
              <h4 class="font-medium text-dark mb-2">如何加入服务器？</h4>
              <p class="text-dark-2 text-sm">在服务器列表中找到感兴趣的服务器，复制服务器地址，在Minecraft多人游戏中添加即可。</p>
            </div>
            <div class="border-b border-light-2 pb-4">
              <h4 class="font-medium text-dark mb-2">服务器是否收费？</h4>
              <p class="text-dark-2 text-sm">恒星MC社区推荐的服务器均为免费加入，部分服务器可能有VIP服务，但不影响正常游戏。</p>
            </div>
            <div class="border-b border-light-2 pb-4">
              <h4 class="font-medium text-dark mb-2">如何举报违规服务器？</h4>
              <p class="text-dark-2 text-sm">请联系管理员邮箱admin@starmc.com，提供服务器名称和违规证据，我们会及时处理。</p>
            </div>
            <div>
              <h4 class="font-medium text-dark mb-2">如何让自己的服务器入驻？</h4>
              <p class="text-dark-2 text-sm">在服务器入驻页面填写申请信息，我们会在1-3个工作日内完成审核。</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const copiedText = ref('')

const copyToClipboard = async (text: string) => {
  try {
    await navigator.clipboard.writeText(text)
    copiedText.value = text
    
    // 2秒后重置提示
    setTimeout(() => {
      copiedText.value = ''
    }, 2000)
  } catch (err) {
    console.error('复制失败:', err)
  }
}
</script>

<style scoped>
.text-dark {
  color: #1D2129;
}
.text-dark-2 {
  color: #4E5969;
}
.bg-light-1 {
  background-color: #F2F3F5;
}
.bg-light-2 {
  background-color: #E5E6EB;
}
.text-primary {
  color: #165DFF;
}
.text-accent {
  color: #FF7D00;
}
.text-success {
  color: #00B42A;
}
</style>
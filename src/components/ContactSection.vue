<template>
  <section id="contact" class="py-16 bg-light-1">
    <div class="max-w-7xl mx-auto px-4">
      <div class="max-w-6xl mx-auto">
        <div class="text-center mb-12">
          <h2 class="text-[clamp(1.5rem,3vw,2.5rem)] font-bold text-dark mb-4">联系我们</h2>
          <p class="text-dark-2 max-w-2xl mx-auto">
            加入恒星MC社区交流群，与更多玩家一起交流游戏心得，获取最新服务器资讯
          </p>
        </div>

        <div class="grid md:grid-cols-2 gap-8">
          <!-- 交流群 -->
          <div
            class="bg-white rounded-xl p-8 text-center shadow-sm hover:shadow-md transition-shadow"
          >
            <div
              class="w-16 h-16 rounded-full bg-primary/10 flex items-center justify-center mx-auto mb-4"
            >
              <img src="@/assets/QQ.svg" alt="QQ群" class="w-8 h-8" />
            </div>
            <h3 class="text-lg font-semibold text-dark mb-2">官方QQ群</h3>
            <p class="text-dark-2 text-sm mb-4">加入我们的官方QQ群，与更多玩家交流</p>
            <a
              href="https://qm.qq.com/q/o5vx2WPe24"
              target="_blank"
              class="px-6 py-2 bg-primary hover:bg-primary/90 text-white rounded-lg transition-colors text-sm inline-block"
            >
              加入交流群
            </a>
          </div>

          <!-- 哔哩哔哩 -->
          <div
            class="bg-white rounded-xl p-8 text-center shadow-sm hover:shadow-md transition-shadow"
          >
            <div
              class="w-16 h-16 rounded-full bg-danger/10 flex items-center justify-center mx-auto mb-4"
            >
              <img src="@/assets/bilibili.svg" alt="哔哩哔哩" class="w-8 h-8" />
            </div>
            <h3 class="text-lg font-semibold text-dark mb-2">哔哩哔哩</h3>
            <p class="text-dark-2 text-sm mb-4">关注我们的哔哩哔哩账号，获取最新动态</p>
            <a
              href="https://space.bilibili.com/500351788"
              target="_blank"
              class="px-6 py-2 bg-danger hover:bg-danger/90 text-white rounded-lg transition-colors text-sm"
            >
              立即关注
            </a>
          </div>
        </div>

        <!-- 常见问题 -->
        <div class="mt-12 bg-white rounded-xl p-8">
          <h3 class="text-xl font-semibold text-dark mb-6">常见问题</h3>
          <div class="space-y-4">
            <div class="border-b border-light-2 pb-4">
              <h4 class="font-medium text-dark mb-2">如何加入服务器？</h4>
              <p class="text-dark-2 text-sm">
                在服务器列表中找到感兴趣的服务器，复制服务器地址，在Minecraft多人游戏中添加即可。
              </p>
            </div>
            <div class="border-b border-light-2 pb-4">
              <h4 class="font-medium text-dark mb-2">服务器是否收费？</h4>
              <p class="text-dark-2 text-sm">
                恒星MC社区推荐的服务器均为免费加入，部分服务器可能有VIP服务，但不影响正常游戏。
              </p>
            </div>
            <div class="border-b border-light-2 pb-4">
              <h4 class="font-medium text-dark mb-2">如何举报违规服务器？</h4>
              <p class="text-dark-2 text-sm">
                请加入官方QQ群联系管理员，提供服务器名称和违规证据，我们会及时处理。
              </p>
            </div>
            <div class="border-b border-light-2 pb-4">
              <h4 class="font-medium text-dark mb-2">如何让自己的服务器入驻？</h4>
              <p class="text-dark-2 text-sm">
                在服务器入驻页面填写申请信息，系统会自动跳转到GitHub Issues页面完成提交。
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.text-dark {
  color: #1d2129;
}
.text-dark-2 {
  color: #4e5969;
}
.bg-light-1 {
  background-color: #f2f3f5;
}
.bg-light-2 {
  background-color: #e5e6eb;
}
.text-primary {
  color: #165dff;
}
.text-accent {
  color: #ff7d00;
}
.text-success {
  color: #00b42a;
}
</style>

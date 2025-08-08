<template>
  <section id="stats" class="py-16 bg-white">
    <div class="container mx-auto px-4">
      <div class="text-center mb-12">
        <h2 class="text-[clamp(1.5rem,3vw,2.5rem)] font-bold text-dark mb-4">社区数据统计</h2>
        <p class="text-dark-2 max-w-2xl mx-auto">
          实时展示恒星MC社区的服务器和玩家数据，见证社区的成长与活力
        </p>
      </div>

      <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
        <!-- 总服务器数 -->
        <div
          class="bg-light-1 rounded-xl p-6 shadow-sm hover:shadow-md transition-shadow transform hover:-translate-y-1 duration-300"
        >
          <div class="flex items-center justify-between mb-4">
            <h3 class="text-lg font-semibold text-dark-2">总服务器数</h3>
            <div
              class="w-10 h-10 rounded-full bg-primary/10 flex items-center justify-center text-primary"
            >
              <i class="fa fa-server"></i>
            </div>
          </div>
          <div class="flex items-end">
            <span class="text-4xl font-bold text-dark">{{ totalServers }}</span>
            <span class="text-success ml-2 flex items-center text-sm">
              <i class="fa fa-arrow-up mr-1"></i>{{ serverGrowth }}%
            </span>
          </div>
          <p class="text-dark-2/80 text-sm mt-2">较上月增长</p>
        </div>

        <!-- 在线服务器 -->
        <div
          class="bg-light-1 rounded-xl p-6 shadow-sm hover:shadow-md transition-shadow transform hover:-translate-y-1 duration-300"
        >
          <div class="flex items-center justify-between mb-4">
            <h3 class="text-lg font-semibold text-dark-2">在线服务器</h3>
            <div
              class="w-10 h-10 rounded-full bg-success/10 flex items-center justify-center text-success"
            >
              <i class="fa fa-check-circle"></i>
            </div>
          </div>
          <div class="flex items-end">
            <span class="text-4xl font-bold text-dark">{{ onlineServers }}</span>
            <span class="text-dark-2 ml-2 text-sm"> 占比{{ onlinePercentage }}% </span>
          </div>
          <p class="text-dark-2/80 text-sm mt-2">当前在线状态</p>
        </div>

        <!-- 总在线人数 -->
        <div
          class="bg-light-1 rounded-xl p-6 shadow-sm hover:shadow-md transition-shadow transform hover:-translate-y-1 duration-300"
        >
          <div class="flex items-center justify-between mb-4">
            <h3 class="text-lg font-semibold text-dark-2">总在线人数</h3>
            <div
              class="w-10 h-10 rounded-full bg-accent/10 flex items-center justify-center text-accent"
            >
              <i class="fa fa-users"></i>
            </div>
          </div>
          <div class="flex items-end">
            <span class="text-4xl font-bold text-dark">{{ totalPlayers }}</span>
            <span class="text-success ml-2 flex items-center text-sm">
              <i class="fa fa-arrow-up mr-1"></i>{{ playerGrowth }}%
            </span>
          </div>
          <p class="text-dark-2/80 text-sm mt-2">较昨日增长</p>
        </div>
      </div>

      <!-- 活跃度图表 -->
      <div class="mt-12 bg-light-1 rounded-xl p-6 shadow-sm">
        <h3 class="text-lg font-semibold text-dark-2 mb-6">社区活跃度趋势</h3>
        <div class="h-64">
          <canvas ref="chartCanvas"></canvas>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref, onMounted, nextTick } from 'vue'

const totalServers = ref(24)
const serverGrowth = ref(12)
const onlineServers = ref(18)
const onlinePercentage = ref(75)
const totalPlayers = ref(1254)
const playerGrowth = ref(8)

const chartCanvas = ref<HTMLCanvasElement>()

onMounted(async () => {
  await nextTick()
  
  if (chartCanvas.value) {
    const ctx = chartCanvas.value.getContext('2d')
    if (ctx) {
      // 创建简单的图表
      const canvas = chartCanvas.value
      const width = canvas.width
      const height = canvas.height
      
      // 清除画布
      ctx.clearRect(0, 0, width, height)
      
      // 设置样式
      ctx.strokeStyle = '#165DFF'
      ctx.lineWidth = 2
      
      // 绘制简单的线图
      ctx.beginPath()
      const points = [
        { x: 40, y: height - 60 },
        { x: 80, y: height - 80 },
        { x: 120, y: height - 100 },
        { x: 160, y: height - 120 },
        { x: 200, y: height - 90 },
        { x: 240, y: height - 70 },
        { x: 280, y: height - 110 },
        { x: 320, y: height - 130 },
        { x: 360, y: height - 100 },
        { x: 400, y: height - 80 }
      ]
      
      ctx.moveTo(points[0].x, points[0].y)
      points.forEach(point => {
        ctx.lineTo(point.x, point.y)
      })
      ctx.stroke()
      
      // 添加渐变填充
      ctx.beginPath()
      ctx.moveTo(points[0].x, points[0].y)
      points.forEach(point => {
        ctx.lineTo(point.x, point.y)
      })
      ctx.lineTo(points[points.length - 1].x, height - 40)
      ctx.lineTo(points[0].x, height - 40)
      ctx.closePath()
      
      const gradient = ctx.createLinearGradient(0, 0, 0, height)
      gradient.addColorStop(0, 'rgba(22, 93, 255, 0.3)')
      gradient.addColorStop(1, 'rgba(22, 93, 255, 0.05)')
      ctx.fillStyle = gradient
      ctx.fill()
    }
  }
})
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
.text-success {
  color: #00B42A;
}
.text-accent {
  color: #FF7D00;
}
</style>
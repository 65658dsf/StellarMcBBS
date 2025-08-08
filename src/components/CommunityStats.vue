<template>
  <section id="stats" class="py-16 bg-white">
    <div class="max-w-7xl mx-auto px-4">
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
            <span id="total-servers-value" class="text-4xl font-bold text-dark">{{
              totalServers
            }}</span>
          </div>
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
            <span id="online-servers-value" class="text-4xl font-bold text-dark">{{
              onlineServers
            }}</span>
          </div>
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
            <span id="total-players-value" class="text-4xl font-bold text-dark">{{
              totalPlayers
            }}</span>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref, onMounted, nextTick, computed } from 'vue'

interface Server {
  id: number
  name: string
  address: string
  online: boolean
  players: number
  maxPlayers: number
  version: string
  type: string
  description: string
  category: string
  ping?: number
}

const props = defineProps<{
  servers: Server[]
}>()

const totalServers = computed(() => props.servers.length)
const onlineServers = computed(() => props.servers.filter(server => server.online).length)
const totalPlayers = computed(() => props.servers.reduce((sum, server) => sum + server.players, 0))

// 数字动画效果
const animateValue = (targetValue: number, duration: number) => {
  let startTimestamp: number | null = null
  const step = (timestamp: number) => {
    if (!startTimestamp) startTimestamp = timestamp
    const progress = Math.min((timestamp - startTimestamp) / duration, 1)

    const value = Math.floor(progress * targetValue)
    return value.toLocaleString()
  }
  return step
}

// 监听元素是否进入视口
const setupIntersectionObserver = () => {
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          const targetId = entry.target.id
          let startTimestamp: number | null = null

          const animateStep = (timestamp: number) => {
            if (!startTimestamp) startTimestamp = timestamp
            const progress = Math.min((timestamp - startTimestamp) / 2000, 1)

            let targetValue = 0
            let element: HTMLElement | null = null

            if (targetId === 'total-servers-value') {
              targetValue = totalServers.value
              element = entry.target as HTMLElement
            } else if (targetId === 'online-servers-value') {
              targetValue = onlineServers.value
              element = entry.target as HTMLElement
            } else if (targetId === 'total-players-value') {
              targetValue = totalPlayers.value
              element = entry.target as HTMLElement
            }

            if (element) {
              const value = Math.floor(progress * targetValue)
              element.textContent = value.toLocaleString()
            }

            if (progress < 1) {
              window.requestAnimationFrame(animateStep)
            } else {
              if (element) {
                element.textContent = targetValue.toLocaleString()
              }
            }
          }

          window.requestAnimationFrame(animateStep)
          observer.unobserve(entry.target)
        }
      })
    },
    { threshold: 0.5 },
  )

  // 观察统计数字元素
  document
    .querySelectorAll('#total-servers-value, #online-servers-value, #total-players-value')
    .forEach((el) => {
      observer.observe(el)
    })
}

onMounted(async () => {
  await nextTick()

  // 设置数字动画的IntersectionObserver
  setupIntersectionObserver()
})
</script>

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
.text-success {
  color: #00b42a;
}
.text-accent {
  color: #ff7d00;
}
</style>

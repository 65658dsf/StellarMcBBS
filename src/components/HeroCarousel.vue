<template>
  <section class="relative h-screen overflow-hidden">
    <div id="carousel" class="h-full">
      <!-- 轮播项 -->
      <div
        v-for="(slide, index) in slides"
        :key="index"
        :class="[
          'carousel-item absolute inset-0 transition-opacity duration-1000',
          currentSlide === index ? 'opacity-100' : 'opacity-0',
        ]"
      >
        <div class="absolute inset-0 bg-gradient-to-b from-black/40 to-black/70 z-10"></div>
        <img :src="slide.image" :alt="slide.alt" class="w-full h-full object-cover" />
        <div class="absolute inset-0 z-20 flex items-center justify-center text-center px-4">
          <div
            :class="[
              'max-w-3xl',
              index === 0 ? 'transform transition-transform duration-1000' : '',
            ]"
          >
            <h1 class="text-[clamp(2rem,5vw,4rem)] font-bold text-white mb-6 text-shadow-lg">
              {{ slide.title }}
            </h1>
            <p
              class="text-[clamp(1rem,2vw,1.25rem)] text-white/90 mb-8 text-shadow max-w-2xl mx-auto"
            >
              {{ slide.description }}
            </p>
            <div class="flex flex-col sm:flex-row justify-center gap-4">
              <a
                :href="slide.primaryButton.href"
                :class="[
                  'px-8 py-3 font-medium rounded-lg transition-all transform hover:scale-105 shadow-lg',
                  slide.primaryButton.class,
                ]"
              >
                <i :class="slide.primaryButton.icon"></i>{{ slide.primaryButton.text }}
              </a>
              <a
                :href="slide.secondaryButton.href"
                class="px-8 py-3 bg-transparent hover:bg-white/10 text-white font-medium rounded-lg border border-white transition-all transform hover:scale-105"
              >
                <i :class="slide.secondaryButton.icon"></i>{{ slide.secondaryButton.text }}
              </a>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- 轮播控制 -->
    <div class="absolute bottom-8 left-0 right-0 z-30 flex justify-center space-x-3">
      <button
        v-for="(dot, index) in slides"
        :key="index"
        @click="goToSlide(index)"
        :class="[
          'w-3 h-3 rounded-full bg-white transition-all',
          currentSlide === index ? 'opacity-100' : 'opacity-50',
        ]"
      ></button>
    </div>

    <!-- 下滑提示 -->
    <div
      class="absolute bottom-10 left-1/2 transform -translate-x-1/2 z-30 animate-bounce hidden md:block"
    >
      <a href="#stats" class="text-white/80 hover:text-white">
        <i class="fa fa-angle-down text-3xl"></i>
      </a>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

const currentSlide = ref(0)
const slides = [
  {
    image: '/bg1.jpg',
    alt: '我的世界服务器风景',
    title: '恒星MC社区',
    description: '汇聚优质Minecraft服务器，打造友好的我的世界玩家社区',
    primaryButton: {
      href: '#contact',
      class: 'bg-accent hover:bg-accent/90 text-white',
      icon: 'fa fa-comments-o mr-2',
      text: '加入交流群',
    },
    secondaryButton: {
      href: '#apply',
      icon: 'fa fa-server mr-2',
      text: '服务器入驻',
    },
  },
  {
    image: '/bg2.jpg',
    alt: '我的世界游戏截图',
    title: '发现精彩服务器',
    description: '从生存到创造，从迷你游戏到大型RPG，找到适合你的服务器',
    primaryButton: {
      href: '#servers',
      class: 'bg-primary hover:bg-primary/90 text-white',
      icon: 'fa fa-search mr-2',
      text: '浏览服务器',
    },
    secondaryButton: {
      href: '#stats',
      icon: 'fa fa-bar-chart-o mr-2',
      text: '查看社区数据',
    },
  },
  {
    image: '/bg3.png',
    alt: '我的世界建筑展示',
    title: '探索无限可能',
    description: '在恒星MC社区，每个玩家都能创造属于自己的精彩世界',
    primaryButton: {
      href: '#servers',
      class: 'bg-success hover:bg-success/90 text-white',
      icon: 'fa fa-rocket mr-2',
      text: '立即探索',
    },
    secondaryButton: {
      href: '#about',
      icon: 'fa fa-info-circle mr-2',
      text: '了解更多',
    },
  },
]

const goToSlide = (index: number) => {
  currentSlide.value = index
}

const nextSlide = () => {
  currentSlide.value = (currentSlide.value + 1) % slides.length
}

let intervalId: number

onMounted(() => {
  intervalId = window.setInterval(nextSlide, 5000) as number
})

onUnmounted(() => {
  if (intervalId) {
    clearInterval(intervalId)
  }
})
</script>

<style scoped>
.text-shadow {
  text-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
}
.text-shadow-lg {
  text-shadow: 0 4px 8px rgba(0, 0, 0, 0.5);
}
</style>

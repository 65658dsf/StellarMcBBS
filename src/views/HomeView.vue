<script setup lang="ts">
import { ref, provide } from 'vue'
import AppNavbar from '@/components/AppNavbar.vue'
import HeroCarousel from '@/components/HeroCarousel.vue'
import CommunityStats from '@/components/CommunityStats.vue'
import ServerList from '@/components/ServerList.vue'
import ServerApply from '@/components/ServerApply.vue'
import ContactSection from '@/components/ContactSection.vue'
import Footer from '@/components/Footer.vue'

interface Server {
  id: number
  name: string
  address: string
  icon: string
  logo?: string
  online: boolean
  players: number
  maxPlayers: number
  version: string
  type: string
  description: string
  category: string
  ping?: number
  city?: string | null
  mod?: string
  motd?: string
}

const servers = ref<Server[]>([])
provide('servers', servers)

const handleServersLoaded = (data: Server[]) => {
  servers.value = data
}
</script>

<template>
  <div class="home">
    <!-- 导航栏 -->
    <AppNavbar />

    <!-- 轮播Banner -->
    <HeroCarousel />

    <!-- 统计卡片组 -->
    <CommunityStats :servers="servers" />

    <!-- 服务器列表 -->
    <ServerList @servers-loaded="handleServersLoaded" />

    <!-- 服务器入驻 -->
    <ServerApply />

    <!-- 联系我们 -->
    <ContactSection />

    <!-- 页脚 -->
    <Footer />
  </div>
</template>

<style scoped>
.home {
  min-height: 100vh;
}
</style>

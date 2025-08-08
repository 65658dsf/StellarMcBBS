<script setup lang="ts">
import { ref, provide } from 'vue'
import AppNavbar from '@/components/AppNavbar.vue'
import HeroCarousel from '@/components/HeroCarousel.vue'
import CommunityStats from '@/components/CommunityStats.vue'
import ServerList from '@/components/ServerList.vue'
import ServerApply from '@/components/ServerApply.vue'
import ContactSection from '@/components/ContactSection.vue'
import Footer from '@/components/Footer.vue'

const servers = ref([])
provide('servers', servers)
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
    <ServerList @servers-loaded="(data) => servers.value = data" />

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

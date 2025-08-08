<script setup lang="ts">
import AppNavbar from '@/components/AppNavbar.vue'
import HeroCarousel from '@/components/HeroCarousel.vue'
import CommunityStats from '@/components/CommunityStats.vue'
import ServerList from '@/components/ServerList.vue'
import ServerApply from '@/components/ServerApply.vue'
import ContactSection from '@/components/ContactSection.vue'
</script>

<template>
  <div class="home">
    <!-- 导航栏 -->
    <AppNavbar />

    <!-- 轮播Banner -->
    <HeroCarousel />

    <!-- 统计卡片组 -->
    <CommunityStats />

    <!-- 服务器列表 -->
    <ServerList />

    <!-- 服务器入驻 -->
    <ServerApply />

    <!-- 联系我们 -->
    <ContactSection />
  </div>
</template>

<style scoped>
.home {
  min-height: 100vh;
}
</style>

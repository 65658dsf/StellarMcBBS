<template>
  <section id="servers" class="py-16 bg-light-1">
    <div class="container mx-auto px-4">
      <div class="text-center mb-12">
        <h2 class="text-[clamp(1.5rem,3vw,2.5rem)] font-bold text-dark mb-4">推荐服务器</h2>
        <p class="text-dark-2 max-w-2xl mx-auto">精选优质Minecraft服务器，总有一款适合你</p>
      </div>

      <!-- 筛选工具栏 -->
      <div class="flex flex-col sm:flex-row justify-between items-center mb-8 gap-4">
        <div class="flex flex-wrap gap-2">
          <button
            v-for="category in categories"
            :key="category.id"
            @click="selectCategory(category.id)"
            :class="[
              'px-4 py-2 rounded-lg text-sm transition-colors',
              selectedCategory === category.id
                ? 'bg-primary text-white'
                : 'bg-white text-dark-2 hover:bg-light-2',
            ]"
          >
            {{ category.name }}
          </button>
        </div>

        <div class="relative w-full sm:w-auto">
          <input
            v-model="searchQuery"
            type="text"
            placeholder="搜索服务器..."
            class="pl-10 pr-4 py-2 rounded-lg border border-light-2 focus:outline-none focus:ring-2 focus:ring-primary/50 w-full sm:w-64"
          />
          <i
            class="fa fa-search absolute left-3 top-1/2 transform -translate-y-1/2 text-dark-2"
          ></i>
        </div>
      </div>

      <!-- 服务器卡片网格 -->
      <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6">
        <div
          v-for="server in filteredServers"
          :key="server.id"
          class="bg-white rounded-xl overflow-hidden shadow-sm hover:shadow-md transition-all duration-300 transform hover:-translate-y-1"
        >
          <div class="p-5">
            <div class="flex items-start gap-4">
              <img
                :src="server.icon"
                :alt="server.name + '服务器图标'"
                class="w-16 h-16 rounded-lg object-cover border border-light-2"
              />
              <div class="flex-1">
                <h3 class="font-bold text-lg mb-1">{{ server.name }}</h3>
                <p class="text-dark-2 text-sm mb-2 flex items-center">
                  <i class="fa fa-map-marker mr-1"></i> {{ server.address }}
                </p>
                <div class="flex items-center gap-2">
                  <span
                    :class="[
                      'inline-flex items-center px-2.5 py-0.5 rounded-full text-xs font-medium',
                      server.online ? 'bg-success/10 text-success' : 'bg-danger/10 text-danger',
                    ]"
                  >
                    <i
                      :class="['mr-1', server.online ? 'fa fa-check-circle' : 'fa fa-times-circle']"
                    ></i>
                    {{ server.online ? '在线' : '离线' }}
                  </span>
                  <span class="text-sm text-dark-2"
                    >{{ server.players }}/{{ server.maxPlayers }} 玩家</span
                  >
                </div>
              </div>
            </div>

            <div class="mt-4 pt-4 border-t border-light-2">
              <div class="flex justify-between text-sm mb-3">
                <span class="text-dark-2"
                  >版本: <span class="text-dark">{{ server.version }}</span></span
                >
                <span class="text-dark-2"
                  >类型: <span class="text-dark">{{ server.type }}</span></span
                >
              </div>
              <p class="text-dark-2 text-sm line-clamp-2">
                {{ server.description }}
              </p>
              <button
                class="mt-4 w-full py-2 border border-primary text-primary hover:bg-primary hover:text-white rounded-lg transition-colors text-sm font-medium"
              >
                查看详情
              </button>
            </div>
          </div>
        </div>
      </div>

      <!-- 空状态 -->
      <div v-if="filteredServers.length === 0" class="text-center py-12">
        <i class="fa fa-server text-4xl text-dark-2 mb-4"></i>
        <p class="text-dark-2">没有找到符合条件的服务器</p>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue'

interface Server {
  id: number
  name: string
  address: string
  icon: string
  online: boolean
  players: number
  maxPlayers: number
  version: string
  type: string
  description: string
  category: string
}

const categories = [
  { id: 'all', name: '全部服务器' },
  { id: 'survival', name: '生存' },
  { id: 'creative', name: '创造' },
  { id: 'rpg', name: 'RPG' },
  { id: 'minigames', name: '迷你游戏' },
]

const selectedCategory = ref('all')
const searchQuery = ref('')

const servers = ref<Server[]>([
  {
    id: 1,
    name: '恒星主城',
    address: 'mc.starmc.com',
    icon: 'https://picsum.photos/id/237/80/80',
    online: true,
    players: 128,
    maxPlayers: 200,
    version: '1.20.1',
    type: '生存/创造',
    description: '官方主城服务器，包含生存、创造和小游戏模式，适合各类玩家体验。',
    category: 'survival',
  },
  {
    id: 2,
    name: '幻想RPG',
    address: 'rpg.fantasy-mc.com',
    icon: 'https://picsum.photos/id/239/80/80',
    online: true,
    players: 87,
    maxPlayers: 150,
    version: '1.19.2',
    type: 'RPG/冒险',
    description: '大型角色扮演服务器，丰富的剧情任务和职业系统，沉浸式游戏体验。',
    category: 'rpg',
  },
  {
    id: 3,
    name: '像素创造',
    address: 'build.pixelmc.net',
    icon: 'https://picsum.photos/id/240/80/80',
    online: true,
    players: 45,
    maxPlayers: 100,
    version: '1.20.1',
    type: '创造/建筑',
    description: '专注于建筑创造的服务器，拥有多种建筑工具和材质包，展示你的创意。',
    category: 'creative',
  },
  {
    id: 4,
    name: '极限生存',
    address: 'survival.extrememc.com',
    icon: 'https://picsum.photos/id/241/80/80',
    online: false,
    players: 0,
    maxPlayers: 80,
    version: '1.20.1',
    type: '生存',
    description: '高难度生存服务器，挑战你的生存技能，适合寻求刺激的玩家。',
    category: 'survival',
  },
  {
    id: 5,
    name: '迷你游戏中心',
    address: 'minigames.mcfun.net',
    icon: 'https://picsum.photos/id/242/80/80',
    online: true,
    players: 67,
    maxPlayers: 120,
    version: '1.19.4',
    type: '迷你游戏',
    description: '多种迷你游戏集合，包括起床战争、空岛战争等，与好友一起畅玩。',
    category: 'minigames',
  },
  {
    id: 6,
    name: '魔法世界',
    address: 'magic.magicalmc.com',
    icon: 'https://picsum.photos/id/243/80/80',
    online: true,
    players: 92,
    maxPlayers: 150,
    version: '1.19.2',
    type: 'RPG/魔法',
    description: '魔法主题RPG服务器，学习魔法技能，探索神秘世界，体验不一样的冒险。',
    category: 'rpg',
  },
])

const selectCategory = (categoryId: string) => {
  selectedCategory.value = categoryId
}

const filteredServers = computed(() => {
  let result = servers.value

  if (selectedCategory.value !== 'all') {
    result = result.filter((server) => server.category === selectedCategory.value)
  }

  if (searchQuery.value) {
    const query = searchQuery.value.toLowerCase()
    result = result.filter(
      (server) =>
        server.name.toLowerCase().includes(query) ||
        server.description.toLowerCase().includes(query) ||
        server.type.toLowerCase().includes(query),
    )
  }

  return result
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
.bg-light-2 {
  background-color: #e5e6eb;
}
.text-success {
  color: #00b42a;
}
.text-danger {
  color: #f53f3f;
}
.line-clamp-2 {
  display: -webkit-box;
  -webkit-line-clamp: 2;
  line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}
</style>

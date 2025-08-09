<template>
  <section id="servers" class="py-16 bg-light-1">
    <div class="max-w-7xl mx-auto px-4">
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
      <div class="flex flex-wrap gap-6 justify-start items-start">
        <div
          v-for="server in filteredServers"
          :key="server.id"
          class="bg-white rounded-xl overflow-hidden shadow-sm hover:shadow-md transition-all duration-300 transform hover:-translate-y-1 min-w-[320px] max-w-md flex-shrink-0"
        >
          <div class="p-5">
            <div class="flex items-start gap-4 min-w-0">
              <img
                :src="getServerIcon(server)"
                :alt="server.name + '服务器图标'"
                @error="handleImageError($event)"
                class="w-16 h-16 rounded-lg object-cover border border-light-2 flex-shrink-0"
              />
              <div class="flex-1 min-w-0">
                <h3 class="font-bold text-lg mb-1">{{ server.name }}</h3>
                <p class="text-dark-2 text-sm mb-2 flex items-center break-all">
                  <i class="fa fa-map-marker mr-1 flex-shrink-0"></i>
                  <span class="whitespace-normal">{{ server.address }}</span>
                </p>
                <div class="flex items-center gap-2 flex-wrap">
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
                    >{{ server.players }}/{{ server.maxPlayers }}人</span
                  >
                  <span class="text-sm text-dark-2 flex items-center">
                    <i class="fa fa-wifi mr-1"></i> {{ server.ping ? server.ping + 'ms' : '超时' }}
                  </span>
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
                {{ server.apiMotd }}
              </p>
              <button
                @click="toggleDetails(server.id)"
                class="mt-4 w-full py-2 border border-primary text-primary hover:bg-primary hover:text-white rounded-lg transition-colors text-sm font-medium"
              >
                {{ expandedCards.has(server.id) ? '收起详情' : '查看详情' }}
              </button>
            </div>
          </div>

          <!-- 展开的详情区域 -->
          <div
            v-if="expandedCards.has(server.id)"
            class="px-5 pb-5 border-t border-light-2 animate-expand"
          >
            <div class="pt-4">
              <h4 class="font-medium text-dark mb-2">服务器详情</h4>
              <p class="text-dark-2 text-sm whitespace-pre-wrap">
                {{ server.description || server.apiMotd || server.motd }}
              </p>
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
import { ref, computed, onMounted } from 'vue'

const emit = defineEmits(['servers-loaded'])

interface ServerData {
  name: string
  ip: string
  port: number
  description?: string
  type: string
  version: string
  motd?: string
  favicon?: string
  max?: number
}

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
  apiMotd?: string
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

const servers = ref<Server[]>([])
const expandedCards = ref<Set<number>>(new Set())

const selectCategory = (categoryId: string) => {
  selectedCategory.value = categoryId
}

const toggleDetails = (serverId: number) => {
  if (expandedCards.value.has(serverId)) {
    expandedCards.value.delete(serverId)
  } else {
    expandedCards.value.add(serverId)
  }
  // 触发响应式更新
  expandedCards.value = new Set(expandedCards.value)
}

const getServerIcon = (server: Server) => {
  // 优先使用API返回的logo
  if (server.logo && server.logo !== '') {
    return server.logo
  }
  // 其次使用本地favicon
  if (server.icon && server.icon !== '') {
    return server.icon
  }
  // 默认图标
  return '/favicon.ico'
}

const handleImageError = (event: Event) => {
  // 图片加载失败时，回退到默认图标
  const imgElement = event.target as HTMLImageElement
  if (imgElement) {
    imgElement.src = '/favicon.ico'
  }
}

const loadServers = async () => {
  try {
    // 1. 先获取本地JSON的基础信息
    const response = await fetch('/servers.json')
    const localServers = await response.json()

    // 2. 创建服务器数据
    servers.value = localServers.map((server: ServerData, _index: number) => ({
      id: _index + 1,
      name: server.name,
      address: `${server.ip}:${server.port}`,
      icon: server.favicon || '',
      logo: '',
      online: false,
      players: 0,
      maxPlayers: server.max || 100,
      version: server.version,
      type: server.type,
      description: server.description || server.motd || '',
      category:
        server.type === '生存'
          ? 'survival'
          : server.type === '创造'
            ? 'creative'
            : server.type === 'RPG'
              ? 'rpg'
              : server.type === '迷你游戏'
                ? 'minigames'
                : 'survival',
      ping: 0,
      city: null,
      mod: server.type,
      motd: server.motd || server.description,
    }))

    // 3. 使用JS脚本获取实时数据
    setTimeout(() => {
      updateServerDataWithJS()
    }, 1000)

    // 立即通知父组件初始数据已加载
    emit('servers-loaded', servers.value)
  } catch (error) {
    console.error('加载服务器数据失败:', error)
  }
}

const updateServerDataWithJS = async () => {
  try {
    // 并行获取所有服务器数据
    const promises = servers.value.map(async (server) => {
      try {
        const apiUrl = `https://list.mczfw.cn/api/${server.address}`
        const response = await fetch(apiUrl)

        if (response.ok) {
          const data = await response.json()

          // 更新服务器数据 - 有延迟数据就算在线
          const isOnline =
            data.ping !== undefined &&
            data.ping !== null &&
            data.motd !== '（此服务器离线或者服务器不存在）'
          return {
            ...server,
            online: isOnline,
            players: data.p || 0,
            maxPlayers: data.mp || server.maxPlayers,
            ping: data.ping || 0,
            city: data.city || null,
            // 保持原始description不变，将API返回的motd存储在apiMotd字段中
            apiMotd: data.motd || server.motd,
            motd: data.motd || server.motd,
          }
        }
      } catch (error) {
        console.error(`获取服务器 ${server.name} 数据失败:`, error)
      }
      return server
    })

    // 等待所有数据更新完成
    const updatedServers = await Promise.all(promises)
    servers.value = updatedServers

    // 通知父组件数据已更新
    emit('servers-loaded', servers.value)
  } catch (error) {
    console.error('更新服务器数据失败:', error)
  }
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

onMounted(() => {
  loadServers()
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
.animate-expand {
  animation: expand 0.3s ease-out;
}

@keyframes expand {
  from {
    opacity: 0;
    max-height: 0;
    transform: translateY(-10px);
  }
  to {
    opacity: 1;
    max-height: 200px;
    transform: translateY(0);
  }
}
</style>

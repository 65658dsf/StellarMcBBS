# 我的世界社区网站设计文档

## 一、项目概述
目标：打造一个响应式的Minecraft社区展示平台，包含服务器数据展示、入驻申请和交流功能，网站名称：恒星MC社区


## 二、技术选型
1. 前端框架：Vue3 + TypeScript
2. UI组件库：Element Plus
3. 构建工具：Vite
4. HTTP库：Axios
5. 表单验证：Vuelidate
6. 部署方式：腾讯云EO
7. 入驻表单：GitHub Issues
8. 包管理工具：pnpm

## 三、页面结构设计

### 1. 首页布局
```
|----------------------------------|
|           轮播Banner（100vh）    |
|   [加入交流群] [服务器入驻]       |
|----------------------------------|
|  统计卡片组（3列）               |
|   ▢ 总服务器数 | ▢ 在线服务器 | ▢ 总在线人数 |
|----------------------------------|
| 提示文字：下滑查看服务器列表      |
|----------------------------------|
|  服务器卡片网格（响应式布局）     |
| [图标] 服务器名称                |
|  地址: mc.server.com             |
|  在线状态：✅ 人数：100/200      |
|  版本：1.20.1  介绍：...         |
|----------------------------------|
```

### 2. 响应式布局规范
| 屏幕宽度 | 卡片布局 | 字体大小 | 间距 |
|----------|----------|----------|------|
| ≥1200px  | 4列网格  | 16px     | 24px |
| 992-1199px | 3列网格  | 15px     | 20px |
| 768-991px  | 2列网格  | 14px     | 16px |
| <768px   | 1列网格  | 13px     | 12px |

## 四、核心组件设计

### 1. 轮播Banner组件
```vue
<template>
  <el-carousel height="100vh">
    <el-carousel-item v-for="banner in banners" :key="banner.id">
      <div class="banner-content">
        <h1>恒星MC社区</h1>
        <el-button type="primary">加入交流群</el-button>
        <el-button>服务器入驻</el-button>
      </div>
    </el-carousel-item>
  </el-carousel>
</template>

<style scoped>
.banner-content {
  position: absolute;
  top: 40%;
  left: 50%;
  transform: translate(-50%, -50%);
  text-align: center;
}
</style>
```

### 2. 服务器卡片组件
```vue
<template>
  <el-card class="server-card">
    <img :src="iconUrl" class="server-icon" />
    <div class="card-content">
      <h3>{{ name }}</h3>
      <p class="address">{{ address }}</p>
      <div class="status">
        <el-tag :type="statusColor">{{ onlineStatus }}</el-tag>
        <span>在线: {{ onlineCount }}/{{ maxPlayers }}</span>
      </div>
      <div class="meta">
        <span>版本: {{ version }}</span>
      </div>
      <p class="description">{{ description }}</p>
    </div>
  </el-card>
</template>

<script setup lang="ts">
defineProps<{
  iconUrl: string;
  name: string;
  address: string;
  onlineStatus: string;
  onlineCount: number;
  maxPlayers: number;
  version: string;
  description: string;
}>();
</script>

<style scoped>
.server-icon {
  width: 64px;
  height: 64px;
}
.card-content {
  padding-left: 16px;
}
.status {
  margin: 8px 0;
}
.meta {
  font-size: 12px;
  color: #666;
}
</style>
```

## 五、GitHub集成方案

### 1. 服务器入驻表单
- 创建GitHub Issue模板：
```markdown
---
name: 服务器入驻申请
about: 申请将您的服务器添加到恒星MC社区
title: '[入驻] 服务器名称'
labels: server-submission
assignees: ''

---

**服务器名称**:
**服务器地址**:
**版本**:
**在线人数**:
**服务器图标** (图片URL):
**服务器简介**:
```

### 2. 表单提交组件
```vue
<template>
  <el-form @submit.prevent="submitForm">
    <el-form-item label="服务器名称">
      <el-input v-model="form.name" />
    </el-form-item>
    <!-- 其他字段 -->
    <el-button type="primary" native-type="submit">提交入驻申请</el-button>
  </el-form>
</template>

<script setup lang="ts">
const form = ref({
  name: '',
  address: '',
  version: '',
  // ...其他字段
});

const submitForm = async () => {
  const issueBody = generateIssueBody(form.value);
  window.open(`https://github.com/your-org/mc-community/issues/new?title=[入驻] ${form.value.name}&body=${encodeURIComponent(issueBody)}`);
};
</script>
```

## 六、数据管理

### 1. 本地存储结构
```json
// servers.json
[
  {
    "id": 1,
    "name": "主城服务器",
    "address": "mc.main.com",
    "icon": "https://example.com/icons/main.png",
    "online": true,
    "players": "100/200",
    "version": "1.20.1",
    "description": "官方主城服务器，欢迎加入"
  }
]
```

### 2. 数据获取方式
```ts
// services/serverService.ts
export const fetchServers = async (): Promise<Server[]> => {
  const response = await axios.get('/data/servers.json');
  return response.data;
};
```

## 七、响应式实现策略

1. 使用Element Plus的栅格系统
```vue
<el-row :gutter="20">
  <el-col :xs="24" :sm="12" :md="8" :lg="6" :xl="6" v-for="server in servers" :key="server.id">
    <ServerCard :server="server" />
  </el-col>
</el-row>
```

2. 媒体查询补充
```css
@media (max-width: 768px) {
  .server-card {
    flex-direction: column;
    align-items: center;
  }
  .card-content {
    padding-left: 0;
    text-align: center;
  }
}
```

## 八、开发计划

1. 第一阶段：
   - 搭建Vue3+TS项目
   - 实现基础页面框架
   - 完成响应式布局

2. 第二阶段：
   - 开发服务器卡片组件
   - 实现数据加载功能
   - 创建GitHub表单

3. 第三阶段：
   - 添加动画效果
   - 优化移动端体验
   - 部署到GitHub Pages

## 九、扩展建议

1. 后续可添加：
   - 实时在线人数统计
   - 服务器分类筛选
   - 用户登录系统
   - Minecraft API对接

2. 性能优化：
   - 图片懒加载
   - 数据分页加载
   - 使用Intersection Observer实现无限滚动

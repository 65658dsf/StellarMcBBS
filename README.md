# StellarMcBBS - 恒星穿透社区

一个基于Vue 3 + TypeScript + Tailwind CSS构建的Minecraft服务器社区网站。

## 项目结构

```
StellarMcBBS/
├── src/
│   ├── components/          # Vue组件
│   │   ├── AppNavbar.vue    # 导航栏组件
│   │   ├── HeroCarousel.vue # 轮播图组件
│   │   ├── CommunityStats.vue # 社区统计组件
│   │   ├── ServerList.vue   # 服务器列表组件
│   │   ├── ServerApply.vue  # 服务器入驻组件
│   │   └── ContactSection.vue # 联系方式组件
│   ├── views/
│   │   └── HomeView.vue     # 主页视图
│   ├── router/
│   │   └── index.ts         # 路由配置
│   └── App.vue              # 根组件
├── index.html               # 入口HTML文件
└── package.json             # 项目依赖
```

## 技术栈

- **Vue 3** - 渐进式JavaScript框架
- **TypeScript** - 类型安全的JavaScript超集
- **Tailwind CSS** - 实用优先的CSS框架
- **Pinia** - 状态管理
- **Vue Router** - 路由管理
- **ESLint + Prettier** - 代码质量和格式化

## 功能特性

- 🎨 现代化的响应式设计
- 📱 移动端友好的布局
- 🎯 服务器列表展示和筛选
- 📊 社区数据统计图表
- 📝 服务器入驻申请
- 📞 联系方式和社交媒体集成
- 🌟 动画效果和交互体验

## 快速开始

### 安装依赖

```bash
pnpm install
```

### 开发环境

```bash
pnpm dev
```

### 构建生产版本

```bash
pnpm build
```

### 预览生产版本

```bash
pnpm preview
```

### 代码检查

```bash
pnpm lint
```

## 组件说明

### AppNavbar.vue
- 响应式导航栏
- 毛玻璃效果背景
- 移动端汉堡菜单

### HeroCarousel.vue
- 自动轮播展示
- 手动控制按钮
- 平滑过渡动画

### CommunityStats.vue
- 社区数据统计
- 图表可视化
- 实时数据展示

### ServerList.vue
- 服务器列表展示
- 搜索和筛选功能
- 状态标签显示

### ServerApply.vue
- 入驻申请表单
- 表单验证
- 入驻须知说明

### ContactSection.vue
- 联系方式展示
- 社交媒体链接
- 常见问题解答

## 自定义配置

### 颜色主题
在 `index.html` 中可以修改Tailwind配置：

```javascript
tailwind.config = {
  theme: {
    extend: {
      colors: {
        primary: '#165DFF',
        secondary: '#36BFFA',
        accent: '#FF7D00',
        // ...其他颜色
      }
    }
  }
}
```

### 服务器数据
修改 `ServerList.vue` 中的 `servers` 数据数组来更新服务器列表。

### 社区统计
在 `CommunityStats.vue` 中更新统计数据和图表配置。

## 部署

构建完成后，将 `dist` 目录中的文件部署到您的Web服务器即可。

## 开发工具推荐

- **VSCode** - 推荐的代码编辑器
- **Volar** - Vue语言支持插件
- **ESLint** - 代码质量检查
- **Prettier** - 代码格式化

## 许可证

MIT License

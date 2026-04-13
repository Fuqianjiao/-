# 🧊 FridgeMate 冰箱智能管家

> 帮你管理冰箱食材 · 追踪保质期 · 智能推荐菜谱  
> 让每一份食材都不被浪费 ❤️

## 📱 项目简介

一款温馨可爱的微信小程序，解决独居/情侣/家庭用户的日常痛点：

- **冰箱里有什么？** 一目了然的食材清单，分类展示
- **什么时候过期？** 自动追踪保质期，临期/过期提醒
- **今晚吃什么？** 根据现有食材智能匹配菜谱
- **一个人怎么吃？** 支持一人食、两人食、家庭三种场景

## ✨ 核心功能

### 🧊 我的冰箱
- 手动添加 / 条码扫描 / 拍照识别（三种方式录入）
- 7大分类：蔬菜、水果、肉类、乳制品、饮料、调料、其他
- 3个存储位置追踪：冷藏室、冷冻室、门架
- 搜索 + 分类筛选 + 多维度排序

### ⏰ 保质期管理
- 生产日期 → 自动计算过期时间
- 扫码自动匹配品牌保质期（蒙牛、伊利、海天等50+品牌）
- 全网搜索保质期信息
- 临期（3天内）+ 已过期醒目标识
- 微信订阅消息推送提醒（每日9点定时检查）

### 🍳 菜谱推荐引擎
- 内置 **10+ 道经典家常菜谱**（西红柿炒鸡蛋、红烧肉、可乐鸡翅...）
- 支持**对接TheMealDB API**获取全球300+道海外菜谱（免费，无需申请密钥）
- 智能匹配算法：同义词映射（"番茄=西红柿"、"土鸡蛋=鸡蛋"）
- 三种场景模式：
  - 🍱 **一人食** — 快手小份菜优先
  - 💕 **两人食** — 有仪式感的双人餐
  - 👨‍👩‍👧‍👦 **家庭餐** — 营养均衡的大份量
- 匹配度百分比 + 缺料提示 + 一键加入购物清单
- 菜谱详情：步骤指引 + 食材清单 + 营养信息 + 一键清耗

### 🛒 购物清单
- 菜谱缺料一键加入
- 手动添加购物项
- 勾选完成 + 清除已完成

### 👨‍👩‍👧‍👦 冰箱共享
- 邀请家人/室友共享同一冰箱数据
- 邀请码机制（安全便捷）

## 🎨 设计风格

**温馨可爱 (Warm & Cute)**
- 主色调：暖橙粉渐变 `#FF9A8B → #FF6A88`
- 大圆角卡片 + 柔和阴影
- 可爱图标 + 微动效（弹性缩放、呼吸灯）
- 渐变色进度条 + 状态动画

## 🛠️ 技术栈

| 层级 | 技术 | 说明 |
|------|------|------|
| **前端** | 微信小程序 (WXML/WXSS/TypeScript) | 原生开发 |
| **状态管理** | App.globalData + wx.storage | 轻量方案 |
| **UI组件** | 自研组件库 | food-card / recipe-card / scene-switcher 等 |
| **后端** | 微信云开发 | 云函数 + 云数据库 |
| **数据库** | 文档型数据库 (类MongoDB) | 5个核心集合 |
| **定时任务** | 云函数定时触发器 | 每日9:00检查保质期 |
| **消息推送** | 微信订阅消息 | 临期/过期提醒 |

## 📁 项目结构

```
fridge-mate/
├── miniprogram/                    # 小程序前端
│   ├── pages/
│   │   ├── index/                  # 首页（总览+推荐）
│   │   ├── fridge/                 # 冰箱页面（分类列表）
│   │   ├── food-detail/            # 食材详情
│   │   ├── add-food/               # 添加食材（手动/扫码/拍照）
│   │   ├── recipes/                # 菜谱发现
│   │   ├── recipe-detail/          # 菜谱详情+烹饪
│   │   ├── shopping-list/          # 购物清单
│   │   └── profile/                # 个人中心（设置/共享）
│   ├── components/                 # 公共组件
│   │   ├── food-card/              # 食材卡片
│   │   ├── recipe-card/            # 菜谱卡片
│   │   ├── scene-switcher/         # 场景切换器
│   │   └── empty-state/            # 空状态占位
│   ├── utils/                      # 工具函数
│   │   ├── constants.ts            # 常量定义
│   │   ├── date.ts                 # 日期工具
│   │   ├── api.ts                  # 云函数封装
│   │   └── matcher.ts              # 食材-菜谱匹配算法
│   ├── styles/                     # 样式系统
│   │   ├── variables.wxss          # CSS变量（色彩/圆角/阴影/动画）
│   │   ├── app.wxss               # 全局样式
│   │   └── animations.wxss         # 动画库
│   ├── app.ts                      # 应用入口
│   └── app.json                    # 配置文件
├── cloudfunctions/                 # 云函数后端
│   ├── addFoodItem/                # 添加食材
│   ├── scanBarcode/                # 扫码识别
│   ├── getRecipeRecommendations/   # 菜谱推荐引擎 ⭐核心
│   ├── fetchMealDB/               # TheMealDB 海外菜谱 API 代理 ⭐新增
│   ├── consumeIngredients/         # 一键清耗
│   ├── checkExpiry/                # 定时保质期检查
│   ├── searchBrandProduct/         # 全网搜索品牌保质期
│   ├── inviteShare/                # 邀请共享
│   └── acceptInvite/              # 接受邀请
└── database/                       # 初始数据脚本
    └── init_data.js                # 菜谱+品牌数据
```

## 🗄️ 数据库设计

### 5个核心集合

1. **`fridge_items`** - 食材记录
2. **`recipes`** - 菜谱数据
3. **`brand_shelf_life`** - 品牌保质期库（50+品牌）
4. **`user_settings`** - 用户偏好设置
5. **`shopping_list`** - 购物清单
6. **`shared_fridges`** - 冰箱共享组
7. **`cooking_history`** - 做菜历史

详细字段定义见 [规划文档](brain/fridge-mate-plan.md)

## 🚀 快速开始

### 1. 环境准备
```bash
# 1. 安装微信开发者工具
# https://developers.weixin.qq.com/miniprogram/dev/devtools/download.html

# 2. 注册微信小程序账号
# https://mp.weixin.qq.com

# 3. 开通云开发环境
# 在开发者工具中 → 云开发 → 创建环境
```

### 2. 导入项目
```bash
# 用微信开发者工具打开 fridge-mate 目录
# 修改 project.config.json 中的 appid 为你自己的 appid
# 修改 app.ts 中的 envId 为你的云开发环境ID
```

### 3. 安装依赖并构建
```bash
cd fridge-mate/miniprogram
npm install --production
# 在开发者工具中点击「工具 → 构建npm」
```

### 4. 部署云函数
```bash
# 右键每个云函数目录 → 上传并部署（云端安装依赖）
# 需要部署的云函数：
# - addFoodItem
# - scanBarcode
# - getRecipeRecommendations
# - fetchMealDB
# - consumeIngredients
# - checkExpiry (含定时触发器配置)
# - searchBrandProduct
# - inviteShare
# - acceptInvite
```

### 5. 创建数据库集合
在云开发控制台 → 数据库 中创建以下集合：
- `fridge_items`
- `recipes`
- `brand_shelf_life`
- `user_settings`
- `shopping_list`
- `shared_fridges`
- `cooking_history`
- `notifications`

### 6. 配置权限规则
各集合建议的数据库权限设置：
- 所有集合：仅创建者可读写（`auth.openid === _openid`）

## 📋 开发计划

### Phase 1 ✅ MVP（当前完成）
- [x] 项目初始化 + UI框架搭建
- [x] 温馨可爱风格设计系统
- [x] 食材 CRUD + 分类展示
- [x] 保质期手动设置 + 进度条
- [x] 10道内置菜谱 + 匹配算法
- [x] 三种场景切换
- [x] 购物清单功能
- [x] 个人中心基础设置

### Phase 2 🔧 智能化增强（已完成）
- [x] 对接**TheMealDB API**获取全球海外菜谱
- [x] 拍照AI识别食材（OCR/图像识别）
- [ ] 订阅消息推送（需申请模板ID）
- [ ] 更多品牌保质期数据接入
- [ ] 做菜历史统计

### Phase 3 🎯 体验打磨（规划中）
- [ ] 数据看板（消耗分析/浪费统计）
- [ ] 智能购物建议
- [ ] 菜谱UGC（用户投稿）
- [ ] 营养摄入统计
- [ ] 社交分享功能

## 📝 注意事项

1. **AppID 替换**: 使用前务必替换 `project.config.json` 中的 `appid` 和 `app.ts` 中的 `envId`
2. **云函数部署**: 每个云函数都需要右键单独上传部署
3. **订阅消息**: 需要在小程序管理后台申请模板ID才能使用到期提醒
4. **TheMealDB API**: 免费开放 API（https://www.themealdb.com/api.php），无需申请密钥

## 📄 License

MIT License © 2026 FridgeMate

---

Made with ❤️ for every home cook 🧊
# -

# 🌟 Moo日记 - 个人日记应用

一个现代化的前后端分离的个人日记应用，支持日记记录、情绪追踪和数据统计。

## 📊 项目架构

```
moo-diary/
├── backend/              # Java Spring Boot后端
│   ├── src/
│   ├── pom.xml
│   └── Dockerfile
├── frontend/             # Vue 3 + Vite前端
│   ├── src/
│   ├── package.json
│   └── Dockerfile
└── docs/                 # 项目文档
```

## 🛠️ 技术栈

### 后端
- **框架**: Spring Boot 3.0
- **认证**: Spring Security + JWT
- **数据库**: MySQL 8.0
- **ORM**: Spring Data JPA
- **构建**: Maven

### 前端
- **框架**: Vue 3
- **构建**: Vite
- **状态管理**: Pinia
- **HTTP客户端**: Axios
- **UI组件**: Element Plus
- **样式**: Tailwind CSS

## ✨ 核心功能

### 用户管理
- ✅ 用户注册、登录、登出
- ✅ JWT令牌认证
- ✅ 用户个人资料

### 日记管理
- ✅ 创建日记（支持标题、内容、心情、天气、标签）
- ✅ 编辑日记
- ✅ 删除日记
- ✅ 按日期查看日记
- ✅ 搜索和过滤日记

### 数据统计
- ✅ 月度日记统计
- ✅ 心情分布图表
- ✅ 标签云展示

## 🚀 快速开始

### 前置要求
- Java 17+
- Node.js 18+
- MySQL 8.0
- Git

### 后端启动

```bash
# 1. 创建数据库
mysql -u root -p < backend/sql/init.sql

# 2. 配置数据库连接
# 编辑 backend/src/main/resources/application.yml

# 3. 启动后端
cd backend
mvn clean install
mvn spring-boot:run
```

后端运行在 `http://localhost:8080`

### 前端启动

```bash
# 1. 安装依赖
cd frontend
npm install

# 2. 启动开发服务器
npm run dev
```

前端运行在 `http://localhost:5173`

## 📖 API文档

详见 [API文档](./docs/API.md)

## 🤝 项目贡献

欢迎提交Issue和Pull Request！

## 📝 许可证

MIT License

<template>
  <div class="profile-container">
    <el-row :gutter="20">
      <!-- 用户信息卡片 -->
      <el-col :xs="24" :sm="24" :md="8">
        <el-card class="profile-card">
          <template #header>
            <span>个人信息</span>
          </template>
          
          <div class="user-avatar">
            <el-avatar
              :src="userStore.user?.avatar"
              :size="100"
            />
          </div>
          
          <div class="user-info">
            <p><strong>用户名：</strong>{{ userStore.user?.username }}</p>
            <p><strong>邮箱：</strong>{{ userStore.user?.email }}</p>
            <p><strong>注册时间：</strong>{{ formatDate(userStore.user?.createdAt) }}</p>
          </div>
        </el-card>
      </el-col>

      <!-- 统计信息 -->
      <el-col :xs="24" :sm="24" :md="16">
        <el-row :gutter="20" class="statistics">
          <el-col :xs="12" :sm="6">
            <el-statistic title="日记总数" :value="statistics.totalDiaries" />
          </el-col>
          <el-col :xs="12" :sm="6">
            <el-statistic title="本月日记" :value="statistics.monthDiaries" />
          </el-col>
          <el-col :xs="12" :sm="6">
            <el-statistic title="最常心情" :value="statistics.topMood" />
          </el-col>
          <el-col :xs="12" :sm="6">
            <el-statistic title="连续记录天数" :value="statistics.consecutiveDays" />
          </el-col>
        </el-row>

        <!-- 心情分布图表 -->
        <el-card class="chart-card" style="margin-top: 20px;">
          <template #header>
            <span>心情分布</span>
          </template>
          <div id="moodChart" style="height: 300px;"></div>
        </el-card>
      </el-col>
    </el-row>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useUserStore } from '../stores/userStore'
import { diaryAPI } from '../api'
import { ElMessage } from 'element-plus'

const userStore = useUserStore()
const statistics = ref({
  totalDiaries: 0,
  monthDiaries: 0,
  topMood: '😐',
  consecutiveDays: 0
})

onMounted(async () => {
  await loadStatistics()
})

const loadStatistics = async () => {
  try {
    const response = await diaryAPI.getStatistics()
    if (response.code === 200) {
      statistics.value = response.data
    }
  } catch (error) {
    ElMessage.error('加载统计数据失败')
  }
}

const formatDate = (date) => {
  return new Date(date).toLocaleDateString('zh-CN')
}
</script>

<style scoped>
.profile-container {
  padding: 20px;
}

.profile-card {
  text-align: center;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
}

:deep(.profile-card .el-card__header) {
  border-bottom: 1px solid rgba(255, 255, 255, 0.2);
  color: white;
}

:deep(.profile-card .el-card__body) {
  background: white;
  color: #333;
}

.user-avatar {
  margin-bottom: 20px;
}

:deep(.user-avatar .el-avatar) {
  background-color: #667eea;
}

.user-info p {
  margin: 10px 0;
  font-size: 14px;
  line-height: 1.8;
}

.statistics {
  margin-top: 20px;
}

:deep(.el-statistic) {
  --el-statistic-content-font-size: 28px;
  --el-statistic-title-font-size: 14px;
}

.chart-card {
  background: white;
}
</style>

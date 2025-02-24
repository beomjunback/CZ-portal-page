<template>
  <div class="ranking-container">
    <div class="header">
      <transition  name="fade-title">
        <h1 v-if="show" class="title">Current Ranking</h1>
      </transition>

      <transition  name="fade-content">
        <h2 v-if="show" class="subtitle">This Week's Top Performers</h2>
      </transition>
    </div>

    <transition  name="fade-content">
      <div v-if="show" class="ranking-list">
        <div
            v-for="(user, index) in users"
            :key="user.id"
            class="ranking-item"
        >
          <div class="rank-info">
            <span class="rank">#{{ index + 1 }}</span>
            <span class="username">{{ user.name }}</span>
            <span class="score">{{ user.score }}</span>
          </div>
          <div class="progress-bar">
            <div class="progress-fill" :style="{ width: (user.score / maxScore * 100) + '%' }"></div>
          </div>
        </div>
      </div>
    </transition>
  </div>
</template>

<script>
import { ref, onMounted } from "vue";

export default {
  name: "CurrentRanking",
  setup() {
    const users = ref(
        Array.from({ length: 20 }, (_, i) => ({
          id: i + 1,
          name: `User ${i + 1}`,
          score: Math.floor(Math.random() * 2000) + 1000,
        })).sort((a, b) => b.score - a.score)
    );

    const maxScore = ref(users.value[0].score);

    const show = ref(false);

    onMounted(() => {
      show.value = true; // 페이지가 로드되면 애니메이션 실행
    });

    return { show, users, maxScore };
  },
};
</script>

<style scoped>
.ranking-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-start;
  height: 100vh;
  color: white;
  text-align: center;
  position: relative;
  padding-top: 80px;
  padding-bottom: 80px;
  font-family: 'Poppins', sans-serif;
}

.header {
  position: relative;
  width: 100%;
  padding: 20px 0;
  z-index: 10;
}

.title {
  margin-top: 60px;
  letter-spacing: 1px;
}

.subtitle {
  font-size: 1.2rem;
  opacity: 0.8;
  margin-bottom: 40px;
}

.ranking-list {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 16px;
  width: 80%;
  max-height: 60vh;
  overflow-y: auto;
  padding-right: 10px;
  border-top: 2px solid rgba(255, 255, 255, 0.2);
  padding-top: 10px;
  position: relative;
}

/* 스크롤바 스타일 */
.ranking-list::-webkit-scrollbar {
  width: 8px;
}

.ranking-list::-webkit-scrollbar-track {
  background: transparent;
}

.ranking-list::-webkit-scrollbar-thumb {
  background: rgba(255, 255, 255, 0.3);
  border-radius: 4px;
}

.ranking-list::-webkit-scrollbar-thumb:hover {
  background: rgba(255, 255, 255, 0.5);
}

.ranking-item {
  width: 100%;
  background: #252525;
  padding: 16px 24px;
  border-radius: 12px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  font-size: 1.1rem;
  color: #eee;
  font-weight: 400;
}

.rank-info {
  display: flex;
  justify-content: space-between;
  width: 100%;
  margin-bottom: 8px;
  font-size: 1rem;
}

.rank {
  font-weight: 500;
  color: #ffcc00;
}

.username {
  flex: 1;
  text-align: center;
}

.score {
  font-weight: 500;
  color: #66bb6a;
}

.progress-bar {
  width: 100%;
  height: 12px;
  background: #444;
  border-radius: 6px;
  overflow: hidden;
}

.progress-fill {
  height: 100%;
  background: linear-gradient(90deg, #ffcc00, #ff8c00);
  border-radius: 6px;
  transition: width 0.5s ease-in-out;
}

.fade-title-enter-active {
  transition: opacity 1s ease, transform 0.8s ease;
}
.fade-title-enter-from {
  opacity: 0;
  transform: translateY(10px);
}

.fade-content-enter-active {
  transition: opacity 1s ease 0.5s, transform 0.8s ease 0.5s;
}
.fade-content-enter-from {
  opacity: 0;
  transform: translateY(10px);
}
</style>

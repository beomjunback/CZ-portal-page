<template>
  <div class="ranking-container">
    <transition name="fade-title">
      <h1 v-if="show" class="title">🏆 Baekjoon King 🏆</h1>
    </transition>

    <transition name="fade-content">
      <p v-if="show" class="subtitle">이번 주 시상 종목 : [가장 많은 문제] <br><br> Recent Top 4</p>
    </transition>
    <transition name="fade-content">
    <div v-if="show" class="podium">
      <div class="rank-container">
        <div class="rank third">
          <div class="rank-box">
            <span class="rank-number">3</span>
          </div>
        </div>
        <div class="user-name">code_master</div>
      </div>
      <div class="rank-container">
        <div class="rank second">
          <div class="rank-box">
            <span class="rank-number">2</span>
            <div class="rank-name">우승</div>
          </div>
        </div>
        <div class="user-name">cau-gragas</div>
      </div>

      <div class="rank-container">
        <div class="rank first">
          <div class="rank-box">
            <span class="rank-number">1</span>
            <div class="rank-name">우승</div>
          </div>
        </div>
        <div class="user-name">whisky killer</div>
      </div>

      <div class="rank-container">
        <div class="rank fourth">
          <div class="rank-box">
            <span class="rank-number">4</span>
          </div>
        </div>
        <div class="user-name">dev_legend</div>
      </div>
    </div>
    </transition>

    <transition name="fade-content">
    <footer v-if="show" class="footer">
      <router-link to="/sign" class="btn">참여하기</router-link>
      <router-link to="/rank" class="btn">Ranking</router-link>
    </footer>
    </transition>

  </div>
</template>

<script>
import { ref, onMounted } from "vue";

export default {
  name: "BaekjoonKing",
  setup() {
    const show = ref(false);

    onMounted(() => {
      show.value = true; // 페이지가 로드되면 애니메이션 실행
    });

    return { show };
  },
};
</script>


<style scoped>
.ranking-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  color: white;
  text-align: center;
  position: relative;
  padding-bottom: 80px;
}

.subtitle {
  font-size: 1.2rem;
  opacity: 0.8;
  margin-bottom: 40px;
}

.podium {
  display: flex;
  justify-content: center;
  align-items: flex-end;
  gap: 30px;
}

.rank-container {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.rank {
  width: 150px;
  height: 250px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 10px;
  background: rgba(255, 255, 255, 0.1);
  box-shadow: 0 8px 32px rgba(255, 255, 255, 0.1);
  text-align: center;
  transition: all 0.3s ease-in-out;
}

.rank-box {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.rank-number {
  font-size: 2rem;
  font-weight: bold;
  margin-bottom: 10px;
}

.rank-name {
  font-size: 1.2rem;
  font-weight: 600;
  opacity: 0.9;
}

.user-name {
  font-size: 1.5rem;
  font-weight: bold;
  margin-top: 30px;
  background: var(--gradient);
  -webkit-background-clip: text;
  background-clip: text;
  -webkit-text-fill-color: transparent;
  animation: gradient 8s linear infinite;
  background-size: 300%;
}

.first {
  height: 300px;
  background: rgba(255, 200, 0, 0.6);
}

.second {
  height: 260px;
  background: rgba(255, 192, 192, 0.6);
}

.third {
  height: 220px;
  background: rgba(192, 192, 255, 0.6);
}

.fourth {
  height: 190px;
  background: rgba(192, 255, 192, 0.6);
}

/* ✅ Footer 스타일 - 버튼을 1~4등 상자와 일치 */
.footer {
  position: absolute;
  bottom: 20px;
  width: 100%;
  display: flex;
  justify-content: center;
  gap: 40px;
}
.btn {
  width: 150px;
  height: 50px;
  font-size: 1.2rem;
  font-weight: bold;
  color: white;
  text-decoration: none;
  border-radius: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: rgba(255, 255, 255, 0.2);
  box-shadow: 0 4px 15px rgba(255, 255, 255, 0.1);
  transition: all 0.3s ease-in-out;
}

.btn:hover {
  background: rgba(255, 255, 255, 0.4);
  box-shadow: 0 6px 20px rgba(255, 255, 255, 0.2);
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


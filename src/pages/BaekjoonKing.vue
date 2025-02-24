<template>
  <div class="ranking-container">
    <transition name="fade-title">
      <h1 v-if="show" class="title">🏆 Baekjoon King 🏆</h1>
    </transition>

    <transition name="fade-content">
      <p v-if="show" class="subtitle">이번 주 시상 종목 : <span class="highlight">[Rating 상승 폭]</span> <br><br> <span class="highlight">Current Top 4</span></p>
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
            </div>
          </div>
          <div class="user-name">cau-gragas</div>
        </div>

        <div class="rank-container">
          <div class="rank first">
            <div class="rank-box">
              <span class="rank-number">1</span>
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
        <router-link to="/rank" class="btn">역대 우승자</router-link>
        <router-link to="/current-rank" class="btn">현재 순위</router-link>
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
      show.value = true;
    });

    return { show };
  },
};
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;600&family=Noto+Sans+KR:wght@400;700&display=swap');

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
  font-family: 'Poppins', 'Noto Sans KR', sans-serif;
}

.subtitle {
  font-size: 1.2rem;
  opacity: 0.8;
  margin-bottom: 40px;
}

.highlight {
  font-weight: 700;
  font-size: 1.3rem;
  color: #ffd700;
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
  width: 140px;
  height: 230px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 12px;
  text-align: center;
  transition: all 0.3s ease-in-out;
  border: 2px solid rgba(255, 255, 255, 0.2);
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
  color: white;
}

.user-name {
  font-size: 1.3rem;
  font-weight: bold;
  margin-top: 20px;
  color: white;
}

.first {
  height: 280px;
  background: linear-gradient(145deg, #b8860b, #8b6914);
  box-shadow: 0 10px 30px rgba(184, 134, 11, 0.2);
}

.second {
  height: 250px;
  background: linear-gradient(145deg, #808080, #696969);
  box-shadow: 0 10px 30px rgba(128, 128, 128, 0.2);
}

.third {
  height: 220px;
  background: linear-gradient(145deg, #8b5a2b, #6f4f28);
  box-shadow: 0 10px 30px rgba(139, 90, 43, 0.2);
}

.fourth {
  height: 190px;
  background: linear-gradient(145deg, #4f6272, #3c4a57);
  box-shadow: 0 10px 30px rgba(79, 98, 114, 0.2);
}


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

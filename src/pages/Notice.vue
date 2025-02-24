<template>
  <div class="notice-container">
    <transition name="fade-title">
      <h1 v-if="show" class="title">📢 NOTICES 📢</h1>
    </transition>

    <transition name="fade-content">
      <div v-if="show" class="notice-content">
        <!-- 왼쪽 -->
        <div class="notice-list">
          <div
              v-for="notice in notices"
              :key="notice.id"
              class="notice-item"
              @click="selectedNotice = notice"
              :class="{
                        'important-notice': notice.flag === 1,
                        'selected-notice': selectedNotice && selectedNotice.id === notice.id
                      }"
          >
            <h3 class="notice-title">{{ notice.title }}</h3>
            <p class="notice-date">{{ notice.date }}</p>
          </div>
        </div>

        <!--오른쪽 -->
        <div class="notice-detail">
          <transition name="fade-detail">
            <div v-if="selectedNotice" :key="selectedNotice.id">
              <div class="detail-header">
                <h2 class="detail-title">{{ selectedNotice.title }}</h2>
                <p class="detail-date">
                  게시: {{ selectedNotice.date }}
                  <span
                      :class="{'status-icon active': selectedNotice.flag === 1, 'status-icon inactive': selectedNotice.flag === 0}"
                  >●</span>
                  <span class="status-text">{{ selectedNotice.flag === 1 ? '진행' : '종료' }}</span>
                </p>
              </div>
              <p class="detail-text">{{ selectedNotice.content }}</p>
            </div>
            <p v-else key="placeholder" class="detail-placeholder">공지사항을 선택하세요.</p>
          </transition>
        </div>
      </div>
    </transition>
  </div>
</template>

<script>
import {ref, onMounted} from "vue";

export default {
  name: "Notice",
  setup() {
    const show = ref(false);

    onMounted(() => {
      show.value = true; // 페이지가 로드되면 애니메이션 실행
    });

    return {show};
  },
  data() {
    return {
      selectedNotice: null,
      notices: []
    };
  },
  async created() {
    await this.loadNotices();
  },
  methods: {
    async loadNotices() {
      try {
        const response = await fetch('/notices.json'); // JSON 데이터 불러오기
        let notices = await response.json();

        // 중요 공지 (flag: 1)를 먼저 정렬, 이후 날짜 기준 최신순 정렬
        notices.sort((a, b) => {
          if (a.flag !== b.flag) {
            return b.flag - a.flag; // flag 1이 우선
          }
          return new Date(b.date) - new Date(a.date); // 최신순 정렬
        });

        this.notices = notices;
      } catch (error) {
        console.error('Failed to load notices:', error);
      }
    }
  }
};
</script>

<style scoped>
.notice-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  overflow: hidden;
  color: white;
  text-align: center;
  position: relative;
  padding-bottom: 80px;
}

.title {
  margin-top: 100px;
  margin-bottom: 30px;
}

/* 공지사항 컨테이너 */
.notice-content {
  display: flex;
  width: 80%;
  height: 60vh;
  gap: 20px;
}

/*왼쪽 */
.notice-list {
  flex: 1;
  background: rgba(255, 255, 255, 0.1);
  padding: 20px;
  border-radius: 10px;
  overflow-y: auto;
  height: 100%;
  box-shadow: 0 8px 32px rgba(255, 255, 255, 0.1);
}

.notice-item {
  padding: 10px;
  margin-bottom: 10px;
  background: rgba(255, 255, 255, 0.2);
  border-radius: 8px;
  cursor: pointer;
  transition: all 0.3s ease-in-out;
  border: 2px solid transparent;
}

.important-notice {
  border: 1.5px solid rgba(229, 115, 115, 0.8);
}

.notice-item:hover,
.selected-notice {
  background: rgba(255, 255, 255, 0.4);
}

.notice-title {
  font-size: 1rem;
  font-weight: bold;
}

.notice-date {
  font-size: 0.8rem;
  opacity: 0.7;
}

/* 오른쪽 */
.notice-detail {
  flex: 1;
  background: rgba(255, 255, 255, 0.1);
  padding: 20px;
  border-radius: 10px;
  overflow-y: auto;
  height: 100%;
  box-shadow: 0 8px 32px rgba(255, 255, 255, 0.1);
}

.detail-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.detail-title {
  font-size: 1.5rem;
  font-weight: bold;
  margin-bottom: 10px;
}

.detail-date {
  font-size: 0.8rem;
  opacity: 0.7;
  text-align: right;
}

.detail-text {
  font-size: 1rem;
  text-align: left;
}

.detail-placeholder {
  font-size: 1rem;
  opacity: 0.7;
}

.status-icon {
  font-size: 0.8rem;
  margin-left: 5px;
}

.status-icon.active {
  color: #4CAF50; /* 초록색 */
}

.status-icon.inactive {
  color: #9E9E9E; /* 회색 */
}

.status-text {
  font-size: 0.8rem;
  margin-left: 5px;
  font-weight: bold;
}

/* 제목 페이드 효과 */
.fade-title-enter-active {
  transition: opacity 1s ease, transform 0.8s ease;
}

.fade-title-enter-from {
  opacity: 0;
  transform: translateY(10px);
}

/* 내용 페이드 효과 */
.fade-content-enter-active {
  transition: opacity 1s ease 0.5s, transform 0.8s ease 0.5s;
}

.fade-content-enter-from {
  opacity: 0;
  transform: translateY(10px);
}

/* 상세 내용 전환 효과 */
.fade-detail-enter-active {
  transition: opacity 0.5s ease, transform 0.3s ease;
}

.fade-detail-enter-from {
  opacity: 0;
  transform: translateY(10px);
}
</style>

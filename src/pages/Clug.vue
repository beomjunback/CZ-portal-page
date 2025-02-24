<template>
  <div class="clug-container">
    <div class="content">
      <!-- 페이지 전환 버튼 -->
      <button class="nav-button left" @click="prevPage" v-if="currentPage > 0">←</button>
      <button class="nav-button right" @click="nextPage" v-if="currentPage < sections.length - 1">→</button>

      <!-- 현재 페이지의 섹션들 (3개씩 배치) -->
      <transition name="fade-in" mode="out-in">
        <div v-if="showContent" :key="currentPage" class="section-group">
          <div class = "logo-container">
            <div v-if="currentPage === 0" class="box"><b>
              <img src="@/assets/clug-logo2.jpeg" alt="CLUG Logo" class="clug-logo">
            </b></div>
          </div>
          <div v-for="(item, index) in sections[currentPage]" :key="index" class="section">
            <div class="section-title">{{ item.title }}</div>
            <p class="section-text">{{ item.content }}</p>
          </div>
        </div>
      </transition>
    </div>
  </div>
</template>

<script>
import {ref, onMounted} from "vue";

export default {
  name: "ZeroPage",
  setup() {
    const currentPage = ref(0);
    const showContent = ref(false); // 처음에는 숨김 상태

    const sections = ref([
      [ // 페이지 1 (로고 포함된 Introduction)
        {
          title: "Introduction",
          content: "안녕하세요! 중앙대학교를 대표하는 오픈소스 소프트웨어 동아리 CLUG입니다!\n" +
              "CLUG는 자유 소프트웨어를 탐구하는, 중앙대학교 리눅스·유닉스 사용자 모임입니다. 다양한 주제의 스터디, 세미나, 멘토링 및 해커톤를 진행합니다. ‘이모저모’와 같은 활동들로 졸업생들과의 만남을 통해 다양한 이야기를 듣고 조언을 얻습니다"
        },
      ],
      [ // 페이지 2
        {title: "Hackathons", content: "We organize hackathons where members can build projects and compete in teams."},
        {title: "Workshops", content: "CLUG holds workshops covering cutting-edge technologies and development tools."},
        {
          title: "Open Source",
          content: "We contribute to open-source projects and encourage collaboration in the community."
        }
      ],
      [ // 페이지 3
        {
          title: "Networking",
          content: "Connect with fellow developers and industry experts through our networking events."
        },
        {
          title: "Tech Talks",
          content: "Learn from experienced speakers who share insights on software engineering and technology."
        },
        {
          title: "Career Support",
          content: "We provide mentorship and career guidance to help our members succeed in tech."
        }
      ],
    ]);

    const nextPage = () => {
      if (currentPage.value < sections.value.length - 1) {
        currentPage.value++;
      }
    };

    const prevPage = () => {
      if (currentPage.value > 0) {
        currentPage.value--;
      }
    };

    onMounted(() => {
      setTimeout(() => {
        showContent.value = true; // 페이지 로드 후 0.3초 뒤에 콘텐츠 표시
      }, 100);
    });

    return {currentPage, sections, nextPage, prevPage, showContent};
  },
};
</script>

<style scoped>
.clug-container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  text-align: left; /* 모든 텍스트 왼쪽 정렬 */
  padding: 40px;
  position: relative;
}

/* 개별 페이지에 3개의 섹션 배치 */
.section-group {
  display: flex;
  flex-direction: column;
  gap: 60px; /* 섹션 간격 */
}

/* 개별 섹션 */
.section {
  width: 100%;
  max-width: 800px;
  background: var(--glass-bg);
  padding: 30px;
  border: var(--border);
  box-shadow: var(--shadow);
  border-radius: 12px;
}

.logo-container {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
  padding: 50px;
  gap: 50px;
}

.logo-container .box {
  position: relative;
  width: 220px; /* 로고 크기에 맞춰 박스 크기 조정 */
  height: 220px;
  display: flex;
  justify-content: center;
  align-items: center;
  background: #fff;
  border-radius: 20px;
  overflow: hidden; /* 넘치는 부분 숨김 */
}


.logo-container .box::before {
  content: "";
  position: absolute;
  inset: 0;
  border-radius: 20px;
  background: #f00;
}
.logo-container .box::after {
  content: "";
  position: absolute;
  inset: 0;
  border-radius: 20px;
  background: #f00;
  filter: blur(16px);
}
.logo-container .box b {
  padding: 30px;
  position: absolute;
  display: block;
  inset: 4px;
  border-radius: 16px;
  background: rgba(0, 0, 0, 0.75);
  z-index: 2;
}

.logo-container .box b p {
  font-weight: 200;
  color: #fff;
  text-shadow: 0 0 15px #fff;
}

.logo-container .box:nth-child(1)::before,
.logo-container .box:nth-child(1)::after {
  background: linear-gradient(45deg, #ffbc00, #ff0058);
}

.logo-container .box:nth-child(2)::before,
.logo-container .box:nth-child(2)::after {
  background: linear-gradient(45deg, #03a9f4, #ff0058);
}

.logo-container .box:nth-child(3)::before,
.logo-container .box:nth-child(3)::after {
  background: linear-gradient(45deg, #4dff03, #00d0ff);
}


/* clug 로고 */
.clug-logo {
  width: 100%;  /* 부모 요소인 .box에 맞춤 */
  height: 100%;
  object-fit: contain; /* 이미지 비율 유지하면서 꽉 차도록 */
}


/* 섹션 제목 */
.section-title {
  display: inline-block;
  padding: 10px 20px;
  font-size: 1.8rem;
  font-weight: bold;
  color: white;
  background: rgba(255, 255, 255, 0.1);
  border-radius: 12px;
  border: 2px solid white;
  margin-bottom: 15px;
}

/* 섹션 본문 */
.section-text {
  font-size: 1.2rem;
  line-height: 1.6;
  color: white;
  white-space: pre-line;
}

/* 네비게이션 버튼 */
.nav-button {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  padding: 12px 18px;
  font-size: 1.5rem;
  border: none;
  background: rgba(255, 255, 255, 0.2);
  color: white;
  cursor: pointer;
  border-radius: 50%;
  transition: 0.3s;
}

.nav-button:hover {
  background: rgba(255, 255, 255, 0.4);
}

.nav-button.left {
  left: 20px;
}

.nav-button.right {
  right: 20px;
}

/* 첫 로딩 시 적용될 Fade-in 애니메이션 */
.fade-in-enter-active {
  transition: opacity 1s ease, transform 0.8s ease;
}

.fade-in-enter-from {
  opacity: 0;
  transform: translateY(20px);
}
</style>

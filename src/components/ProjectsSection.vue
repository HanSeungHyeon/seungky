<template>
  <section id="projects" class="projects" ref="sectionRef">
    <div :class="['projects__inner', { visible }]">
      <div class="projects__header">
        <div class="section-tag">Projects</div>
      </div>

      <div class="category">
        <div class="category__header">
          <h3 class="category__title">회사 프로젝트</h3>
          <span class="category__count">{{ companyProjects.length }}</span>
        </div>
        <div class="featured">
          <div
            v-for="(p, i) in companyProjects"
            :key="'company-' + i"
            class="feat-card"
            role="button"
            tabindex="0"
            @click="openModal(p)"
            @keydown.enter="openModal(p)"
            @keydown.space.prevent="openModal(p)"
          >
            <div class="feat-card__header-top">
              <h3 class="feat-card__name">{{ p.name }}</h3>
              <span v-if="p.period" class="feat-card__period">{{ p.period }}</span>
            </div>
            <p class="feat-card__desc">{{ p.desc }}</p>
            <div class="feat-card__tags">
              <span v-for="t in p.tags" :key="t" class="feat-card__tag">{{ t }}</span>
            </div>
          </div>
        </div>
      </div>

      <div class="category">
        <div class="category__header">
          <h3 class="category__title">사이드 프로젝트</h3>
          <span class="category__count">{{ sideProjects.length }}</span>
        </div>
        <div class="featured">
          <div
            v-for="(p, i) in sideProjects"
            :key="'side-' + i"
            class="feat-card"
            role="button"
            tabindex="0"
            @click="openModal(p)"
            @keydown.enter="openModal(p)"
            @keydown.space.prevent="openModal(p)"
          >
            <div class="feat-card__header-top">
              <h3 class="feat-card__name">{{ p.name }}</h3>
              <span v-if="p.period" class="feat-card__period">{{ p.period }}</span>
            </div>
            <p class="feat-card__desc">{{ p.desc }}</p>
            <div class="feat-card__tags">
              <span v-for="t in p.tags" :key="t" class="feat-card__tag">{{ t }}</span>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Modal -->
    <Teleport to="body">
      <Transition name="modal">
        <div v-if="modal" class="modal-overlay" @click.self="closeModal">
          <div class="modal" role="dialog" aria-modal="true" :aria-label="modal.name">
            <button class="modal__close" aria-label="닫기" @click="closeModal">✕</button>
            <div class="modal__header-top">
              <h2 class="modal__title">{{ modal.name }}</h2>
              <span v-if="modal.period" class="modal__period">{{ modal.period }}</span>
            </div>
            <div class="modal__tags">
              <span v-for="t in modal.tags" :key="t" class="modal__tag">{{ t }}</span>
            </div>
            <div class="modal__body">
              <h4 class="modal__subtitle">프로젝트 소개</h4>
              <p>{{ modal.desc }}</p>

              <h4 class="modal__subtitle">주요 기능</h4>
              <ul class="modal__features">
                <li v-for="f in modal.features" :key="f">{{ f }}</li>
              </ul>

              <h4 class="modal__subtitle">담당 역할</h4>
              <p>{{ modal.role }}</p>
            </div>
            <div class="modal__footer">
              <a v-if="modal.link && modal.link !== '#'" :href="modal.link" target="_blank" class="modal__btn">
                {{ modal.link.includes('github.com') ? 'GitHub에서 보기 →' : '프로젝트 보기 →' }}
              </a>
              <a
                v-for="store in modal.storeLinks || []"
                :key="store.label"
                :href="store.url"
                target="_blank"
                rel="noopener noreferrer"
                class="modal__btn"
              >
                {{ store.label }}
              </a>
            </div>
          </div>
        </div>
      </Transition>
    </Teleport>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const sectionRef  = ref(null)
const visible     = ref(false)
const modal       = ref(null)

function openModal(project) {
  modal.value = project
  document.body.style.overflow = 'hidden'
}

function closeModal() {
  modal.value = null
  document.body.style.overflow = ''
}

const companyProjects = [
  {
    name: '라포라포(RAPORAPO)',
    period: '2025',
    link: '#',
    desc: '게이미케이션 교육 플랫폼.',
    tags: ['Spring', 'Vue', 'Node.js', 'AWS'],
    features: [
      '콘텐츠 에디터',
      'QR게임, OX게임, 주사위게임',
      '관리자 대시보드',
      'https://raporapo.com',
    ],
    role: '관리자 대시보드, 결제 기능, 기억력게임 개발',
  },
  {
    name: '코오롱 해킹메일 모의 훈련',
    period: '2023',
    link: '#',
    desc: '코오롱 사내 해킹메일 관련 훈련, 교육, 시험 관리자 시스템.',
    tags: ['Spring', 'Oracle', 'Tomcat', 'Linux'],
    features: [
      '사용자 관리 (인사 연동)',
      '메일 훈련 (메일 발송, 결과 통계)',
      '보안 교육 시스템 (pdf, mp4)',
      '보안 시험 시스템',
      '관리자 대시보드',
    ],
    role: '환경 구축, 솔루션 커스터마이징, 프로젝트 관리 담당',
  },
  {
    name: '경동 ERP 시스템',
    period: '2023',
    link: '#',
    desc: '경동 사내 ERP 시스템.',
    tags: ['웹스퀘어', 'ChartJs', 'JS', 'Oracle'],
    features: [
      '시스템 코드 관리',
      '거래처 관리',
      '주문, 수요, 공급, 재고 관리',
      '계획 관리',
    ],
    role: '계획, 주문, 공급 관리 개발',
  },
  {
    name: '외교부 정보보안 시스템',
    period: '2022',
    link: '#',
    desc: '보안장비, IP, 방화벽 등 외교부 내 정보보안 시스템 관리자 대시보드.',
    tags: ['Spring', 'Maria DB', 'JSP', 'Linux',],
    features: [
      '보안장비(pc, 복사기, 노트북) 관리',
      'IP, 방화벽, 망점점, 차단사이트, pc신청',
      '용역사업관리',
      '알림메일 발송',
      '결재 시스템 구축',
    ],
    role: 'Spring 백엔드 아키텍처 설계 및 API 개발 담당',
  },
]

const sideProjects = [
  {
    name: '미니언(MINION)',
    period: '2026',
    link: 'https://minion.fan',
    storeLinks: [
      { label: 'Google Play', url: 'https://play.google.com/store/apps/details?id=com.minion.app' },
      { label: 'App Store', url: 'https://apps.apple.com/kr/app/minion/id6826082325' },
    ],
    desc: 'LCK 경기 일정·기록부터 팬 소통까지 한곳에 모은 e스포츠 팬 커뮤니티 플랫폼. 웹과 앱을 함께 운영하는 멀티 플랫폼 서비스입니다.',
    tags: ['Next.js', 'React', 'TypeScript', 'Supabase', 'Expo'],
    features: [
      'LCK 경기 일정·플레이오프 대진표·승부 예측 제공',
      '선수/챔피언 통계 및 POM(Player of the Match) 하이라이트',
      '팬톡 게시판과 10개 팀별 팬 채널 커뮤니티 운영',
      '국내 매체 e스포츠 뉴스 및 경기 하이라이트 영상 아카이빙',
      'Supabase 기반 데이터 관리와 웹/앱 공통 운영 구조 설계',
    ],
    role: '기획·디자인·프론트엔드 개발을 맡아 웹/앱 동시 런칭까지 참여',
  },
  {
    name: 'DA (detail-auto)',
    period: '2026',
    link: 'https://github.com/HanSeungHyeon/detail-auto',
    desc: '상품 정보와 이미지를 바탕으로 AI 상품 상세 페이지 구성을 돕도록 설계한 웹 앱입니다. 샘플 탐색, 작성 폼, 대시보드와 결과 화면 UI를 구현했으며 인증·저장·생성 서버 액션은 준비 중입니다.',
    tags: ['Next.js 16', 'React 19', 'TypeScript', 'Tailwind CSS 4', 'shadcn/ui', 'Zustand', 'Supabase', 'Groq'],
    features: [
      '뷰티·패션·리빙·테크 샘플 콘텐츠 및 상세 페이지 UI',
      '이미지 업로드와 상품명, 타깃, 가격, 할인율, 판매 포인트 입력 폼',
      '가격과 할인율을 반영한 할인가 미리보기',
      '로그인·회원가입 화면과 프로젝트 대시보드 UI',
      '히어로, 문제 제기, 해결책, 사용 방법, 리뷰, 혜택, CTA로 구성되는 결과 화면',
      'Groq 모델을 사용하는 상세 콘텐츠 생성 유틸리티와 Supabase 데이터 스키마 작성',
      '인증·프로젝트 생성 및 조회 서버 액션은 준비 중이며, 실제 생성·저장 흐름은 아직 연결되지 않음',
    ],
    role: '상품 상세 페이지 생성 서비스의 화면과 입력 흐름을 구성하고, AI 콘텐츠 생성 유틸리티 및 Supabase 데이터 스키마를 작성했습니다.',
  },
  {
    name: '와유(WAU)',
    period: '2025',
    link: 'https://github.com/HanSeungHyeon/wau',
    desc: '모바일 청첩장 웹 프로젝트로, 결혼식 초대장을 감성적으로 전달하는 브랜딩형 서비스.',
    tags: ['Nuxt 3', 'Vue 3', 'TypeScript', 'Responsive'],
    features: [
      '모바일 친화적인 청첩장 레이아웃 구성',
      '감성적인 브랜딩 UI와 초대 문구 중심 디자인',
      '반응형 페이지로 모바일 사용자 경험 최적화',
    ],
    role: '프론트엔드 구현 및 모바일 중심 UX 설계 참여',
  },
  {
    name: 'selLF',
    period: '2024',
    link: 'https://github.com/HanSeungHyeon/selLf',
    desc: '프로젝트 포트폴리오를 게시하고 방문자가 카테고리별로 살펴볼 수 있도록 만든 Spring Boot 기반 웹 서비스입니다. 프로젝트 목록과 소개·이력·문의 페이지, 회원 및 게시판 기능을 구현했습니다.',
    tags: ['Java 8', 'Spring Boot 2.6', 'Spring MVC', 'Thymeleaf', 'MyBatis', 'PostgreSQL', 'Firebase FCM'],
    features: [
      '프로젝트 게시글 목록과 카테고리 필터 제공',
      '게시글 상세 조회, 작성, 수정, 삭제 기능',
      '회원가입, 로그인, 계정 정보 찾기 및 수정',
      '문의 양식을 통한 이메일 발송',
      '이미지 업로드와 출력',
      'Firebase Cloud Messaging 기반 브라우저 알림 구독 및 관리자 알림 발송',
      '관리자 메뉴와 /admin 경로 접근 제어',
    ],
    role: '포트폴리오 사이트의 서버 기능과 화면을 구현했습니다. Controller-Service-Mapper 구조로 기능을 구성하고 Thymeleaf와 MyBatis를 연동했습니다.',
  },
]

function onKeydown(e) {
  if (e.key === 'Escape') closeModal()
}

let observer
onMounted(() => {
  observer = new IntersectionObserver(
    ([entry]) => { if (entry.isIntersecting) visible.value = true },
    { threshold: 0.05 }
  )
  if (sectionRef.value) observer.observe(sectionRef.value)
  window.addEventListener('keydown', onKeydown)
})
onUnmounted(() => {
  observer?.disconnect()
  window.removeEventListener('keydown', onKeydown)
})
</script>

<style scoped>
.projects {
  padding: 64px 32px;
  max-width: 1100px;
  margin: 0 auto;
}

.projects__inner {
  opacity: 0;
  transform: translateY(24px);
  transition: opacity .7s var(--ease), transform .7s var(--ease);
}
.projects__inner.visible { opacity: 1; transform: none; }

.projects__header {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  margin-bottom: 48px;
}

.section-tag {
  font-family: var(--font-mono);
  font-size: 13px;
  font-weight: 500;
  color: var(--accent);
  padding-bottom: 16px;
  border-bottom: 2px solid var(--accent);
  display: inline-block;
}

.category { margin-bottom: 48px; }

.category__header {
  display: flex;
  align-items: center;
  gap: 8px;
  margin-bottom: 20px;
}

.category__title {
  font-family: var(--font-display);
  font-size: 16px;
  font-weight: 600;
  color: var(--text);
}

.category__count {
  font-family: var(--font-mono);
  font-size: 11px;
  font-weight: 500;
  color: var(--text-muted);
  background: var(--border-light);
  padding: 2px 8px;
  border-radius: 99px;
}

.featured {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 16px;
}

.feat-card {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: var(--radius-md);
  padding: 28px;
  transition: all .2s;
  cursor: pointer;
}
.feat-card:hover {
  border-color: var(--accent);
  box-shadow: var(--shadow-md);
  transform: translateY(-2px);
}
.feat-card:focus-visible {
  outline: 2px solid var(--accent);
  outline-offset: 2px;
}

.feat-card__header-top { display: flex; justify-content: space-between; align-items: flex-start; margin-bottom: 8px; }
.feat-card__name {
  font-family: var(--font-display);
  font-size: 18px; font-weight: 600;
  color: var(--text); margin-bottom: 0;
}
.feat-card__period { font-size: 13px; color: var(--text-muted); font-family: var(--font-mono); }
.feat-card__desc {
  font-size: 13px; color: var(--text-secondary);
  line-height: 1.6; margin-bottom: 20px;
}
.feat-card__tags { display: flex; flex-wrap: wrap; gap: 6px; }
.feat-card__tag {
  font-family: var(--font-mono); font-size: 11px;
  color: var(--accent); background: var(--accent-light);
  padding: 3px 10px; border-radius: 99px;
}

/* ── Modal ── */
.modal-overlay {
  position: fixed;
  inset: 0;
  z-index: 1000;
  background: rgba(0, 0, 0, 0.5);
  backdrop-filter: blur(4px);
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 24px;
}

.modal {
  background: var(--surface);
  border-radius: var(--radius-lg);
  max-width: 600px;
  width: 100%;
  max-height: 85vh;
  overflow-y: auto;
  padding: 40px;
  position: relative;
  box-shadow: var(--shadow-lg);
}

.modal__close {
  position: absolute;
  top: 16px; right: 16px;
  width: 36px; height: 36px;
  border: none;
  background: var(--border-light);
  border-radius: 50%;
  font-size: 16px;
  color: var(--text-muted);
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all .2s;
}
.modal__close:hover {
  background: var(--border);
  color: var(--text);
}

.modal__header-top { display: flex; justify-content: space-between; align-items: center; margin-bottom: 12px; }
.modal__title {
  font-family: var(--font-display);
  font-size: 28px;
  font-weight: 700;
  color: var(--text);
  margin-bottom: 0;
}
.modal__period { font-size: 16px; color: var(--text-muted); font-family: var(--font-mono); }

.modal__tags { display: flex; flex-wrap: wrap; gap: 6px; margin-bottom: 28px; }
.modal__tag {
  font-family: var(--font-mono); font-size: 12px;
  color: var(--accent); background: var(--accent-light);
  padding: 4px 12px; border-radius: 99px;
}

.modal__body { margin-bottom: 28px; }

.modal__subtitle {
  font-size: 14px;
  font-weight: 600;
  color: var(--text);
  margin-bottom: 8px;
  margin-top: 24px;
}
.modal__subtitle:first-child { margin-top: 0; }

.modal__body p {
  font-size: 14px;
  color: var(--text-secondary);
  line-height: 1.8;
}

.modal__features {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 6px;
}

.modal__features li {
  font-size: 14px;
  color: var(--text-secondary);
  padding-left: 16px;
  position: relative;
}
.modal__features li::before {
  content: '';
  position: absolute;
  left: 0; top: 9px;
  width: 5px; height: 5px;
  border-radius: 50%;
  background: var(--accent);
}

.modal__footer {
  display: flex;
  flex-wrap: wrap;
  gap: 16px;
  padding-top: 20px;
  border-top: 1px solid var(--border);
}

.modal__btn {
  display: inline-flex;
  font-size: 14px;
  font-weight: 600;
  color: var(--accent);
  transition: opacity .2s;
}
.modal__btn:hover { opacity: .7; }

/* Modal transition */
.modal-enter-active,
.modal-leave-active {
  transition: opacity .25s var(--ease);
}
.modal-enter-active .modal,
.modal-leave-active .modal {
  transition: transform .25s var(--ease), opacity .25s var(--ease);
}
.modal-enter-from,
.modal-leave-to {
  opacity: 0;
}
.modal-enter-from .modal {
  transform: translateY(16px) scale(0.97);
  opacity: 0;
}
.modal-leave-to .modal {
  transform: translateY(8px) scale(0.99);
  opacity: 0;
}

@media (max-width: 900px) {
  .projects { padding: 48px 20px; }
  .featured { grid-template-columns: 1fr; }
  .category { margin-bottom: 36px; }
  .projects__header { flex-direction: column; gap: 16px; }
  .modal { padding: 28px; max-height: 90vh; }
}
</style>

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
            @click="openModal(p)"
          >
            <h3 class="feat-card__name">{{ p.name }}</h3>
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
            @click="openModal(p)"
          >
            <h3 class="feat-card__name">{{ p.name }}</h3>
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
          <div class="modal">
            <button class="modal__close" @click="closeModal">✕</button>
            <h2 class="modal__title">{{ modal.name }}</h2>
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
                GitHub에서 보기 →
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
    name: '외교부 정보보안 시스템',
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
  {
    name: '코오롱 해킹메일 모의 훈련',
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
    name: '라포라포(RAPORAPO)',
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
    name: '경동 ERP 시스템',
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
]

const sideProjects = [
  {
    name: 'TPD (10초 그림일기)',
    link: 'https://github.com/HanSeungHyeon/tpd',
    desc: '10초 제한 시간 안에 그림을 그려 일기로 저장하는 웹 앱.',
    tags: ['Nuxt 3', 'Vue 3', 'TypeScript'],
    features: [
      '10초 타이머 캔버스 드로잉 보드',
      '그림 + 제목 + 내용을 포함한 일기 CRUD',
    ],
    role: '풀스택 기획/설계/개발 전체 담당 (1인 개발)',
  },
  {
    name: 'zoom',
    link: 'https://github.com/HanSeungHyeon/zoom',
    desc: 'Zoom 클론 코딩',
    tags: ['Nuxt 3', 'Vue 3', 'TypeScript'],
    features: [
      'Zoom 클론 코딩',
    ],
  },
  {
    name: '와유(WAU)',
    link: 'https://github.com/HanSeungHyeon/wau',
    desc: 'Zoom 클론 코딩',
    tags: ['Nuxt 3', 'Vue 3', 'TypeScript'],
    features: [
      'Zoom 클론 코딩',
    ],
  },
  {
    name: 'selLF',
    link: 'https://github.com/HanSeungHyeon/selLf',
    desc: '24년도 포트폴리오 사이트',
    tags: ['Spring Boot', 'PostgreSQL', 'Java'],
    features: [
      '24년도 포트폴리오 사이트',
    ],
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

.feat-card__name {
  font-family: var(--font-display);
  font-size: 18px; font-weight: 600;
  color: var(--text); margin-bottom: 8px;
}
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

.modal__title {
  font-family: var(--font-display);
  font-size: 28px;
  font-weight: 700;
  color: var(--text);
  margin-bottom: 12px;
}

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

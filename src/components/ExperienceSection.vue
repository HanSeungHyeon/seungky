<template>
  <section id="experience" class="exp" ref="sectionRef">
    <div :class="['exp__inner', { visible }]">
      <div class="section-tag">Experience</div>

      <div class="exp__list">
        <div
          v-for="(item, i) in experience"
          :key="i"
          class="exp__card"
        >
          <div class="exp__card-header">
            <div>
              <h3 class="exp__role">{{ item.role }}</h3>
              <div class="exp__company">{{ item.company }}</div>
            </div>
            <div class="exp__meta">
              <span class="exp__period">{{ item.period }}</span>
              <span :class="['exp__badge', item.current ? 'exp__badge--active' : '']">
                {{ item.type }}
              </span>
            </div>
          </div>
          <p class="exp__desc">{{ item.desc }}</p>
          <div class="exp__tags">
            <span v-for="t in item.stack" :key="t" class="exp__tag">{{ t }}</span>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const sectionRef = ref(null)
const visible = ref(false)

const experience = [
  {
    period: '2023 — 현재',
    type: '재직 중',
    current: true,
    role: 'Frontend Developer',
    company: 'Tech Company Inc.',
    desc: 'Vue 3 & React 기반 대규모 웹 애플리케이션 개발 및 유지보수. 성능 최적화로 로딩 속도 40% 단축. 디자인 시스템 설계 및 공통 컴포넌트 라이브러리 구축.',
    stack: ['Vue 3', 'React', 'TypeScript', 'Webpack'],
  },
  {
    period: '2021 — 2023',
    type: '풀스택',
    current: false,
    role: 'Full-Stack Developer',
    company: 'Startup Labs',
    desc: 'Node.js + React 풀스택 개발. RESTful API 설계 및 구현. PostgreSQL 데이터베이스 스키마 설계와 쿼리 최적화. AWS 인프라 구성.',
    stack: ['Node.js', 'React', 'PostgreSQL', 'AWS'],
  },
  {
    period: '2020 — 2021',
    type: '첫 커리어',
    current: false,
    role: 'Junior Developer',
    company: 'Web Agency Co.',
    desc: 'Java/Spring Boot 백엔드 개발 및 Vanilla JavaScript 프론트엔드 작업. 다수의 기업 웹사이트 퍼블리싱과 CMS 연동 개발.',
    stack: ['Java', 'Spring Boot', 'JavaScript', 'MySQL'],
  },
]

let observer
onMounted(() => {
  observer = new IntersectionObserver(
    ([entry]) => { if (entry.isIntersecting) visible.value = true },
    { threshold: 0.1 }
  )
  if (sectionRef.value) observer.observe(sectionRef.value)
})
onUnmounted(() => observer?.disconnect())
</script>

<style scoped>
.exp {
  padding: 100px 32px;
  max-width: 1100px;
  margin: 0 auto;
}

.exp__inner {
  opacity: 0;
  transform: translateY(24px);
  transition: opacity .7s var(--ease), transform .7s var(--ease);
}
.exp__inner.visible { opacity: 1; transform: none; }

.section-tag {
  font-family: var(--font-mono);
  font-size: 13px;
  font-weight: 500;
  color: var(--accent);
  margin-bottom: 48px;
  padding-bottom: 16px;
  border-bottom: 2px solid var(--accent);
  display: inline-block;
}

.exp__list {
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.exp__card {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: var(--radius-md);
  padding: 28px 32px;
  transition: all .2s;
}

.exp__card:hover {
  border-color: var(--accent);
  box-shadow: var(--shadow-md);
}

.exp__card-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: 16px;
  gap: 16px;
}

.exp__role {
  font-family: var(--font-display);
  font-size: 20px;
  font-weight: 600;
  color: var(--text);
  margin-bottom: 4px;
}

.exp__company {
  font-size: 14px;
  color: var(--accent);
  font-weight: 500;
}

.exp__meta {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  gap: 6px;
  flex-shrink: 0;
}

.exp__period {
  font-family: var(--font-mono);
  font-size: 12px;
  color: var(--text-muted);
}

.exp__badge {
  font-size: 11px;
  font-weight: 600;
  padding: 3px 10px;
  border-radius: 99px;
  background: var(--border-light);
  color: var(--text-muted);
}

.exp__badge--active {
  background: var(--green-light);
  color: var(--green);
}

.exp__desc {
  font-size: 14px;
  color: var(--text-secondary);
  line-height: 1.7;
  margin-bottom: 16px;
}

.exp__tags { display: flex; flex-wrap: wrap; gap: 6px; }

.exp__tag {
  font-family: var(--font-mono);
  font-size: 12px;
  color: var(--text-muted);
  background: var(--border-light);
  padding: 4px 12px;
  border-radius: 6px;
}

@media (max-width: 900px) {
  .exp { padding: 80px 20px; }
  .exp__card { padding: 20px; }
  .exp__card-header { flex-direction: column; }
  .exp__meta { flex-direction: row; align-items: center; }
}
</style>

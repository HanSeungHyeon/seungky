<template>
  <section id="experience" class="exp" ref="sectionRef">
    <div :class="['exp__inner', { visible }]">
      <div class="sec-label">02 — Experience</div>

      <div class="exp__list">
        <div
          v-for="(item, i) in experience"
          :key="i"
          class="exp__item"
          :style="{ transitionDelay: i * 0.08 + 's' }"
        >
          <div class="exp__meta">
            <span class="exp__period">{{ item.period }}</span>
            <span class="exp__type">{{ item.type }}</span>
          </div>
          <div class="exp__content">
            <h3 class="exp__role">{{ item.role }}</h3>
            <div class="exp__company">{{ item.company }}</div>
            <p class="exp__desc">{{ item.desc }}</p>
            <div class="exp__tags">
              <span v-for="t in item.stack" :key="t" class="exp__tag">{{ t }}</span>
            </div>
          </div>
          <div class="exp__num">{{ String(i + 1).padStart(2, '0') }}</div>
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
    role: 'Frontend Developer',
    company: 'Tech Company Inc.',
    desc: 'Vue 3 & React 기반 대규모 웹 애플리케이션 개발 및 유지보수. 성능 최적화로 로딩 속도 40% 단축. 디자인 시스템 설계 및 공통 컴포넌트 라이브러리 구축.',
    stack: ['Vue 3', 'React', 'TypeScript', 'Webpack'],
  },
  {
    period: '2021 — 2023',
    type: '풀스택',
    role: 'Full-Stack Developer',
    company: 'Startup Labs',
    desc: 'Node.js + React 풀스택 개발. RESTful API 설계 및 구현. PostgreSQL 데이터베이스 스키마 설계와 쿼리 최적화. AWS 인프라 구성.',
    stack: ['Node.js', 'React', 'PostgreSQL', 'AWS'],
  },
  {
    period: '2020 — 2021',
    type: '첫 커리어',
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
  padding: 120px 60px;
  max-width: 1300px;
  margin: 0 auto;
}

.exp__inner {
  opacity: 0;
  transform: translateY(24px);
  transition: opacity .8s var(--ease-out), transform .8s var(--ease-out);
}
.exp__inner.visible { opacity: 1; transform: none; }

.sec-label {
  font-family: var(--font-mono);
  font-size: 11px;
  letter-spacing: .12em;
  text-transform: uppercase;
  color: var(--ink-60);
  margin-bottom: 56px;
  display: flex;
  align-items: center;
  gap: 12px;
}
.sec-label::after {
  content: '';
  flex: 1; height: 1px;
  background: var(--border);
  max-width: 80px;
}

.exp__list { display: flex; flex-direction: column; }

.exp__item {
  display: grid;
  grid-template-columns: 160px 1fr 48px;
  gap: 32px;
  align-items: start;
  padding: 40px 0;
  border-bottom: 1px solid var(--border);
  cursor: default;
  transition: background .2s;
  border-radius: 4px;
}

.exp__item:last-child { border-bottom: none; }

.exp__item:hover { background: var(--white); }
.exp__item:hover .exp__num { opacity: 1; }

.exp__meta { padding-top: 4px; }

.exp__period {
  display: block;
  font-family: var(--font-mono);
  font-size: 12px;
  color: var(--ink-60);
  margin-bottom: 6px;
  letter-spacing: .03em;
}

.exp__type {
  display: inline-block;
  font-size: 11px;
  font-weight: 500;
  color: var(--sage);
  background: var(--sage-soft);
  padding: 3px 10px;
  border-radius: 99px;
  letter-spacing: .03em;
}

.exp__role {
  font-family: var(--font-display);
  font-size: 26px;
  font-weight: 400;
  color: var(--ink);
  letter-spacing: -.01em;
  margin-bottom: 6px;
}

.exp__company {
  font-family: var(--font-mono);
  font-size: 12px;
  color: var(--indigo);
  margin-bottom: 14px;
  letter-spacing: .04em;
}

.exp__desc {
  font-size: 14px;
  color: var(--ink-60);
  line-height: 1.75;
  font-weight: 300;
  margin-bottom: 16px;
  max-width: 560px;
}

.exp__tags { display: flex; flex-wrap: wrap; gap: 6px; }

.exp__tag {
  font-family: var(--font-mono);
  font-size: 11px;
  color: var(--ink-60);
  background: var(--cream);
  border: 1px solid var(--border);
  padding: 3px 10px;
  border-radius: 4px;
  letter-spacing: .03em;
}

.exp__num {
  font-family: var(--font-display);
  font-size: 40px;
  color: var(--border);
  line-height: 1;
  text-align: right;
  opacity: 0;
  transition: opacity .2s;
  padding-top: 4px;
}

@media (max-width: 900px) {
  .exp { padding: 80px 24px; }
  .exp__item { grid-template-columns: 1fr; gap: 12px; }
  .exp__num { display: none; }
}
</style>

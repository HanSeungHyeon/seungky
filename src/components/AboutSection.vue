<template>
  <section id="about" class="about" ref="sectionRef">
    <div :class="['about__inner', { visible }]">
      <div class="sec-label">01 — About</div>

      <div class="about__grid">
        <div class="about__left">
          <h2 class="about__title">
            코드로 아이디어를<br>
            <em>현실로</em> 만듭니다.
          </h2>
          <p class="about__body">
            안녕하세요, <strong>홍길동</strong>입니다. JavaScript와 Java를 중심으로
            프론트엔드부터 백엔드까지 폭넓게 다루는 풀스택 개발자입니다.
          </p>
          <p class="about__body">
            사용자가 진심으로 쓰고 싶어하는 서비스를 만드는 것이 목표입니다.
            코드의 품질과 성능, 그리고 디테일을 중요하게 생각합니다.
          </p>
        </div>

        <div class="about__right">
          <div class="skills">
            <div class="skills__title">기술 스택</div>
            <div
              v-for="skill in skills"
              :key="skill.name"
              class="skill"
            >
              <div class="skill__head">
                <span class="skill__name">{{ skill.name }}</span>
                <span class="skill__pct">{{ skill.pct }}%</span>
              </div>
              <div class="skill__track">
                <div
                  class="skill__fill"
                  :style="{
                    width: visible ? skill.pct + '%' : '0%',
                    background: skill.color,
                    transitionDelay: skill.delay
                  }"
                ></div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Tag cloud -->
      <div class="tags">
        <span v-for="t in tags" :key="t" class="tag">{{ t }}</span>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const sectionRef = ref(null)
const visible = ref(false)

const skills = [
  { name: 'JavaScript', pct: 92, color: 'var(--indigo)', delay: '0s' },
  { name: 'Vue 3 / React', pct: 88, color: '#6B8F71', delay: '.1s' },
  { name: 'Java', pct: 82, color: '#3A7CA5', delay: '.2s' },
  { name: 'Node.js', pct: 76, color: 'var(--indigo)', delay: '.3s' },
  { name: 'TypeScript', pct: 71, color: '#6B8F71', delay: '.4s' },
  { name: 'Spring Boot', pct: 65, color: '#3A7CA5', delay: '.5s' },
]

const tags = [
  'Vue 3', 'React', 'JavaScript', 'TypeScript', 'Java',
  'Spring Boot', 'Node.js', 'REST API', 'Git', 'MySQL',
  'PostgreSQL', 'MongoDB', 'Docker', 'CI/CD', 'Figma',
]

let observer
onMounted(() => {
  observer = new IntersectionObserver(
    ([entry]) => { if (entry.isIntersecting) visible.value = true },
    { threshold: 0.15 }
  )
  if (sectionRef.value) observer.observe(sectionRef.value)
})
onUnmounted(() => observer?.disconnect())
</script>

<style scoped>
.about {
  padding: 120px 60px;
  max-width: 1300px;
  margin: 0 auto;
}

.about__inner {
  opacity: 0;
  transform: translateY(32px);
  transition: opacity .8s var(--ease-out), transform .8s var(--ease-out);
}

.about__inner.visible {
  opacity: 1;
  transform: none;
}

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
  flex: 1;
  height: 1px;
  background: var(--border);
  max-width: 80px;
}

.about__grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 80px;
  margin-bottom: 64px;
}

.about__title {
  font-family: var(--font-display);
  font-size: clamp(32px, 4vw, 52px);
  font-weight: 400;
  letter-spacing: -.02em;
  line-height: 1.15;
  color: var(--ink);
  margin-bottom: 28px;
}

.about__title em {
  color: var(--indigo);
  font-style: italic;
}

.about__body {
  font-size: 16px;
  color: var(--ink-60);
  line-height: 1.85;
  font-weight: 300;
  margin-bottom: 16px;
}

.about__body strong { color: var(--ink); font-weight: 500; }

.skills__title {
  font-family: var(--font-mono);
  font-size: 11px;
  letter-spacing: .1em;
  text-transform: uppercase;
  color: var(--ink-60);
  margin-bottom: 28px;
}

.skill { margin-bottom: 20px; }

.skill__head {
  display: flex;
  justify-content: space-between;
  margin-bottom: 8px;
}

.skill__name { font-size: 14px; font-weight: 500; color: var(--ink); }
.skill__pct  { font-family: var(--font-mono); font-size: 12px; color: var(--ink-60); }

.skill__track {
  height: 2px;
  background: var(--border);
  border-radius: 99px;
  overflow: hidden;
}

.skill__fill {
  height: 100%;
  border-radius: 99px;
  transition: width 1.4s var(--ease-out);
}

/* Tag cloud */
.tags {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  padding-top: 48px;
  border-top: 1px solid var(--border);
}

.tag {
  font-family: var(--font-mono);
  font-size: 12px;
  color: var(--ink-60);
  background: var(--white);
  border: 1px solid var(--border);
  padding: 5px 14px;
  border-radius: 99px;
  letter-spacing: .03em;
  transition: all .18s;
}

.tag:hover {
  background: var(--indigo-soft);
  border-color: var(--indigo);
  color: var(--indigo);
}

@media (max-width: 900px) {
  .about { padding: 80px 24px; }
  .about__grid { grid-template-columns: 1fr; gap: 48px; }
}
</style>

<template>
  <section id="about" class="about" ref="sectionRef">
    <div :class="['about__inner', { visible }]">
      <div class="about__grid">
        <div class="about__left">
          <h3 class="col-title">PROFILE</h3>
          <h2 class="profile__name">한승현</h2>

          <ul class="profile__info">
            <li>1996.04.18 / 서울시 동작구</li>
            <li>tmdgus4720@naver.com</li>
          </ul>

          <div class="profile__edu">
            <h3 class="col-title">EDUCATION</h3>
            <ul class="edu-list">
              <li v-for="edu in education" :key="edu.name" class="edu-item">
                <span class="edu-name">{{ edu.name }}</span>
                <span class="edu-year">{{ edu.year }}</span>
              </li>
            </ul>
          </div>
        </div>

        <div class="about__right">
          <div class="right-block">
            <h3 class="col-title">SKILL</h3>
            <div class="skill-list">
              <div v-for="skill in skills" :key="skill.name" class="skill">
                <span class="skill__name">{{ skill.name }}</span>
                <div class="skill__track">
                  <div
                    class="skill__fill"
                    :style="{ width: visible ? skill.pct + '%' : '0%' }"
                  ></div>
                </div>
              </div>
            </div>
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

const education = [
  { name: '한양사이버대학교 응용소프트웨어학과 졸업', year: '2026' },
  { name: '연암대학교 동물보호계열 졸업', year: '2020' },
  { name: '천안 두정고등학교 졸업', year: '2015' },
]

const skills = [
  { name: 'JAVA', pct: 95 },
  { name: 'SPRING BOOT', pct: 90 },
  { name: 'MYSQL', pct: 85 },
  { name: 'JAVASCRIPT', pct: 82 },
  { name: 'ORACLE', pct: 72 },
  { name: 'NODE.JS', pct: 70 },
  { name: 'VUE', pct: 70 },
  { name: 'POSTGRESQL', pct: 65 },
  { name: 'AWS', pct: 60 },
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
  padding: 64px 32px;
  max-width: 1100px;
  margin: 0 auto;
}

.about__inner {
  opacity: 0;
  transform: translateY(24px);
  transition: opacity .7s var(--ease), transform .7s var(--ease);
}
.about__inner.visible { opacity: 1; transform: none; }

.about__grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 80px;
}

.col-title {
  font-family: var(--font-display);
  font-size: 14px;
  font-weight: 700;
  color: var(--accent);
  letter-spacing: 0.08em;
  margin-bottom: 24px;
}

/* ── Profile (Left) ── */
.profile__name {
  font-family: var(--font-display);
  font-size: 28px;
  font-weight: 700;
  color: var(--text);
  margin-bottom: 20px;
}

.profile__info {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 6px;
  margin-bottom: 28px;
  padding-bottom: 28px;
  border-bottom: 1px solid var(--border);
}

.profile__info li {
  font-size: 14px;
  color: var(--text-secondary);
  line-height: 1.6;
}

/* Education */
.edu-list {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.edu-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 12px;
}

.edu-name {
  font-size: 14px;
  color: var(--text);
  font-weight: 500;
}

.edu-year {
  font-family: var(--font-mono);
  font-size: 12px;
  color: var(--text-muted);
  flex-shrink: 0;
}

/* ── Right Column ── */
.right-block {
  margin-bottom: 40px;
}
.right-block:last-child { margin-bottom: 0; }

/* Skill */
.skill-list {
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.skill {
  display: grid;
  grid-template-columns: 120px 1fr;
  align-items: center;
  gap: 16px;
}

.skill__name {
  font-family: var(--font-mono);
  font-size: 12px;
  font-weight: 500;
  color: var(--text);
  letter-spacing: 0.02em;
}

.skill__track {
  height: 8px;
  background: var(--border-light);
  border-radius: 99px;
  overflow: hidden;
}

.skill__fill {
  height: 100%;
  border-radius: 99px;
  background: var(--accent);
  transition: width 1.2s var(--ease);
}

@media (max-width: 900px) {
  .about { padding: 48px 20px; }
  .about__grid {
    grid-template-columns: 1fr;
    gap: 56px;
  }
  .skill { grid-template-columns: 100px 1fr; }
}
</style>

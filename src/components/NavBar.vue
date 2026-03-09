<template>
  <nav :class="['nav', { 'nav--scrolled': scrolled }]">
    <a href="#home" class="nav__logo">홍길동</a>
    <ul class="nav__links">
      <li v-for="item in links" :key="item.id">
        <a :href="`#${item.id}`" :class="['nav__link', { active: active === item.id }]">
          {{ item.label }}
        </a>
      </li>
    </ul>
    <a href="mailto:hello@example.com" class="nav__cta">연락하기</a>
  </nav>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const scrolled = ref(false)
const active = ref('home')

const links = [
  { id: 'about',      label: 'About' },
  { id: 'experience', label: '경력' },
  { id: 'projects',   label: '프로젝트' },
  { id: 'contact',    label: 'Contact' },
]

function onScroll() {
  scrolled.value = window.scrollY > 40

  const sections = ['home', 'about', 'experience', 'projects', 'contact']
  for (const id of [...sections].reverse()) {
    const el = document.getElementById(id)
    if (el && window.scrollY >= el.offsetTop - 120) {
      active.value = id
      break
    }
  }
}

onMounted(() => window.addEventListener('scroll', onScroll, { passive: true }))
onUnmounted(() => window.removeEventListener('scroll', onScroll))
</script>

<style scoped>
.nav {
  position: fixed;
  top: 0; left: 0; right: 0;
  z-index: 100;
  display: flex;
  align-items: center;
  gap: 48px;
  padding: 28px 60px;
  transition: padding .4s var(--ease-out), background .4s, box-shadow .4s;
}

.nav--scrolled {
  padding: 16px 60px;
  background: rgba(250, 248, 244, 0.92);
  backdrop-filter: blur(16px);
  box-shadow: 0 1px 0 var(--border);
}

.nav__logo {
  font-family: var(--font-display);
  font-size: 20px;
  color: var(--ink);
  letter-spacing: -.01em;
  margin-right: auto;
}

.nav__links {
  display: flex;
  gap: 36px;
}

.nav__link {
  font-size: 14px;
  font-weight: 400;
  color: var(--ink-60);
  letter-spacing: .01em;
  transition: color .2s;
  position: relative;
}

.nav__link::after {
  content: '';
  position: absolute;
  left: 0; right: 0; bottom: -3px;
  height: 1px;
  background: var(--indigo);
  transform: scaleX(0);
  transform-origin: left;
  transition: transform .25s var(--ease-out);
}

.nav__link:hover,
.nav__link.active {
  color: var(--ink);
}

.nav__link.active::after,
.nav__link:hover::after {
  transform: scaleX(1);
}

.nav__cta {
  font-size: 13px;
  font-weight: 500;
  color: var(--white);
  background: var(--ink);
  padding: 9px 20px;
  border-radius: 6px;
  letter-spacing: .01em;
  transition: background .2s, transform .2s;
}

.nav__cta:hover {
  background: var(--indigo);
  transform: translateY(-1px);
}

@media (max-width: 768px) {
  .nav { padding: 20px 24px; gap: 24px; }
  .nav--scrolled { padding: 14px 24px; }
  .nav__links { display: none; }
}
</style>

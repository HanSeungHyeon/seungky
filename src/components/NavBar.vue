<template>
  <nav :class="['nav', { 'nav--scrolled': scrolled }]">
    <div class="nav__inner">
      <a href="#home" class="nav__logo">승카이</a>
      <ul class="nav__links">
        <li v-for="item in links" :key="item.id">
          <a
            :href="`#${item.id}`"
            :class="['nav__link', { active: active === item.id }]"
            @click="setActive(item.id)"
          >
            {{ item.label }}
          </a>
        </li>
      </ul>
    </div>
  </nav>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const scrolled = ref(false)
const active = ref('home')

const links = [
  { id: 'about',    label: 'About' },
  { id: 'projects', label: 'Projects' },
  { id: 'contact',  label: 'Contact' },
]

function setActive(id) {
  active.value = id
}

function onScroll() {
  scrolled.value = window.scrollY > 40

  const docEl = document.documentElement
  const scrollBottom = window.innerHeight + window.scrollY
  const docHeight = docEl.scrollHeight

  // 거의 페이지 맨 아래에 도달했을 때는 무조건 contact 활성화
  if (scrollBottom >= docHeight - 4) {
    active.value = 'contact'
    return
  }

  const sectionIds = ['home', 'about', 'projects', 'contact']
  let current = 'home'

  for (const id of sectionIds) {
    const el = document.getElementById(id)
    if (!el) continue
    const rect = el.getBoundingClientRect()
    if (rect.top <= 160) {
      current = id
    }
  }

  active.value = current
}

onMounted(() => {
  window.addEventListener('scroll', onScroll, { passive: true })
  onScroll()
})
onUnmounted(() => window.removeEventListener('scroll', onScroll))
</script>

<style scoped>
.nav {
  position: fixed;
  top: 0; left: 0; right: 0;
  z-index: 100;
  transition: all .3s var(--ease);
}

.nav__inner {
  max-width: 1100px;
  margin: 0 auto;
  padding: 20px 32px;
  display: flex;
  align-items: center;
  gap: 40px;
  transition: padding .3s var(--ease);
}

.nav--scrolled {
  background: rgba(255, 255, 255, 0.85);
  backdrop-filter: blur(20px);
  border-bottom: 1px solid var(--border);
}

.nav--scrolled .nav__inner {
  padding: 14px 32px;
}

.nav__logo {
  font-family: var(--font-display);
  font-size: 18px;
  font-weight: 800;
  color: var(--accent);
  margin-right: auto;
  letter-spacing: -0.02em;
}

.nav__links { display: flex; gap: 32px; }

.nav__link {
  font-size: 14px;
  font-weight: 500;
  color: var(--text-muted);
  transition: color .2s;
}

.nav__link:hover,
.nav__link.active {
  color: var(--text);
}

.nav__cta {
  font-size: 13px;
  font-weight: 600;
  color: var(--accent);
  border: 1.5px solid var(--accent);
  padding: 7px 18px;
  border-radius: 99px;
  transition: all .2s;
}

.nav__cta:hover {
  background: var(--accent);
  color: white;
}

@media (max-width: 768px) {
  .nav__inner { padding: 16px 20px; gap: 20px; }
  .nav--scrolled .nav__inner { padding: 12px 20px; }
  .nav__links { display: none; }
}
</style>

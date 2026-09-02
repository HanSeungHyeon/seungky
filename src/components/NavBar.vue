<template>
  <nav :class="['nav', { 'nav--scrolled': scrolled || menuOpen }]">
    <div class="nav__inner">
      <a href="#home" class="nav__logo" @click="closeMenu">승카이</a>

      <button
        class="nav__toggle"
        :aria-expanded="menuOpen"
        aria-label="메뉴 열기/닫기"
        @click="menuOpen = !menuOpen"
      >
        <span :class="['nav__toggle-bar', { open: menuOpen }]"></span>
        <span :class="['nav__toggle-bar', { open: menuOpen }]"></span>
        <span :class="['nav__toggle-bar', { open: menuOpen }]"></span>
      </button>

      <ul :class="['nav__links', { 'nav__links--open': menuOpen }]">
        <li v-for="item in links" :key="item.id">
          <a
            :href="`#${item.id}`"
            :class="['nav__link', { active: active === item.id }]"
            @click="onLinkClick(item.id)"
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
const menuOpen = ref(false)

const links = [
  { id: 'about',    label: 'About' },
  { id: 'projects', label: 'Projects' },
  { id: 'contact',  label: 'Contact' },
]

function onLinkClick(id) {
  active.value = id
  closeMenu()
}

function closeMenu() {
  menuOpen.value = false
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

/* ── Hamburger ── */
.nav__toggle {
  display: none;
  flex-direction: column;
  justify-content: center;
  gap: 5px;
  width: 40px;
  height: 40px;
  padding: 8px;
  border: none;
  background: transparent;
  cursor: pointer;
}

.nav__toggle-bar {
  display: block;
  width: 100%;
  height: 2px;
  background: var(--text);
  border-radius: 2px;
  transition: transform .25s var(--ease), opacity .25s var(--ease);
}

.nav__toggle-bar.open:nth-child(1) { transform: translateY(7px) rotate(45deg); }
.nav__toggle-bar.open:nth-child(2) { opacity: 0; }
.nav__toggle-bar.open:nth-child(3) { transform: translateY(-7px) rotate(-45deg); }

@media (max-width: 768px) {
  .nav__inner { padding: 16px 20px; gap: 20px; }
  .nav--scrolled .nav__inner { padding: 12px 20px; }

  .nav__toggle { display: flex; }

  .nav__links {
    position: absolute;
    top: 100%;
    left: 0;
    right: 0;
    flex-direction: column;
    gap: 0;
    background: rgba(255, 255, 255, 0.95);
    backdrop-filter: blur(20px);
    border-bottom: 1px solid var(--border);
    padding: 8px 20px 16px;
    transform: translateY(-8px);
    opacity: 0;
    pointer-events: none;
    transition: transform .25s var(--ease), opacity .25s var(--ease);
  }

  .nav__links--open {
    transform: translateY(0);
    opacity: 1;
    pointer-events: auto;
  }

  .nav__link {
    display: block;
    padding: 14px 0;
    font-size: 15px;
  }

  .nav__links li + li .nav__link {
    border-top: 1px solid var(--border-light);
  }
}
</style>

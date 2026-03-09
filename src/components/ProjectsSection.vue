<template>
  <section id="projects" class="projects" ref="sectionRef">
    <div :class="['projects__inner', { visible }]">
      <div class="projects__header">
        <div class="sec-label">03 — Projects</div>
        <div class="github-status">
          <span :class="['status-dot', reposLoaded ? 'ok' : 'loading']"></span>
          <span class="status-text">{{ statusText }}</span>
        </div>
      </div>

      <!-- Featured projects -->
      <div class="featured">
        <a
          v-for="(p, i) in featured"
          :key="i"
          :href="p.link"
          target="_blank"
          class="feat-card"
          :style="{ transitionDelay: i * 0.1 + 's' }"
        >
          <div class="feat-card__top">
            <span class="feat-card__emoji">{{ p.emoji }}</span>
            <span class="feat-card__arrow">↗</span>
          </div>
          <h3 class="feat-card__name">{{ p.name }}</h3>
          <p class="feat-card__desc">{{ p.desc }}</p>
          <div class="feat-card__tags">
            <span v-for="t in p.tags" :key="t" class="feat-card__tag">{{ t }}</span>
          </div>
        </a>
      </div>

      <!-- GitHub Repos -->
      <div class="repos-block">
        <div class="repos-header">
          <span class="repos-title">GitHub 공개 저장소</span>
          <a :href="`https://github.com/${GITHUB_USERNAME}`" target="_blank" class="repos-link">
            전체 보기 →
          </a>
        </div>

        <div v-if="reposError" class="repos-notice repos-notice--warn">
          ⚠️ <code>GITHUB_USERNAME</code>을 본인 아이디로 변경해주세요.
        </div>

        <div v-else class="repos-grid">
          <template v-if="repos.length">
            <a
              v-for="repo in repos"
              :key="repo.id"
              :href="repo.html_url"
              target="_blank"
              class="repo-card"
            >
              <div class="repo-card__name">{{ repo.name }}</div>
              <div class="repo-card__desc">{{ repo.description || '설명 없음' }}</div>
              <div class="repo-card__foot">
                <span v-if="repo.language" class="repo-card__lang">
                  <i class="lang-dot" :style="{ background: langColor(repo.language) }"></i>
                  {{ repo.language }}
                </span>
                <span class="repo-card__stat">★ {{ repo.stargazers_count }}</span>
                <span class="repo-card__stat">⑂ {{ repo.forks_count }}</span>
              </div>
            </a>
          </template>
          <template v-else>
            <div class="repos-loading">
              <span class="spinner"></span> 불러오는 중...
            </div>
          </template>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const GITHUB_USERNAME = 'hanseunghyeon'

const sectionRef  = ref(null)
const visible     = ref(false)
const repos       = ref([])
const reposLoaded = ref(false)
const reposError  = ref(false)
const statusText  = ref('GitHub 연결 중...')

const featured = [
  {
    emoji: '🛒',
    name: 'ShopFlow',
    link: '#',
    desc: 'Vue 3 + Node.js 풀스택 이커머스. 실시간 재고 관리, Stripe 결제, 관리자 대시보드.',
    tags: ['Vue 3', 'Node.js', 'MongoDB', 'Stripe'],
  },
  {
    emoji: '📊',
    name: 'DataVis',
    link: '#',
    desc: 'D3.js 인터랙티브 데이터 시각화 대시보드. WebSocket 실시간 스트리밍 지원.',
    tags: ['D3.js', 'React', 'WebSocket', 'Redis'],
  },
  {
    emoji: '🤖',
    name: 'ChatBot API',
    link: '#',
    desc: 'Spring Boot 기반 AI 챗봇 백엔드. REST + WebSocket 하이브리드 아키텍처.',
    tags: ['Spring Boot', 'Java', 'PostgreSQL'],
  },
]

const LANG_COLORS = {
  JavaScript: '#d4a82a', TypeScript: '#3178c6', Java: '#b07219',
  Python: '#3572a5', HTML: '#c0432a', CSS: '#563d7c',
  Vue: '#42b883', Go: '#00add8', Rust: '#a86132', Kotlin: '#7f52ff',
}

function langColor(lang) {
  return LANG_COLORS[lang] || '#999'
}

async function loadRepos() {
  if (GITHUB_USERNAME === 'YOUR_USERNAME') {
    reposError.value = true
    statusText.value = 'username 미설정'
    return
  }
  try {
    const res = await fetch(
      `https://api.github.com/users/${GITHUB_USERNAME}/repos?sort=stars&per_page=9&type=public`
    )
    if (!res.ok) throw new Error()
    const data = await res.json()
    repos.value = data
    reposLoaded.value = true
    statusText.value = `${data.length}개 저장소 연결됨`
  } catch {
    statusText.value = 'GitHub 연결 실패'
    reposError.value = true
  }
}

let observer
onMounted(() => {
  loadRepos()
  observer = new IntersectionObserver(
    ([entry]) => { if (entry.isIntersecting) visible.value = true },
    { threshold: 0.05 }
  )
  if (sectionRef.value) observer.observe(sectionRef.value)
})
onUnmounted(() => observer?.disconnect())
</script>

<style scoped>
.projects {
  padding: 120px 60px;
  max-width: 1300px;
  margin: 0 auto;
}

.projects__inner {
  opacity: 0;
  transform: translateY(24px);
  transition: opacity .8s var(--ease-out), transform .8s var(--ease-out);
}
.projects__inner.visible { opacity: 1; transform: none; }

.projects__header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 56px;
}

.sec-label {
  font-family: var(--font-mono);
  font-size: 11px;
  letter-spacing: .12em;
  text-transform: uppercase;
  color: var(--ink-60);
  display: flex;
  align-items: center;
  gap: 12px;
}
.sec-label::after {
  content: '';
  width: 80px; height: 1px;
  background: var(--border);
}

.github-status {
  display: flex;
  align-items: center;
  gap: 8px;
}

.status-dot {
  width: 7px; height: 7px;
  border-radius: 50%;
}

.status-dot.ok { background: var(--sage); }
.status-dot.loading {
  background: #d4a82a;
  animation: blink 1.4s ease-in-out infinite;
}

@keyframes blink { 0%,100%{opacity:1} 50%{opacity:.3} }

.status-text {
  font-family: var(--font-mono);
  font-size: 11px;
  color: var(--ink-60);
  letter-spacing: .05em;
}

.featured {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 16px;
  margin-bottom: 64px;
}

.feat-card {
  background: var(--white);
  border: 1px solid var(--border);
  border-radius: 14px;
  padding: 28px;
  display: block;
  transition: all .25s var(--ease-out);
  cursor: pointer;
}

.feat-card:hover {
  border-color: var(--indigo);
  transform: translateY(-4px);
  box-shadow: 0 16px 40px rgba(45,58,140,.08);
}

.feat-card__top {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: 16px;
}

.feat-card__emoji { font-size: 26px; }

.feat-card__arrow {
  font-size: 18px;
  color: var(--ink-30);
  transition: color .2s, transform .2s;
}

.feat-card:hover .feat-card__arrow {
  color: var(--indigo);
  transform: translate(2px, -2px);
}

.feat-card__name {
  font-family: var(--font-display);
  font-size: 22px;
  font-weight: 400;
  color: var(--ink);
  margin-bottom: 10px;
  letter-spacing: -.01em;
}

.feat-card__desc {
  font-size: 13px;
  color: var(--ink-60);
  line-height: 1.65;
  margin-bottom: 20px;
  font-weight: 300;
}

.feat-card__tags { display: flex; flex-wrap: wrap; gap: 6px; }

.feat-card__tag {
  font-family: var(--font-mono);
  font-size: 10px;
  color: var(--indigo);
  background: var(--indigo-soft);
  padding: 3px 10px;
  border-radius: 99px;
  letter-spacing: .03em;
}

.repos-block { margin-bottom: 64px; }

.repos-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-bottom: 20px;
  border-bottom: 1px solid var(--border);
  margin-bottom: 20px;
}

.repos-title {
  font-family: var(--font-mono);
  font-size: 12px;
  color: var(--ink-60);
  letter-spacing: .08em;
  text-transform: uppercase;
}

.repos-link {
  font-family: var(--font-mono);
  font-size: 12px;
  color: var(--indigo);
  transition: opacity .2s;
}
.repos-link:hover { opacity: .7; }

.repos-notice {
  font-family: var(--font-mono);
  font-size: 13px;
  padding: 20px;
  border-radius: 8px;
  color: #92660a;
  background: #fef9ec;
  border: 1px solid #f0d88a;
}

.repos-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(270px, 1fr));
  gap: 12px;
}

.repo-card {
  background: var(--white);
  border: 1px solid var(--border);
  border-radius: 10px;
  padding: 20px;
  display: block;
  transition: all .2s;
  cursor: pointer;
}

.repo-card:hover {
  border-color: var(--ink-30);
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(0,0,0,.05);
}

.repo-card__name {
  font-weight: 500;
  font-size: 14px;
  color: var(--indigo);
  margin-bottom: 6px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.repo-card__desc {
  font-size: 12px;
  color: var(--ink-60);
  line-height: 1.5;
  margin-bottom: 14px;
  font-weight: 300;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.repo-card__foot {
  display: flex;
  gap: 12px;
  align-items: center;
}

.repo-card__lang {
  display: flex;
  align-items: center;
  gap: 5px;
  font-family: var(--font-mono);
  font-size: 11px;
  color: var(--ink-60);
}

.lang-dot {
  width: 8px; height: 8px;
  border-radius: 50%;
  flex-shrink: 0;
}

.repo-card__stat {
  font-family: var(--font-mono);
  font-size: 11px;
  color: var(--ink-60);
}

.repos-loading {
  grid-column: 1/-1;
  text-align: center;
  padding: 48px;
  font-family: var(--font-mono);
  font-size: 12px;
  color: var(--ink-60);
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
}

.spinner {
  width: 16px; height: 16px;
  border: 2px solid var(--border);
  border-top-color: var(--indigo);
  border-radius: 50%;
  animation: spin 1s linear infinite;
}

@keyframes spin { to { transform: rotate(360deg); } }

@media (max-width: 900px) {
  .projects { padding: 80px 24px; }
  .featured { grid-template-columns: 1fr; }
  .projects__header { flex-direction: column; align-items: flex-start; gap: 16px; }
}
</style>

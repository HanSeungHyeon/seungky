<template>
  <section id="contact" class="contact" ref="sectionRef">
    <div :class="['contact__inner', { visible }]">
      <div class="section-tag">Contact</div>

      <div class="contact__grid">
        <div class="contact__left">
          <h2 class="contact__title">
            같이 만들고<br>싶은 게 있나요?
          </h2>
          <p class="contact__body">
            새로운 기회나 협업 제안에 항상 열려 있습니다.<br>
            편하게 연락해 주세요.
          </p>
          <div class="contact__links">
            <template v-for="link in links" :key="link.label">
              <button
                v-if="link.copy"
                type="button"
                class="contact__link contact__link--copy"
                @click="copyEmail(link.text)"
              >
                <span class="contact__link-label">{{ link.label }}</span>
                <span class="contact__link-sep">·</span>
                <span class="contact__link-text">{{ link.text }}</span>
                <span class="contact__link-copied" :class="{ show: copied }">{{ copied ? '복사됨!' : '클릭하면 복사' }}</span>
              </button>
              <a
                v-else
                :href="link.href"
                :target="link.external ? '_blank' : undefined"
                class="contact__link"
              >
                <span class="contact__link-label">{{ link.label }}</span>
                <span class="contact__link-sep">·</span>
                <span class="contact__link-text">{{ link.text }}</span>
              </a>
            </template>
          </div>
        </div>

        <div class="contact__right">
          <div class="code-card">
            <div class="code-card__bar">
              <span class="code-dot"></span><span class="code-dot"></span><span class="code-dot"></span>
              <span class="code-card__file">contact.js</span>
            </div>
            <pre class="code-card__body"><span class="c-k">const</span> <span class="c-v">developer</span> = {
  <span class="c-p">name</span>:     <span class="c-s">'한승현'</span>,
  <span class="c-p">role</span>:     <span class="c-s">'Full-Stack Dev'</span>,
  <span class="c-p">mbti</span>:     <span class="c-s">'ISFJ'</span>,
  <span class="c-p">stack</span>:    [<span class="c-s">'Java'</span>, <span class="c-s">'Spring'</span>, <span class="c-s">'Vue'</span>, <span class="c-s">'Nuxt'</span>, <span class="c-s">'Node.js'</span>, <span class="c-s">'Mysql'</span>],
  <span class="c-p">location</span>: <span class="c-s">'Seoul, KR'</span>,
}</pre>
          </div>

          <div class="availability">
            <span class="avail-dot"></span>
            언제든 새로운 기회를 맞이할 준비가 되어있습니다.
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
const copied = ref(false)

const links = [
  { label: 'Email', text: 'tmdgus4720@naver.com', copy: true },
  { label: 'GitHub', text: 'github.com/hanseunghyeon', href: 'https://github.com/hanseunghyeon', external: true },
  { label: 'velog', text: 'velog.io/@tmdgus4720/posts', href: 'https://velog.io/@tmdgus4720/posts', external: true },
]

let copiedTimer
async function copyEmail(email) {
  try {
    await navigator.clipboard.writeText(email)
  } catch {
    const ta = document.createElement('textarea')
    ta.value = email
    ta.style.position = 'fixed'
    ta.style.opacity = '0'
    document.body.appendChild(ta)
    ta.select()
    document.execCommand('copy')
    document.body.removeChild(ta)
  }
  copied.value = true
  clearTimeout(copiedTimer)
  copiedTimer = setTimeout(() => { copied.value = false }, 1600)
}

let observer
onMounted(() => {
  observer = new IntersectionObserver(
    ([entry]) => { if (entry.isIntersecting) visible.value = true },
    { threshold: 0.2 }
  )
  if (sectionRef.value) observer.observe(sectionRef.value)
})
onUnmounted(() => {
  observer?.disconnect()
  clearTimeout(copiedTimer)
})
</script>

<style scoped>
.contact {
  padding: 64px 32px;
  max-width: 1100px;
  margin: 0 auto;
}

.contact__inner {
  opacity: 0;
  transform: translateY(24px);
  transition: opacity .7s var(--ease), transform .7s var(--ease);
}
.contact__inner.visible { opacity: 1; transform: none; }

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

.contact__grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 80px;
  align-items: start;
}

.contact__title {
  font-family: var(--font-display);
  font-size: clamp(32px, 5vw, 48px);
  font-weight: 700;
  letter-spacing: -0.02em;
  line-height: 1.2;
  color: var(--text);
  margin-bottom: 20px;
}

.contact__body {
  font-size: 15px;
  color: var(--text-secondary);
  line-height: 1.8;
  margin-bottom: 36px;
}

.contact__links {
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.contact__link {
  font-size: 14px;
  color: var(--text-secondary);
  text-decoration: none;
}

.contact__link:hover {
  color: var(--accent);
}

.contact__link--copy {
  display: inline-flex;
  align-items: center;
  align-self: flex-start;
  padding: 0;
  border: none;
  background: none;
  font: inherit;
  cursor: pointer;
}

.contact__link-copied {
  margin-left: 8px;
  font-family: var(--font-mono);
  font-size: 11px;
  color: var(--text-muted);
  opacity: 0;
  transition: opacity .2s;
}

.contact__link--copy:hover .contact__link-copied,
.contact__link-copied.show {
  opacity: 1;
}

.contact__link-copied.show {
  color: var(--green);
}

.contact__link-label {
  font-weight: 600;
  color: var(--text);
}

.contact__link-sep {
  margin: 0 4px;
  color: var(--text-muted);
}

.contact__link-text {
  font-family: var(--font-mono);
}

.code-card {
  background: #1e293b;
  border-radius: var(--radius-md);
  overflow: hidden;
  margin-bottom: 16px;
  box-shadow: var(--shadow-lg);
}

.code-card__bar {
  display: flex;
  align-items: center;
  gap: 6px;
  padding: 12px 16px;
  background: rgba(255,255,255,.04);
  border-bottom: 1px solid rgba(255,255,255,.06);
}

.code-dot {
  width: 10px; height: 10px;
  border-radius: 50%;
  background: rgba(255,255,255,.1);
}

.code-card__file {
  font-family: var(--font-mono);
  font-size: 12px;
  color: rgba(255,255,255,.3);
  margin-left: 6px;
}

.code-card__body {
  font-family: var(--font-mono);
  font-size: 13px;
  color: rgba(255,255,255,.5);
  padding: 20px;
  line-height: 2;
  white-space: pre;
}

.c-k { color: #c792ea; }
.c-v { color: #82aaff; }
.c-p { color: #7FD0DA; }
.c-s { color: #C3E88D; }

.availability {
  display: flex;
  align-items: center;
  gap: 8px;
  font-size: 13px;
  color: var(--text-secondary);
}

.avail-dot {
  width: 8px; height: 8px;
  border-radius: 50%;
  background: var(--green);
  animation: pulse 2s ease-in-out infinite;
}

@keyframes pulse {
  0%,100% { opacity: 1; transform: scale(1); }
  50% { opacity: .4; transform: scale(.8); }
}

@media (max-width: 900px) {
  .contact { padding: 48px 20px; }
  .contact__grid { grid-template-columns: 1fr; gap: 48px; }
}
</style>

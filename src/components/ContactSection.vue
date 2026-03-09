<template>
  <section id="contact" class="contact" ref="sectionRef">
    <div :class="['contact__inner', { visible }]">
      <div class="sec-label">04 — Contact</div>

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
            <a
              v-for="link in links"
              :key="link.label"
              :href="link.href"
              :target="link.external ? '_blank' : undefined"
              class="contact__link"
            >
              <span class="contact__link-icon">{{ link.icon }}</span>
              <span class="contact__link-text">{{ link.label }}</span>
              <span class="contact__link-arrow">→</span>
            </a>
          </div>
        </div>

        <div class="contact__right">
          <div class="code-snippet">
            <div class="code-snippet__bar">
              <span class="dot"></span><span class="dot"></span><span class="dot"></span>
              <span class="code-snippet__file">contact.js</span>
            </div>
            <pre class="code-snippet__body"><span class="c-k">const</span> <span class="c-v">me</span> = {
  <span class="c-p">name</span>:         <span class="c-s">'홍길동'</span>,
  <span class="c-p">role</span>:         <span class="c-s">'Full-Stack Dev'</span>,
  <span class="c-p">stack</span>:        [<span class="c-s">'JS'</span>, <span class="c-s">'Java'</span>, <span class="c-s">'Vue'</span>],
  <span class="c-p">open_to_work</span>: <span class="c-k">true</span>,
  <span class="c-p">location</span>:     <span class="c-s">'Seoul, KR'</span>,
  <span class="c-p">coffee</span>:       <span class="c-s">'always ☕'</span>,
}</pre>
          </div>

          <div class="availability">
            <span class="avail-dot"></span>
            현재 새로운 기회를 찾고 있습니다
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

const links = [
  { icon: '✉', label: 'hello@example.com', href: 'mailto:hello@example.com' },
  { icon: '⟨/⟩', label: 'github.com/YOUR_USERNAME', href: 'https://github.com/YOUR_USERNAME', external: true },
  { icon: 'in', label: 'linkedin.com/in/YOUR_USERNAME', href: 'https://linkedin.com/in/YOUR_USERNAME', external: true },
]

let observer
onMounted(() => {
  observer = new IntersectionObserver(
    ([entry]) => { if (entry.isIntersecting) visible.value = true },
    { threshold: 0.2 }
  )
  if (sectionRef.value) observer.observe(sectionRef.value)
})
onUnmounted(() => observer?.disconnect())
</script>

<style scoped>
.contact {
  padding: 120px 60px 80px;
  max-width: 1300px;
  margin: 0 auto;
}

.contact__inner {
  opacity: 0;
  transform: translateY(24px);
  transition: opacity .8s var(--ease-out), transform .8s var(--ease-out);
}
.contact__inner.visible { opacity: 1; transform: none; }

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
  width: 80px; height: 1px;
  background: var(--border);
}

.contact__grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 80px;
  align-items: center;
}

.contact__title {
  font-family: var(--font-display);
  font-size: clamp(36px, 5vw, 60px);
  font-weight: 400;
  letter-spacing: -.02em;
  line-height: 1.1;
  color: var(--ink);
  margin-bottom: 24px;
}

.contact__body {
  font-size: 16px;
  color: var(--ink-60);
  line-height: 1.75;
  font-weight: 300;
  margin-bottom: 40px;
}

.contact__links { display: flex; flex-direction: column; gap: 4px; }

.contact__link {
  display: flex;
  align-items: center;
  gap: 14px;
  padding: 16px;
  border-radius: 10px;
  border: 1px solid transparent;
  transition: all .2s;
  cursor: pointer;
}

.contact__link:hover {
  background: var(--white);
  border-color: var(--border);
}

.contact__link:hover .contact__link-arrow {
  transform: translateX(4px);
  color: var(--indigo);
}

.contact__link-icon {
  width: 36px; height: 36px;
  border-radius: 8px;
  background: var(--indigo-soft);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 14px;
  color: var(--indigo);
  flex-shrink: 0;
}

.contact__link-text {
  font-family: var(--font-mono);
  font-size: 13px;
  color: var(--ink-60);
  flex: 1;
}

.contact__link:hover .contact__link-text { color: var(--ink); }

.contact__link-arrow {
  font-size: 14px;
  color: var(--ink-30);
  transition: all .2s;
}

.code-snippet {
  background: var(--ink);
  border-radius: 14px;
  overflow: hidden;
  margin-bottom: 16px;
  box-shadow: 0 20px 60px rgba(26,24,20,.12);
}

.code-snippet__bar {
  display: flex;
  align-items: center;
  gap: 6px;
  padding: 14px 18px;
  background: rgba(255,255,255,.04);
  border-bottom: 1px solid rgba(255,255,255,.06);
}

.dot {
  width: 10px; height: 10px;
  border-radius: 50%;
  background: rgba(255,255,255,.12);
}

.code-snippet__file {
  font-family: var(--font-mono);
  font-size: 11px;
  color: rgba(255,255,255,.3);
  letter-spacing: .06em;
  margin-left: 6px;
}

.code-snippet__body {
  font-family: var(--font-mono);
  font-size: 13px;
  color: rgba(255,255,255,.55);
  padding: 24px;
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
  gap: 10px;
  font-family: var(--font-mono);
  font-size: 12px;
  color: var(--ink-60);
  letter-spacing: .04em;
}

.avail-dot {
  width: 8px; height: 8px;
  border-radius: 50%;
  background: var(--sage);
  animation: pulse 2s ease-in-out infinite;
}

@keyframes pulse {
  0%,100% { opacity: 1; transform: scale(1); }
  50% { opacity: .5; transform: scale(.8); }
}

@media (max-width: 900px) {
  .contact { padding: 80px 24px 60px; }
  .contact__grid { grid-template-columns: 1fr; gap: 48px; }
}
</style>

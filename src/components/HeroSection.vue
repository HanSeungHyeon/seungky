<template>
  <section id="home" class="hero">
    <div class="hero__grid">
      <div class="hero__content">
        <div class="hero__badge">
          <span class="hero__dot"></span>
          Full-Stack Developer
        </div>

        <h1 class="hero__title">
          안녕하세요,<br>
          <span class="hero__name">한승현</span>입니다.
        </h1>

        <p class="hero__desc">
          깔끔한 구조, 일관된 규칙, 읽기 쉬운 코드.<br>
          유지보수와 확장이 쉬운 개발을 추구합니다.
        </p>

        <div class="hero__scroll" @click="scrollToAbout">
          <span class="hero__scroll-text">Scroll</span>
          <span class="hero__scroll-line"></span>
        </div>
      </div>

      <div class="hero__photo">
        <img class="hero__photo-img" :src="profileImg" alt="한승현 프로필 사진" />
      </div>
    </div>
  </section>
</template>

<script setup>
import profileImg from '../assets/profile.jpg'

function scrollToAbout() {
  document.getElementById('about')?.scrollIntoView({ behavior: 'smooth' })
}
</script>

<style scoped>
.hero {
  max-width: 1100px;
  margin: 0 auto;
  padding: 120px 32px 64px;
}

.hero__grid {
  display: grid;
  grid-template-columns: 1fr 360px;
  gap: 64px;
  align-items: center;
  width: 100%;
}

.hero__content {
  display: flex;
  flex-direction: column;
}

.hero__badge {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  font-family: var(--font-mono);
  font-size: 14px;
  color: var(--accent);
  background: var(--accent-light);
  padding: 8px 20px;
  border-radius: 99px;
  margin-bottom: 36px;
  max-width: max-content;
  animation: fadeUp .6s var(--ease) both;
}

.hero__dot {
  width: 6px; height: 6px;
  border-radius: 50%;
  background: var(--green);
  animation: pulse 2s ease-in-out infinite;
}

@keyframes pulse {
  0%,100% { opacity: 1; }
  50% { opacity: .4; }
}

.hero__title {
  font-family: var(--font-display);
  font-size: clamp(44px, 7vw, 80px);
  font-weight: 700;
  line-height: 1.12;
  letter-spacing: -0.03em;
  color: var(--text);
  margin-bottom: 28px;
  animation: fadeUp .6s .1s var(--ease) both;
}

.hero__name { color: var(--accent); }

.hero__desc {
  font-size: 18px;
  color: var(--text-secondary);
  line-height: 1.85;
  max-width: 480px;
  margin-bottom: 0;
  animation: fadeUp .6s .2s var(--ease) both;
}

.hero__scroll {
  display: flex;
  align-items: center;
  gap: 12px;
  margin-top: 56px;
  cursor: pointer;
  animation: fadeUp .6s .4s var(--ease) both;
}

.hero__scroll-text {
  font-family: var(--font-mono);
  font-size: 12px;
  text-transform: uppercase;
  letter-spacing: 0.15em;
  color: var(--text-muted);
  transition: color .2s;
}

.hero__scroll:hover .hero__scroll-text {
  color: var(--accent);
}

.hero__scroll-line {
  width: 48px;
  height: 1px;
  background: var(--border);
  position: relative;
  overflow: hidden;
}

.hero__scroll-line::after {
  content: '';
  position: absolute;
  left: 0; top: 0;
  width: 100%; height: 100%;
  background: var(--accent);
  animation: scrollLine 2s ease-in-out infinite;
}

@keyframes scrollLine {
  0%   { transform: translateX(-100%); }
  50%  { transform: translateX(0); }
  100% { transform: translateX(100%); }
}

.hero__photo {
  animation: fadeUp .6s .2s var(--ease) both;
}

.hero__photo-img {
  width: 100%;
  aspect-ratio: 3 / 4;
  border-radius: var(--radius-lg);
  object-fit: cover;
  box-shadow: var(--shadow-lg);
}

@keyframes fadeUp {
  from { opacity: 0; transform: translateY(20px); }
  to   { opacity: 1; transform: translateY(0); }
}

@media (max-width: 900px) {
  .hero { padding: 100px 20px 48px; }
  .hero__grid {
    grid-template-columns: 1fr;
    gap: 48px;
  }
  .hero__photo { order: -1; }
  .hero__photo-img { max-width: 260px; margin: 0 auto; }
}
</style>

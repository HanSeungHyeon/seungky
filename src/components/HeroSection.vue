<template>
  <section id="home" class="hero">
    <div class="hero__eyebrow">
      <span class="hero__dot"></span>
      JavaScript &amp; Java Developer
    </div>

    <h1 class="hero__name">
      <span class="hero__name-top">홍길동</span>
      <em class="hero__name-sub">Full-Stack</em>
    </h1>

    <p class="hero__desc">
      사용자 경험을 세밀하게 설계하는 개발자입니다.<br>
      명확한 코드로 복잡한 문제를 해결합니다.
    </p>

    <div class="hero__actions">
      <a href="#projects" class="btn btn--primary">프로젝트 보기</a>
      <a href="#about" class="btn btn--ghost">더 알아보기 ↓</a>
    </div>

    <div class="hero__badges">
      <div class="badge" style="--d:.1s">
        <span class="badge__num">5+</span>
        <span class="badge__label">년 경력</span>
      </div>
      <div class="badge" style="--d:.2s">
        <span class="badge__num">20+</span>
        <span class="badge__label">프로젝트</span>
      </div>
      <div class="badge" style="--d:.3s">
        <span class="badge__num">∞</span>
        <span class="badge__label">커피 사랑</span>
      </div>
    </div>

    <div class="hero__rule"></div>
  </section>
</template>

<style scoped>
.hero {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: 160px 60px 100px;
  position: relative;
  overflow: hidden;
  max-width: 1300px;
  margin: 0 auto;
}

.hero__eyebrow {
  display: flex;
  align-items: center;
  gap: 10px;
  font-family: var(--font-mono);
  font-size: 12px;
  color: var(--ink-60);
  letter-spacing: .08em;
  text-transform: uppercase;
  margin-bottom: 32px;
  animation: fadeUp .7s var(--ease-out) both;
}

.hero__dot {
  width: 7px; height: 7px;
  border-radius: 50%;
  background: var(--sage);
  flex-shrink: 0;
  animation: blink 2.4s ease-in-out infinite;
}

@keyframes blink {
  0%, 100% { opacity: 1; }
  50% { opacity: .3; }
}

.hero__name {
  font-family: var(--font-display);
  font-weight: 400;
  line-height: .9;
  letter-spacing: -.03em;
  margin-bottom: 36px;
  animation: fadeUp .7s .08s var(--ease-out) both;
}

.hero__name-top {
  display: block;
  font-size: clamp(80px, 13vw, 180px);
  color: var(--ink);
}

.hero__name-sub {
  display: block;
  font-size: clamp(50px, 8vw, 110px);
  color: var(--indigo);
  font-style: italic;
}

.hero__desc {
  font-size: clamp(16px, 2vw, 19px);
  color: var(--ink-60);
  line-height: 1.75;
  max-width: 440px;
  margin-bottom: 48px;
  font-weight: 300;
  animation: fadeUp .7s .16s var(--ease-out) both;
}

.hero__actions {
  display: flex;
  gap: 14px;
  animation: fadeUp .7s .24s var(--ease-out) both;
}

.btn {
  display: inline-flex;
  align-items: center;
  font-size: 14px;
  font-weight: 500;
  padding: 13px 26px;
  border-radius: 8px;
  letter-spacing: .01em;
  transition: all .22s var(--ease-out);
  cursor: pointer;
}

.btn--primary {
  background: var(--ink);
  color: var(--white);
}

.btn--primary:hover {
  background: var(--indigo);
  transform: translateY(-2px);
  box-shadow: 0 8px 24px rgba(45,58,140,.18);
}

.btn--ghost {
  color: var(--ink-60);
  border: 1px solid var(--border);
  background: var(--white);
}

.btn--ghost:hover {
  border-color: var(--ink-30);
  color: var(--ink);
  transform: translateY(-2px);
}

.hero__badges {
  position: absolute;
  right: 60px;
  bottom: 100px;
  display: flex;
  flex-direction: column;
  gap: 12px;
  animation: fadeUp .7s .35s var(--ease-out) both;
}

.badge {
  display: flex;
  align-items: baseline;
  gap: 8px;
  background: var(--white);
  border: 1px solid var(--border);
  border-radius: 12px;
  padding: 16px 22px;
  animation: fadeUp .6s calc(.4s + var(--d)) var(--ease-out) both;
  transition: transform .2s, box-shadow .2s;
}

.badge:hover {
  transform: translateY(-3px);
  box-shadow: 0 8px 24px rgba(0,0,0,.06);
}

.badge__num {
  font-family: var(--font-display);
  font-size: 28px;
  color: var(--indigo);
  line-height: 1;
}

.badge__label {
  font-size: 12px;
  color: var(--ink-60);
  font-weight: 400;
}

.hero__rule {
  position: absolute;
  left: 60px; right: 60px;
  bottom: 0;
  height: 1px;
  background: var(--border);
}

@keyframes fadeUp {
  from { opacity: 0; transform: translateY(24px); }
  to   { opacity: 1; transform: translateY(0); }
}

@media (max-width: 768px) {
  .hero { padding: 130px 24px 80px; }
  .hero__badges { position: static; margin-top: 40px; flex-direction: row; }
  .hero__rule { left: 24px; right: 24px; }
}
</style>

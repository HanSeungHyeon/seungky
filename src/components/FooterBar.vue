<template>
  <footer class="footer">
    <div class="footer__inner">
      <span class="footer__copy">© 2025 한승현. Built with Vue 3</span>
      <a href="#home" class="footer__top">맨 위로 ↑</a>
    </div>
  </footer>
</template>

<style scoped>
.footer {
  border-top: 1px solid var(--border);
  padding: 28px 60px;
}

.footer__inner {
  max-width: 1300px;
  margin: 0 auto;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.footer__copy {
  font-family: var(--font-mono);
  font-size: 12px;
  color: var(--ink-60);
  letter-spacing: .04em;
}

.footer__top {
  font-family: var(--font-mono);
  font-size: 12px;
  color: var(--ink-60);
  letter-spacing: .06em;
  transition: color .2s;
}

.footer__top:hover { color: var(--indigo); }

@media (max-width: 768px) {
  .footer { padding: 24px; }
  .footer__inner { flex-direction: column; gap: 8px; }
}
</style>

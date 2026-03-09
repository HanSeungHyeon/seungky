<template>
  <footer class="footer">
    <div class="footer__inner">
      <span class="footer__copy">© 2026 한승현 Portfolio</span>
      <a href="#home" class="footer__top">↑ Top</a>
    </div>
  </footer>
</template>

<style scoped>
.footer {
  border-top: 1px solid var(--border);
  padding: 24px 32px;
}

.footer__inner {
  max-width: 1100px;
  margin: 0 auto;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.footer__copy {
  font-size: 13px;
  color: var(--text-muted);
}

.footer__top {
  font-size: 13px;
  font-weight: 500;
  color: var(--text-muted);
  transition: color .2s;
}

.footer__top:hover { color: var(--accent); }

@media (max-width: 768px) {
  .footer { padding: 20px; }
  .footer__inner { flex-direction: column; gap: 8px; }
}
</style>

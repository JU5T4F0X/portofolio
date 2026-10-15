<template>
  <footer class="footer">
    <div class="container footer-content">
      <div class="footer-logo">
        <ArchLogo :size="20" />
        <span class="footer-brand">denis<span class="f-sep">@</span>arch</span>
      </div>
      <p class="footer-copy">
        <span class="f-mono">© {{ year }} Denis Hendri Wawo</span>
        <span class="f-sep-dot">·</span>
        <span class="f-mono f-dim">Built with Vue 3 + TypeScript</span>
      </p>
    </div>
  </footer>
</template>

<script setup lang="ts">
import ArchLogo from './ArchLogo.vue'
const year = new Date().getFullYear()
</script>

<style scoped>
.footer {
  border-top: 1px solid var(--border-dim);
  padding: 28px 0;
  background: #000;
}

.footer-content {
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-wrap: wrap;
  gap: 16px;
}

.footer-logo {
  display: flex;
  align-items: center;
  gap: 8px;
}

.footer-brand {
  font-family: var(--font-mono);
  font-size: 0.85rem;
  color: var(--arch-blue);
}

.f-sep { color: var(--text-dim); }

.footer-copy {
  display: flex;
  align-items: center;
  gap: 10px;
  flex-wrap: wrap;
}

.f-mono {
  font-family: var(--font-mono);
  font-size: 0.75rem;
  color: var(--text-secondary);
}

.f-dim { color: var(--text-dim); }
.f-arch { color: var(--arch-blue); }
.f-sep-dot { color: var(--text-dim); }
</style>

<template>
  <nav class="navbar" :class="{ scrolled: isScrolled }">
    <div class="nav-container">

      <!-- Desktop Nav Links -->
      <ul class="nav-links" :class="{ open: menuOpen }">
        <li v-for="item in navItems" :key="item.id">
          <a
            :href="`#${item.id}`"
            class="nav-link"
            :class="{ active: activeSection === item.id }"
            @click.prevent="() => { scrollTo(item.id); menuOpen = false }"
          >
            <span class="nav-num">{{ item.num }}</span>
            {{ item.label }}
          </a>
        </li>
      </ul>

      <!-- Hamburger -->
      <button class="hamburger" @click="menuOpen = !menuOpen" :class="{ active: menuOpen }" aria-label="Toggle menu">
        <span></span>
        <span></span>
        <span></span>
      </button>
    </div>
  </nav>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

const isScrolled = ref(false)
const menuOpen = ref(false)
const activeSection = ref('home')

const navItems = [
  { id: 'home', label: 'home', num: '01.' },
  { id: 'about', label: 'about', num: '02.' },
  { id: 'skills', label: 'skills', num: '03.' },
  { id: 'projects', label: 'projects', num: '04.' },
  { id: 'experience', label: 'experience', num: '05.' },
  { id: 'contact', label: 'contact', num: '06.' },
]

const scrollTo = (id: string) => {
  const el = document.getElementById(id)
  if (el) el.scrollIntoView({ behavior: 'smooth' })
}

const handleScroll = () => {
  isScrolled.value = window.scrollY > 20

  // Determine active section
  const sections = navItems.map(item => document.getElementById(item.id))
  const scrollPos = window.scrollY + 120

  for (let i = sections.length - 1; i >= 0; i--) {
    const section = sections[i]
    if (section && section.offsetTop <= scrollPos && navItems[i]) {
      activeSection.value = navItems[i]!.id
      break
    }
  }
}

onMounted(() => window.addEventListener('scroll', handleScroll))
onUnmounted(() => window.removeEventListener('scroll', handleScroll))
</script>

<style scoped>
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 1000;
  height: var(--navbar-height);
  transition: var(--transition);
  border-bottom: 1px solid transparent;
}

.navbar.scrolled {
  background: #000;
  border-bottom-color: var(--border-dim);
}

.nav-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 24px;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 32px;
}

.nav-links {
  display: flex;
  align-items: center;
  gap: 4px;
  list-style: none;
}

.nav-link {
  display: flex;
  align-items: center;
  gap: 4px;
  padding: 6px 14px;
  font-family: var(--font-mono);
  font-size: 0.8rem;
  color: var(--text-secondary);
  text-decoration: none;
  border-radius: 6px;
  transition: var(--transition);
  position: relative;
}

.nav-link::after {
  content: '';
  position: absolute;
  bottom: 2px;
  left: 50%;
  transform: translateX(-50%);
  width: 0;
  height: 1px;
  background: var(--arch-blue);
  transition: width var(--transition);
}

.nav-link:hover,
.nav-link.active {
  color: var(--arch-blue);
  background: var(--arch-blue-dim);
}

.nav-link.active::after { width: 60%; }

.nav-num {
  color: var(--arch-blue);
  font-size: 0.7rem;
  opacity: 0.8;
}

/* Hamburger */
.hamburger {
  display: none;
  flex-direction: column;
  gap: 5px;
  cursor: pointer;
  background: none;
  border: none;
  padding: 8px;
}

.hamburger span {
  display: block;
  width: 22px;
  height: 2px;
  background: var(--text-secondary);
  border-radius: 2px;
  transition: var(--transition);
}

.hamburger.active span:nth-child(1) {
  transform: translateY(7px) rotate(45deg);
  background: var(--arch-blue);
}
.hamburger.active span:nth-child(2) { opacity: 0; }
.hamburger.active span:nth-child(3) {
  transform: translateY(-7px) rotate(-45deg);
  background: var(--arch-blue);
}

@media (max-width: 768px) {
  .hamburger { display: flex; }

  .nav-links {
    position: fixed;
    top: var(--navbar-height);
    right: 0;
    bottom: 0;
    width: 260px;
    flex-direction: column;
    align-items: flex-start;
    padding: 32px 24px;
    gap: 8px;
    background: #000;
    border-left: 1px solid var(--border-dim);
    transform: translateX(100%);
    transition: transform var(--transition);
  }

  .nav-links.open { transform: translateX(0); }
  .nav-link { font-size: 0.9rem; padding: 10px 16px; width: 100%; }
}
</style>

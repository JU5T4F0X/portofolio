<template>
  <section id="home" class="hero">
    <div class="container hero-content">
      <!-- Hero Text (Left column) -->
      <div class="hero-text" :class="{ visible: heroVisible }">
        <p class="hero-greeting">Hello, World.</p>
        <h1 class="hero-name">Denis Hendri <span class="name-highlight">Wawo</span></h1>
        <p class="hero-role">
          <span class="role-prefix">$ </span>
          <span class="role-text">{{ currentRole }}</span>
          <span class="cursor-blink" style="width:2px;height:1.1em;background:var(--arch-blue);"></span>
        </p>
        <p class="hero-desc">
          7th-semester Information Systems student at <span class="text-arch">Telkom University</span>.
          Full-stack developer. Cyber security enthusiast. Arch user.
        </p>

        <div class="hero-btns">
          <a href="#projects" class="btn btn-primary" @click.prevent="scrollTo('projects')">
            <span>~/projects</span>
          </a>
          <a href="#contact" class="btn btn-ghost" @click.prevent="scrollTo('contact')">
            <span>get in touch</span>
          </a>
          <button class="btn btn-toggle" @click="heroTab = heroTab === 'photo' ? 'terminal' : 'photo'">
            <Terminal v-if="heroTab === 'photo'" :size="14" />
            <User v-else :size="14" />
            <span>{{ heroTab === 'photo' ? 'terminal' : 'photo' }}</span>
          </button>
        </div>

        <!-- Arch hint -->
        <div class="arch-hint">
          <ArchLogo :size="16" />
          <span class="arch-hint-text">btw, i use arch</span>
        </div>
      </div>

      <!-- Hero Visual (Right column: BIG Photo Card & Terminal Switcher) -->
      <div class="terminal-window hero-visual" ref="terminalRef">
        <div class="terminal-header hero-window-header">
          <div class="terminal-dots">
            <div class="terminal-dot red"></div>
            <div class="terminal-dot yellow"></div>
            <div class="terminal-dot green"></div>
          </div>
          <div class="hero-tabs">
            <button
              class="hero-tab"
              :class="{ active: heroTab === 'photo' }"
              @click="heroTab = 'photo'"
              type="button"
            >
              <User :size="13" />
              <span>denis.jpg</span>
            </button>
            <button
              class="hero-tab"
              :class="{ active: heroTab === 'terminal' }"
              @click="heroTab = 'terminal'"
              type="button"
            >
              <Terminal :size="13" />
              <span>fastfetch</span>
            </button>
          </div>
        </div>

        <!-- Tab 1: BIG Photo View (DEFAULT - PROMINENT & HIGH RESOLUTION) -->
        <div v-show="heroTab === 'photo'" class="hero-photo-view">
          <div class="hero-photo-frame">
            <img src="/denis-photo.jpg" alt="Denis Hendri Wawo" class="hero-big-img" />
            <div class="hero-photo-gradient"></div>
            <div class="hero-photo-caption">
              <span class="caption-name">Denis Hendri Wawo</span>
              <span class="caption-role">Full-Stack Developer · Cyber Security</span>
            </div>
          </div>
        </div>

        <!-- Tab 2: Terminal View -->
        <div v-show="heroTab === 'terminal'" class="terminal-body hero-terminal-body">
          <div v-for="(line, index) in visibleLines" :key="index" class="terminal-line">
            <template v-if="line.type === 'command'">
              <span class="terminal-user">denis</span>
              <span class="terminal-path"> ~/portfolio</span>
              <span class="terminal-arrow"> $ </span>
              <span class="terminal-cmd">{{ line.content }}</span>
            </template>
            <template v-else-if="line.type === 'output'">
              <span :class="'terminal-out-' + (line.color || 'default')">{{ line.content }}</span>
            </template>
            <template v-else-if="line.type === 'blank'">
              <br />
            </template>
          </div>
          <div class="terminal-line" v-if="showCursor">
            <span class="terminal-user">denis</span>
            <span class="terminal-path"> ~/portfolio</span>
            <span class="terminal-arrow"> $ </span>
            <span class="cursor-blink"></span>
          </div>
        </div>
      </div>
    </div>

    <!-- Scroll indicator -->
    <div class="scroll-indicator">
      <div class="scroll-line"></div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'
import ArchLogo from './ArchLogo.vue'
import { User, Terminal } from '@lucide/vue'

const heroTab = ref<'photo' | 'terminal'>('photo')
const terminalRef = ref<HTMLElement | null>(null)
const visibleLines = ref<any[]>([])
const showCursor = ref(false)
const heroVisible = ref(false)

const roles = [
  'Full-Stack Developer',
  'Cyber Security',
  'Linux Enthusiast',
  'Information Systems Student',
  'Software Engineer Intern',
]
const currentRole = ref('')
let roleIndex = 0
let charIndex = 0
let isDeleting = false

const terminalScript = [
  { type: 'command', content: 'fastfetch' },
  { type: 'output', content: '╔══════════════════════════════════════╗', color: 'arch' },
  { type: 'output', content: '  OS        : Arch Linux x86_64', color: 'default' },
  { type: 'output', content: '  Kernel    : 6.11.4-arch1-1', color: 'default' },
  { type: 'output', content: '  Shell     : bash 5.2.37', color: 'default' },
  { type: 'output', content: '  WM        : Hyprland', color: 'green' },
  { type: 'output', content: '  Terminal  : kitty', color: 'default' },
  { type: 'output', content: '  GitHub    : github.com/JU5T4F0X', color: 'arch' },
  { type: 'output', content: '╚══════════════════════════════════════╝', color: 'arch' },
  { type: 'blank', content: '' },
  { type: 'command', content: 'cat welcome.txt' },
  { type: 'output', content: '  Welcome to my portfolio!', color: 'green' },
  { type: 'output', content: '  Denis Hendri Wawo - Full-Stack Dev', color: 'default' },
  { type: 'blank', content: '' },
]

const scrollTo = (id: string) => {
  const el = document.getElementById(id)
  if (el) el.scrollIntoView({ behavior: 'smooth' })
}

const typeRole = () => {
  const target = roles[roleIndex]
  if (!target) return
  if (!isDeleting) {
    currentRole.value = target.slice(0, charIndex + 1)
    charIndex++
    if (charIndex === target.length) {
      isDeleting = true
      setTimeout(typeRole, 2000)
      return
    }
  } else {
    currentRole.value = target.slice(0, charIndex - 1)
    charIndex--
    if (charIndex === 0) {
      isDeleting = false
      roleIndex = (roleIndex + 1) % roles.length
    }
  }
  setTimeout(typeRole, isDeleting ? 60 : 80)
}

const runTerminal = async () => {
  for (const line of terminalScript) {
    if (line.type === 'command') {
      const cmdLine = { type: 'command', content: '' }
      visibleLines.value.push(cmdLine)
      for (const char of line.content) {
        cmdLine.content += char
        await sleep(60)
      }
      await sleep(300)
    } else {
      visibleLines.value.push({ ...line })
      await sleep(80)
    }
  }
  showCursor.value = true
}

const sleep = (ms: number) => new Promise(resolve => setTimeout(resolve, ms))

onMounted(async () => {
  await sleep(400)
  await runTerminal()
  heroVisible.value = true
  typeRole()
})
</script>

<style scoped>
.hero {
  min-height: 100vh;
  display: flex;
  align-items: center;
  position: relative;
  padding-top: var(--navbar-height);
  overflow: hidden;
}

.hero-content {
  display: grid;
  grid-template-columns: 1fr 1.05fr;
  gap: 56px;
  align-items: center;
  padding-top: 40px;
  padding-bottom: 40px;
}

/* Hero text */
.hero-text {
  opacity: 0;
  transform: translateY(20px);
  transition: all 0.8s ease 0.3s;
}

.hero-text.visible {
  opacity: 1;
  transform: translateY(0);
}

.hero-greeting {
  font-family: var(--font-mono);
  font-size: 0.95rem;
  color: var(--green-terminal);
  margin-bottom: 12px;
  letter-spacing: 0.05em;
}

.hero-name {
  font-size: clamp(2.3rem, 5vw, 3.6rem);
  font-weight: 800;
  line-height: 1.1;
  margin-bottom: 16px;
  letter-spacing: -0.02em;
}

.name-highlight {
  color: var(--arch-blue);
}

.hero-role {
  font-family: var(--font-mono);
  font-size: 1.1rem;
  color: var(--arch-blue);
  margin-bottom: 20px;
  display: flex;
  align-items: center;
  gap: 4px;
}

.role-prefix { color: var(--green-terminal); }

.hero-desc {
  color: var(--text-secondary);
  font-size: 1rem;
  line-height: 1.7;
  margin-bottom: 32px;
  max-width: 440px;
}

.text-arch { color: var(--arch-blue); font-weight: 500; }

.hero-btns {
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
  margin-bottom: 28px;
}

.btn-toggle {
  background: transparent;
  color: var(--text-secondary);
  border: 1px solid var(--border-dim);
}

.btn-toggle:hover {
  color: var(--text-bright);
  border-color: var(--border-arch);
  background: var(--arch-blue-dim);
}

/* Arch hint */
.arch-hint {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 6px 12px;
  background: var(--arch-blue-dim);
  border: 1px solid var(--border-arch);
  border-radius: 6px;
  font-family: var(--font-mono);
  font-size: 0.75rem;
  color: var(--arch-blue);
}

/* Hero Visual (BIG Photo & Terminal Container) */
.hero-visual {
  animation: fadeInUp 0.8s ease forwards;
  border: 1px solid #282828;
  border-radius: 14px;
  overflow: hidden;
  background: #000;
  box-shadow: 0 20px 50px -10px rgba(0, 0, 0, 0.7);
  transition: border-color var(--transition), box-shadow var(--transition);
}

.hero-visual:hover {
  border-color: #3a3a3a;
  box-shadow: 0 24px 60px -10px rgba(0, 0, 0, 0.85);
}

.hero-window-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px 14px;
  background: var(--bg-terminal-header);
  border-bottom: 1px solid #1a1a1a;
}

.terminal-dots {
  display: flex;
  align-items: center;
  gap: 8px;
}

.hero-tabs {
  display: flex;
  gap: 6px;
}

.hero-tab {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  padding: 4px 10px;
  background: transparent;
  border: 1px solid transparent;
  border-radius: 6px;
  font-family: var(--font-mono);
  font-size: 0.72rem;
  color: var(--text-dim);
  cursor: pointer;
  transition: var(--transition);
}

.hero-tab:hover {
  color: var(--text-primary);
  background: rgba(255, 255, 255, 0.06);
}

.hero-tab.active {
  color: var(--arch-blue);
  background: var(--arch-blue-dim);
  border-color: var(--border-arch);
  font-weight: 600;
}

/* BIG Photo View */
.hero-photo-view {
  width: 100%;
}

.hero-photo-frame {
  position: relative;
  width: 100%;
  height: 480px;
  overflow: hidden;
  background: #000;
}

.hero-big-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: center 25%;
  display: block;
  transition: transform 0.6s cubic-bezier(0.16, 1, 0.3, 1);
}

.hero-visual:hover .hero-big-img {
  transform: scale(1.03);
}

.hero-photo-gradient {
  position: absolute;
  inset: 0;
  background: linear-gradient(
    to bottom,
    rgba(0, 0, 0, 0) 55%,
    rgba(0, 0, 0, 0.6) 80%,
    rgba(0, 0, 0, 0.95) 100%
  );
  pointer-events: none;
}



.hero-photo-caption {
  position: absolute;
  bottom: 18px;
  left: 20px;
  right: 20px;
  display: flex;
  flex-direction: column;
  gap: 4px;
  z-index: 2;
}

.caption-name {
  font-size: 1.25rem;
  font-weight: 700;
  color: #ffffff;
  letter-spacing: -0.01em;
}

.caption-role {
  font-family: var(--font-mono);
  font-size: 0.82rem;
  color: var(--arch-blue-bright);
}

/* Terminal View */
.hero-terminal-body {
  height: 480px;
  overflow-y: auto;
  padding: 24px;
}

.terminal-sep { color: var(--text-dim); font-family: var(--font-mono); }
.terminal-host { color: var(--arch-blue); font-family: var(--font-mono); }
.terminal-path { color: var(--purple-accent); font-family: var(--font-mono); font-size: 0.875rem; }
.terminal-arrow { color: var(--green-terminal); font-family: var(--font-mono); }
.terminal-cmd { color: var(--text-primary); font-family: var(--font-mono); font-size: 0.875rem; }

.terminal-out-default { color: var(--text-secondary); font-family: var(--font-mono); font-size: 0.8rem; padding-left: 8px; }
.terminal-out-arch { color: var(--arch-blue); font-family: var(--font-mono); font-size: 0.8rem; padding-left: 8px; }
.terminal-out-green { color: var(--green-terminal); font-family: var(--font-mono); font-size: 0.8rem; padding-left: 8px; }

/* Scroll indicator */
.scroll-indicator {
  position: absolute;
  bottom: 32px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 8px;
  font-family: var(--font-mono);
  font-size: 0.65rem;
  color: var(--text-dim);
  letter-spacing: 0.15em;
  text-transform: uppercase;
}

.scroll-line {
  width: 1px;
  height: 40px;
  background: var(--border-dim);
}

@media (max-width: 900px) {
  .hero-content {
    grid-template-columns: 1fr;
    gap: 40px;
  }
  .hero-photo-frame, .hero-terminal-body {
    height: 380px;
  }
}
</style>

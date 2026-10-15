<template>
  <section id="home" class="hero">
    <div class="container hero-content">
      <!-- Terminal typing effect -->
      <div class="terminal-window hero-terminal" ref="terminalRef">
        <div class="terminal-header">
          <div class="terminal-dot red"></div>
          <div class="terminal-dot yellow"></div>
          <div class="terminal-dot green"></div>
          <span class="terminal-title">~/portfolio - bash</span>
        </div>
        <div class="terminal-body">
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

      <!-- Hero Text -->
      <div class="hero-text" :class="{ visible: heroVisible }">
        <p class="hero-greeting">Hello, World.</p>
        <h1 class="hero-name">Denis Hendri <span class="name-highlight">Wawo</span></h1>
        <p class="hero-role">
          <span class="role-prefix">$ </span>
          <span class="role-text">{{ currentRole }}</span>
          <span class="cursor-blink" style="width:2px;height:1.1em;background:var(--arch-blue);"></span>
        </p>
        <p class="hero-desc">
          6th-semester Information Systems student at <span class="text-arch">Telkom University</span>.
          Full-stack developer. Linux enthusiast. Arch user.
        </p>

        <div class="hero-btns">
          <a href="#projects" class="btn btn-primary" @click.prevent="scrollTo('projects')">
            <span>~/projects</span>
          </a>
          <a href="#contact" class="btn btn-ghost" @click.prevent="scrollTo('contact')">
            <span>get in touch</span>
          </a>
        </div>

        <!-- Arch hint -->
        <div class="arch-hint">
          <ArchLogo :size="16" />
          <span class="arch-hint-text">btw, i use arch</span>
        </div>
      </div>
    </div>

    <!-- Scroll indicator (line only, no text) -->
    <div class="scroll-indicator">
      <div class="scroll-line"></div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'
import ArchLogo from './ArchLogo.vue'

const terminalRef = ref<HTMLElement | null>(null)
const visibleLines = ref<any[]>([])
const showCursor = ref(false)
const heroVisible = ref(false)

const roles = [
  'Full-Stack Developer',
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
      // type character by character
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
  grid-template-columns: 1fr 1fr;
  gap: 64px;
  align-items: center;
  padding-top: 40px;
  padding-bottom: 40px;
}

/* Terminal */
.hero-terminal {
  animation: fadeInUp 0.8s ease forwards;
}

.terminal-sep { color: var(--text-dim); font-family: var(--font-mono); }
.terminal-host { color: var(--arch-blue); font-family: var(--font-mono); }
.terminal-path { color: var(--purple-accent); font-family: var(--font-mono); font-size: 0.875rem; }
.terminal-arrow { color: var(--green-terminal); font-family: var(--font-mono); }
.terminal-cmd { color: var(--text-primary); font-family: var(--font-mono); font-size: 0.875rem; }

.terminal-out-default { color: var(--text-secondary); font-family: var(--font-mono); font-size: 0.8rem; padding-left: 8px; }
.terminal-out-arch { color: var(--arch-blue); font-family: var(--font-mono); font-size: 0.8rem; padding-left: 8px; }
.terminal-out-green { color: var(--green-terminal); font-family: var(--font-mono); font-size: 0.8rem; padding-left: 8px; }

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
  font-size: 0.9rem;
  color: var(--green-terminal);
  margin-bottom: 12px;
  letter-spacing: 0.05em;
}

.hero-name {
  font-size: clamp(2.2rem, 5vw, 3.5rem);
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
  max-width: 420px;
}

.text-arch { color: var(--arch-blue); font-weight: 500; }

.hero-btns {
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
  margin-bottom: 28px;
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
  .hero-terminal { order: 2; }
  .hero-text { order: 1; }
}
</style>

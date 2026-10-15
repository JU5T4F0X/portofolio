<template>
  <section id="skills" class="section">
    <div class="container">
      <p class="section-label">// 03. skills</p>
      <h2 class="section-title">Tech Stack</h2>

      <div class="skills-layout">
        <div class="skill-categories">
          <div
            class="card skill-card"
            v-for="category in skills"
            :key="category.name"
          >
            <div class="skill-card-header">
              <component :is="category.icon" :size="18" class="skill-cat-icon" />
              <span class="skill-name">{{ category.name }}</span>
            </div>
            <div class="skill-tags">
              <span class="tag" v-for="skill in category.items" :key="skill">{{ skill }}</span>
            </div>
          </div>
        </div>

        <!-- Neofetch-style terminal -->
        <div class="terminal-window skills-terminal">
          <div class="terminal-header">
            <div class="terminal-dot red"></div>
            <div class="terminal-dot yellow"></div>
            <div class="terminal-dot green"></div>
            <span class="terminal-title">denis@arch ~ skills --list</span>
          </div>
          <div class="terminal-body">
            <div class="nf-row">
              <div class="nf-arch">
                <ArchLogo :size="96" />
              </div>
              <div class="nf-info">
                <p class="nf-line"><span class="nf-user">denis</span><span class="nf-at"> ~/portfolio</span></p>
                <p class="nf-sep">─────────────────────</p>
                <p class="nf-line"><span class="nf-key">OS</span><span class="nf-colon">: </span><span class="nf-val">Arch Linux x86_64</span></p>
                <p class="nf-line"><span class="nf-key">Shell</span><span class="nf-colon">: </span><span class="nf-val">bash 5.2.37</span></p>
                <p class="nf-line"><span class="nf-key">WM</span><span class="nf-colon">: </span><span class="nf-val">Hyprland</span></p>
                <p class="nf-line"><span class="nf-key">Editor</span><span class="nf-colon">: </span><span class="nf-val">Neovim</span></p>
                <p class="nf-line"><span class="nf-key">Lang</span><span class="nf-colon">: </span><span class="nf-val">JS / TS / PHP</span></p>
                <p class="nf-line"><span class="nf-key">Stack</span><span class="nf-colon">: </span><span class="nf-val">Next.js / Laravel</span></p>
                <p class="nf-line"><span class="nf-key">DB</span><span class="nf-colon">: </span><span class="nf-val">MySQL</span></p>
                <p class="nf-sep">─────────────────────</p>
                <div class="nf-colors">
                  <span v-for="c in colors" :key="c" class="nf-dot" :style="{ background: c }"></span>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { Code2, Globe, Wrench, Terminal } from '@lucide/vue'
import ArchLogo from './ArchLogo.vue'

const skills = [
  {
    name: 'Languages',
    icon: Code2,
    items: ['JavaScript', 'TypeScript', 'Python', 'PHP', 'Java'],
  },
  {
    name: 'Web & Frameworks',
    icon: Globe,
    items: ['HTML', 'CSS', 'Tailwind CSS', 'Vue.js', 'Next.js', 'Express.js', 'Laravel'],
  },
  {
    name: 'Tools & Technologies',
    icon: Wrench,
    items: ['MySQL', 'Git', 'Linux', 'WebSockets', 'REST APIs', 'Selenium', 'Katalon'],
  },
  {
    name: 'Linux & Multi-OS',
    icon: Terminal,
    items: ['Arch Linux', 'Rocky Linux', 'Kali Linux', 'Parrot OS', 'Bash', 'SSH', 'Neovim'],
  },
]

const colors = [
  '#1793d1', '#7cb87c', '#8a7bb8', '#b87a9c',
  '#c9a06a', '#d4b45a', '#e06c75', '#6aa8b8',
]
</script>

<style scoped>
.skills-layout {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 40px;
  align-items: start;
}

.skill-categories {
  display: grid;
  grid-template-columns: 1fr;
  gap: 16px;
}

.skill-card { cursor: default; }

.skill-card-header {
  display: flex;
  align-items: center;
  gap: 10px;
  margin-bottom: 14px;
}

.skill-cat-icon { color: var(--arch-blue); }

.skill-name {
  font-family: var(--font-mono);
  font-size: 0.85rem;
  color: var(--arch-blue);
  font-weight: 600;
  letter-spacing: 0.05em;
}

.skill-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}

.skills-terminal .terminal-body { padding: 24px; }

.nf-row {
  display: flex;
  gap: 28px;
  align-items: flex-start;
}

.nf-arch { flex-shrink: 0; }
.nf-info { flex: 1; }

.nf-line {
  font-family: var(--font-mono);
  font-size: 0.78rem;
  line-height: 1.9;
}

.nf-user { color: var(--green-terminal); font-weight: 700; }
.nf-at { color: var(--text-dim); }
.nf-host { color: var(--arch-blue); font-weight: 700; }

.nf-sep {
  font-family: var(--font-mono);
  font-size: 0.72rem;
  color: var(--text-dim);
  margin: 4px 0;
}

.nf-key { color: var(--arch-blue); font-weight: 600; }
.nf-colon { color: var(--text-dim); }
.nf-val { color: var(--text-primary); }

.nf-colors {
  display: flex;
  gap: 6px;
  margin-top: 8px;
  flex-wrap: wrap;
}

.nf-dot {
  width: 16px;
  height: 16px;
  border-radius: 3px;
  display: inline-block;
}

@media (max-width: 768px) {
  .skills-layout { grid-template-columns: 1fr; }
  .nf-row { flex-direction: column; align-items: center; }
}
</style>

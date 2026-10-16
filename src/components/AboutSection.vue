<template>
  <section id="about" class="section">
    <div class="container">
      <p class="section-label">// 02. about</p>
      <h2 class="section-title">About Me</h2>

      <div class="about-grid">
        <!-- Terminal bio -->
        <div class="about-bio">
          <div class="terminal-window bio-terminal">
            <div class="terminal-header">
              <div class="terminal-dot red"></div>
              <div class="terminal-dot yellow"></div>
              <div class="terminal-dot green"></div>
              <span class="terminal-title">cat bio.md</span>
            </div>
            <div class="terminal-body">
              <p class="t-line"><span class="t-key">name</span>: <span class="t-val">Denis Hendri Wawo</span></p>
              <p class="t-line"><span class="t-key">location</span>: <span class="t-val">Jakarta Pusat, Indonesia</span></p>
              <p class="t-line"><span class="t-key">university</span>: <span class="t-val">Telkom University</span></p>
              <p class="t-line"><span class="t-key">major</span>: <span class="t-val">Information Systems</span></p>
              <p class="t-line"><span class="t-key">semester</span>: <span class="t-val">7th</span></p>
              <p class="t-line"><span class="t-key">gpa</span>: <span class="t-val gpa">3.53 / 4.00</span></p>
              <p class="t-line"><span class="t-key">email</span>: <span class="t-val link">hendrikdenis3@gmail.com</span></p>
              <p class="t-line"><span class="t-key">phone</span>: <span class="t-val">+62-819-0634-0877</span></p>
              <br/>
              <p class="t-line"><span class="t-key">distro</span>: <span class="t-val arch">Arch Linux (daily)</span></p>
              <p class="t-line"><span class="t-key">also</span>: <span class="t-val">Rocky, Kali, Parrot OS</span></p>
              <p class="t-line"><span class="t-key">wm</span>: <span class="t-val">Hyprland</span></p>
              <p class="t-line"><span class="t-key">editor</span>: <span class="t-val">Neovim / VSCode</span></p>
              <p class="t-line"><span class="t-key">shell</span>: <span class="t-val">bash 5.2.37</span></p>
            </div>
          </div>
        </div>

        <!-- Story + stats -->
        <div class="about-story">
          <div class="story-block">
            <p class="story-text">
              I'm a 7th-semester <span class="hl">Information Systems</span> student at
              <span class="hl">Telkom University</span> with a strong focus on
              <span class="hl">Software Engineering</span>, <span class="hl">Cyber Security</span>, and full-stack web development.
            </p>
            <p class="story-text">
              I build scalable web applications, design RESTful APIs, and architect relational
              databases. I love working with modern frameworks and applying OOP principles to
              write clean, maintainable code.
            </p>
            <p class="story-text">
              Outside of coding, I'm a hardcore <span class="hl-arch">Arch Linux</span> enthusiast -
              I rice my desktop, tweak my dotfiles, and live in the terminal.
              I'm also experienced across multiple Linux distros including
              <span class="hl">Rocky Linux</span>, <span class="hl">Kali Linux</span>, and <span class="hl">Parrot OS</span>.
            </p>
          </div>

          <div class="stats-grid">
            <div class="stat-item" v-for="stat in stats" :key="stat.label">
              <span class="stat-value">{{ stat.value }}</span>
              <span class="stat-label">{{ stat.label }}</span>
            </div>
          </div>

          <div class="os-badge">
            <ArchLogo :size="26" />
            <div class="os-badge-info">
              <span class="os-name">Arch Linux</span>
              <span class="os-tagline">Daily Driver & Dev Environment</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import ArchLogo from './ArchLogo.vue'

const stats = [
  { value: '3+', label: 'Projects Built' },
  { value: '3.53', label: 'GPA' },
  { value: '7th', label: 'Semester' },
  { value: '10+', label: 'Tech Stack' },
]
</script>

<style scoped>
.about-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 48px;
  align-items: start;
}



.bio-terminal .terminal-body { padding: 20px 24px; }

.t-line {
  font-family: var(--font-mono);
  font-size: 0.82rem;
  line-height: 2;
  color: var(--text-secondary);
}
.t-key { color: var(--arch-blue); }
.t-val { color: var(--text-primary); }
.t-val.gpa { color: var(--green-terminal); font-weight: 600; }
.t-val.link { color: var(--purple-accent); text-decoration: underline; }
.t-val.arch { color: var(--arch-blue); font-weight: 600; }

.story-block { margin-bottom: 32px; }
.story-text {
  color: var(--text-secondary);
  font-size: 0.95rem;
  line-height: 1.8;
  margin-bottom: 16px;
}
.hl { color: var(--arch-blue); font-weight: 500; }
.hl-arch { color: var(--arch-blue); font-weight: 700; }

.stats-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 16px;
  margin-bottom: 28px;
}
.stat-item {
  background: var(--bg-card);
  border: 1px solid var(--border-dim);
  border-radius: 10px;
  padding: 16px 12px;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 4px;
  transition: var(--transition);
}
.stat-item:hover {
  border-color: var(--border-arch);
}
.stat-value {
  font-family: var(--font-mono);
  font-size: 1.4rem;
  font-weight: 700;
  color: var(--arch-blue);
}
.stat-label {
  font-family: var(--font-mono);
  font-size: 0.65rem;
  color: var(--text-dim);
  text-transform: uppercase;
  letter-spacing: 0.1em;
  text-align: center;
}

.os-badge {
  display: inline-flex;
  align-items: center;
  gap: 14px;
  padding: 14px 20px;
  background: var(--bg-card);
  border: 1px solid var(--border-arch);
  border-radius: 8px;
}
.os-badge-info { display: flex; flex-direction: column; gap: 2px; }
.os-name {
  font-family: var(--font-mono);
  font-size: 0.9rem;
  font-weight: 600;
  color: var(--arch-blue);
}
.os-tagline {
  font-family: var(--font-mono);
  font-size: 0.7rem;
  color: var(--text-dim);
  font-style: italic;
}

@media (max-width: 768px) {
  .about-grid { grid-template-columns: 1fr; }
  .stats-grid { grid-template-columns: repeat(2, 1fr); }
}
</style>

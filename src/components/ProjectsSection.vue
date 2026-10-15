<template>
  <section id="projects" class="section">
    <div class="container">
      <p class="section-label">// 04. projects</p>
      <h2 class="section-title">Projects</h2>

      <div class="projects-grid">
        <div
          class="card project-card"
          v-for="project in projects"
          :key="project.title"
        >
          <div class="project-header">
            <div class="project-icon-wrap">
              <component :is="project.icon" :size="22" class="project-icon" />
            </div>
            <div class="project-badges">
              <span class="project-type-badge">{{ project.type }}</span>
            </div>
          </div>

          <h3 class="project-title">{{ project.title }}</h3>
          <p class="project-desc">{{ project.desc }}</p>

          <ul class="project-bullets">
            <li v-for="bullet in project.bullets" :key="bullet">
              <ChevronRight :size="14" class="bullet-icon" />
              <span>{{ bullet }}</span>
            </li>
          </ul>

          <div class="project-footer">
            <div class="project-tags">
              <span class="tag" v-for="tech in project.tech" :key="tech">{{ tech }}</span>
            </div>
            <a
              :href="project.github"
              target="_blank"
              rel="noopener noreferrer"
              class="github-link"
              :title="`View ${project.title} on GitHub`"
            >
              <GitBranch :size="16" />
              <span>source</span>
            </a>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { Hotel, Pill, Globe, ChevronRight, GitBranch } from '@lucide/vue'



const projects = [
  {
    icon: Hotel,
    type: 'Full-Stack',
    title: 'Real-Time Hotel Management System',
    desc: 'A full-stack hotel management web app with real-time room status updates and responsive UI.',
    bullets: [
      'Built with Next.js leveraging React foundation for responsive UI and API routes for server-side logic',
      'Integrated WebSockets for real-time communication and instant dynamic data updates',
      'Designed MySQL database architecture for reservations and operational data',
    ],
    tech: ['TypeScript', 'Next.js', 'WebSockets', 'MySQL', 'React'],
    github: 'https://github.com/JU5T4F0X/Project-Hotel-U-dengan-websocket',
  },
  {
    icon: Pill,
    type: 'Web App',
    title: 'Pharmacy Information System',
    desc: 'A web-based pharmacy management app (Apotik Telkom) for streamlined inventory and administration.',
    bullets: [
      'Built web-based pharmacy management application to streamline inventory tracking',
      'Structured application logic using PHP for data transactions and user interfaces',
      'Designed for efficient operational administration workflows',
    ],
    tech: ['PHP', 'HTML', 'CSS', 'MySQL'],
    github: 'https://github.com/JU5T4F0X/Apotik-telkom',
  },
  {
    icon: Globe,
    type: 'Full-Stack / Microservice',
    title: 'KPPM Telkom University',
    desc: 'Web platform for Kerja Praktik Pengabdian Masyarakat (KPPM) at Telkom University, built with a microservice architecture.',
    bullets: [
      'Architected using microservice pattern with Express.js as backend services for modular and scalable APIs',
      'Built responsive frontend with Next.js for server-side rendering and optimized user experience',
      'Collaborated in a team to design and ship a full-featured KPPM management platform',
    ],
    tech: ['Next.js', 'Express.js', 'Microservice', 'MySQL', 'REST API'],
    github: 'https://github.com/Web-KPPM-Tel-U/KPPM-Telkom-University',
  },
]
</script>

<style scoped>
.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
  gap: 24px;
}

.project-card {
  display: flex;
  flex-direction: column;
  gap: 14px;
}

.project-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.project-icon-wrap {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 40px;
  height: 40px;
  border-radius: 8px;
  background: var(--arch-blue-dim);
  border: 1px solid var(--border-arch);
}

.project-icon { color: var(--arch-blue); }

.project-badges { display: flex; gap: 8px; align-items: center; }

.project-type-badge {
  font-family: var(--font-mono);
  font-size: 0.7rem;
  color: var(--green-terminal);
  border: 1px solid rgba(124, 184, 124, 0.28);
  background: rgba(124, 184, 124, 0.08);
  padding: 3px 10px;
  border-radius: 4px;
}

.project-title {
  font-size: 1.05rem;
  font-weight: 700;
  color: var(--text-primary);
  line-height: 1.3;
}

.project-desc {
  font-size: 0.875rem;
  color: var(--text-secondary);
  line-height: 1.6;
}

.project-bullets {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 6px;
  flex: 1;
}

.project-bullets li {
  font-size: 0.8rem;
  color: var(--text-secondary);
  line-height: 1.5;
  display: flex;
  align-items: flex-start;
  gap: 6px;
}

.bullet-icon {
  color: var(--arch-blue);
  flex-shrink: 0;
  margin-top: 2px;
}

.project-footer {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 12px;
  margin-top: auto;
  padding-top: 12px;
  border-top: 1px solid var(--border-dim);
  flex-wrap: wrap;
}

.project-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
}

.github-link {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  font-family: var(--font-mono);
  font-size: 0.75rem;
  color: var(--text-dim);
  text-decoration: none;
  padding: 4px 10px;
  border: 1px solid var(--border-dim);
  border-radius: 6px;
  transition: var(--transition);
  flex-shrink: 0;
}

.github-link:hover {
  color: var(--arch-blue);
  border-color: var(--border-arch);
  background: var(--arch-blue-dim);
}
</style>

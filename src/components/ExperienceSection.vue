<template>
  <section id="experience" class="section">
    <div class="container">
      <p class="section-label">// 05. experience</p>
      <h2 class="section-title">Experience</h2>

      <div class="exp-layout">
        <!-- Timeline -->
        <div class="timeline">
          <div
            class="timeline-item"
            v-for="(exp, i) in experiences"
            :key="i"
          >
            <div class="timeline-marker">
              <div class="timeline-dot"></div>
              <div class="timeline-line" v-if="i < experiences.length - 1"></div>
            </div>
            <div class="card timeline-card">
              <div class="exp-header">
                <div>
                  <h3 class="exp-role">{{ exp.role }}</h3>
                  <p class="exp-company">{{ exp.company }}</p>
                  <p class="exp-location">
                    <MapPin :size="12" class="loc-icon" /> {{ exp.location }}
                  </p>
                </div>
                <span class="period-badge">{{ exp.period }}</span>
              </div>
              <ul class="exp-bullets">
                <li v-for="bullet in exp.bullets" :key="bullet">
                  <ChevronRight :size="14" class="bullet-icon" />
                  <span>{{ bullet }}</span>
                </li>
              </ul>
            </div>
          </div>
        </div>

        <!-- Education + terminal -->
        <div class="edu-panel">
          <div class="card edu-card">
            <div class="edu-icon-wrap">
              <GraduationCap :size="28" class="edu-icon" />
            </div>
            <h3 class="edu-title">Education</h3>
            <div class="edu-detail">
              <p class="edu-school">Telkom University</p>
              <p class="edu-major">Bachelor of Information Systems</p>
              <p class="edu-meta">
                <MapPin :size="12" class="loc-icon" /> Jakarta, Indonesia
              </p>
              <p class="edu-meta">2023 - Present</p>
              <div class="gpa-badge">
                <span class="gpa-label">GPA</span>
                <span class="gpa-value">3.53 / 4.00</span>
              </div>
            </div>
          </div>

          <div class="terminal-window edu-terminal">
            <div class="terminal-header">
              <div class="terminal-dot red"></div>
              <div class="terminal-dot yellow"></div>
              <div class="terminal-dot green"></div>
              <span class="terminal-title">uptime</span>
            </div>
            <div class="terminal-body">
              <p class="t-cmd"><span class="t-prompt">$</span> uptime --pretty</p>
              <p class="t-out">up 6 semesters, studying hard</p>
              <br/>
              <p class="t-cmd"><span class="t-prompt">$</span> pacman -Syu knowledge</p>
              <p class="t-out">:: Upgrading packages...</p>
              <p class="t-out t-green">  web-dev-skills  ████████ 100%</p>
              <p class="t-out t-green">  multi-os-skills ████████ 100%</p>
              <p class="t-out t-arch">  oop-patterns    ██████░░  75%</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { MapPin, ChevronRight, GraduationCap } from '@lucide/vue'

const experiences = [
  {
    role: 'Software Engineering Intern',
    company: 'Telkom University',
    location: 'Jakarta',
    period: 'Jul 2026 - Sep 2026',
    bullets: [
      'Developed a full-stack, mobile-friendly web platform for KPPM (Kerja Praktik Pengabdian Masyarakat) Telkom University Jakarta',
      'Architected the system using a microservice pattern, separating concerns across independent backend services with Express.js',
      'Built a responsive, mobile-first frontend using Next.js with server-side rendering for optimal performance',
      'Collaborated with a team to deliver a production-ready platform covering the full project lifecycle',
    ],
  },
  {
    role: 'Administration Intern',
    company: 'PT Lotte Shopping Indonesia',
    location: 'Jakarta',
    period: 'Sep 2022 - Dec 2022',
    bullets: [
      'Recorded and verified daily sales data into SAP and Microsoft Excel to ensure accuracy of operational reports',
      'Requested approval for daily sales data printouts from Head of Administration, Manager, and General Manager',
      'Digitalized and consolidated corporate expense receipts into PDF format to streamline documentation and audit',
      'Maintained physical document archiving system and assisted during annual physical inventory count',
    ],
  },
]
</script>

<style scoped>
.exp-layout {
  display: grid;
  grid-template-columns: 1.3fr 1fr;
  gap: 40px;
  align-items: start;
}

.timeline { display: flex; flex-direction: column; }

.timeline-item {
  display: flex;
  gap: 20px;
}

.timeline-marker {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding-top: 24px;
  flex-shrink: 0;
}

.timeline-dot {
  width: 14px;
  height: 14px;
  border-radius: 50%;
  background: var(--arch-blue);
  border: 2px solid #000;
  flex-shrink: 0;
}

.timeline-line {
  width: 1px;
  flex: 1;
  background: var(--border-dim);
  margin-top: 8px;
  min-height: 40px;
}

.timeline-card { flex: 1; margin-bottom: 24px; }

.exp-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  gap: 16px;
  margin-bottom: 16px;
  flex-wrap: wrap;
}

.exp-role {
  font-size: 1rem;
  font-weight: 700;
  color: var(--text-primary);
  margin-bottom: 4px;
}

.exp-company {
  font-family: var(--font-mono);
  font-size: 0.85rem;
  color: var(--arch-blue);
  margin-bottom: 4px;
}

.exp-location {
  display: flex;
  align-items: center;
  gap: 4px;
  font-size: 0.78rem;
  color: var(--text-dim);
}

.loc-icon { color: var(--text-dim); flex-shrink: 0; }

.period-badge {
  font-family: var(--font-mono);
  font-size: 0.72rem;
  color: var(--green-terminal);
  border: 1px solid rgba(124, 184, 124, 0.28);
  background: rgba(124, 184, 124, 0.08);
  padding: 4px 10px;
  border-radius: 4px;
  white-space: nowrap;
}

.exp-bullets {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.exp-bullets li {
  font-size: 0.83rem;
  color: var(--text-secondary);
  line-height: 1.6;
  display: flex;
  align-items: flex-start;
  gap: 6px;
}

.bullet-icon { color: var(--arch-blue); flex-shrink: 0; margin-top: 2px; }

.edu-panel { display: flex; flex-direction: column; gap: 20px; }

.edu-card { text-align: center; }

.edu-icon-wrap {
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 12px;
}

.edu-icon { color: var(--arch-blue); }

.edu-title {
  font-size: 1rem;
  font-weight: 700;
  color: var(--arch-blue);
  margin-bottom: 16px;
  font-family: var(--font-mono);
}

.edu-detail { display: flex; flex-direction: column; gap: 6px; align-items: center; }

.edu-school {
  font-size: 1rem;
  font-weight: 600;
  color: var(--text-primary);
}

.edu-major {
  font-size: 0.85rem;
  color: var(--text-secondary);
}

.edu-meta {
  font-size: 0.78rem;
  color: var(--text-dim);
  font-family: var(--font-mono);
  display: flex;
  align-items: center;
  gap: 4px;
}

.gpa-badge {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 8px 20px;
  background: var(--arch-blue-dim);
  border: 1px solid var(--border-arch);
  border-radius: 8px;
  margin-top: 8px;
}

.gpa-label {
  font-family: var(--font-mono);
  font-size: 0.75rem;
  color: var(--text-dim);
  text-transform: uppercase;
}

.gpa-value {
  font-family: var(--font-mono);
  font-size: 1.1rem;
  font-weight: 700;
  color: var(--green-terminal);
}

.edu-terminal .terminal-body { padding: 16px 20px; }
.t-prompt { color: var(--arch-blue); font-family: var(--font-mono); }
.t-cmd { font-family: var(--font-mono); font-size: 0.78rem; color: var(--text-primary); margin-bottom: 4px; }
.t-out { font-family: var(--font-mono); font-size: 0.75rem; color: var(--text-secondary); padding-left: 12px; line-height: 1.8; }
.t-green { color: var(--green-terminal); }
.t-arch { color: var(--arch-blue); }

@media (max-width: 768px) {
  .exp-layout { grid-template-columns: 1fr; }
}
</style>

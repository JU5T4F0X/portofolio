<template>
  <section id="contact" class="section">
    <div class="container">
      <p class="section-label">// 06. contact</p>
      <h2 class="section-title">Get In Touch</h2>

      <div class="contact-layout">
        <!-- Terminal contact form -->
        <div class="terminal-window contact-terminal">
          <div class="terminal-header">
            <div class="terminal-dot red"></div>
            <div class="terminal-dot yellow"></div>
            <div class="terminal-dot green"></div>
            <span class="terminal-title">send-message.sh</span>
          </div>
          <div class="terminal-body">
            <p class="ct-line"><span class="ct-comment">#!/bin/bash</span></p>
            <p class="ct-line"><span class="ct-comment"># Reach out to Denis</span></p>
            <br/>
            <p class="ct-line">
              <span class="ct-key">NAME</span>=<span class="ct-str">"<input
                v-model="form.name"
                class="ct-input"
                placeholder="your name"
                id="contact-name"
              />"</span>
            </p>
            <p class="ct-line">
              <span class="ct-key">EMAIL</span>=<span class="ct-str">"<input
                v-model="form.email"
                class="ct-input"
                placeholder="your@email.com"
                id="contact-email"
              />"</span>
            </p>
            <p class="ct-line">
              <span class="ct-key">MESSAGE</span>=<span class="ct-str">"<input
                v-model="form.message"
                class="ct-input ct-input-wide"
                placeholder="your message here"
                id="contact-message"
              />"</span>
            </p>
            <br/>
            <p class="ct-line"><span class="ct-comment"># Send!</span></p>
            <button class="ct-run-btn" @click="handleSubmit" id="contact-submit">
              <ChevronRight :size="14" />
              ./send-message.sh
            </button>
            <p class="ct-success" v-if="submitted">
              <Check :size="13" style="display:inline;vertical-align:middle;" />
              Message sent! Redirecting to email client...
            </p>
          </div>
        </div>

        <!-- Contact info -->
        <div class="contact-info">
          <p class="contact-intro">
            I'm open to <span class="hl">Software Engineering internships</span> and
            collaborations. Feel free to reach out.
          </p>

          <div class="contact-links">
            <a
              v-for="link in contactLinks"
              :key="link.label"
              :href="link.href"
              :id="link.id"
              class="contact-link-card"
              target="_blank"
              rel="noopener noreferrer"
            >
              <div class="cl-icon-wrap">
                <component :is="link.icon" :size="18" class="cl-icon" />
              </div>
              <div class="cl-info">
                <span class="cl-label">{{ link.label }}</span>
                <span class="cl-value">{{ link.value }}</span>
              </div>
              <ArrowRight :size="16" class="cl-arrow" />
            </a>
          </div>

          <div class="arch-footer-hint">
            <ArchLogo :size="18" />
            <span>Made on Arch Linux</span>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { Mail, Phone, GitBranch, ExternalLink, MapPin, ChevronRight, ArrowRight, Check } from '@lucide/vue'
import ArchLogo from './ArchLogo.vue'

const form = ref({ name: '', email: '', message: '' })
const submitted = ref(false)

const contactLinks = [
  {
    id: 'contact-email-link',
    icon: Mail,
    label: 'Email',
    value: 'hendrikdenis3@gmail.com',
    href: 'mailto:hendrikdenis3@gmail.com',
  },
  {
    id: 'contact-phone-link',
    icon: Phone,
    label: 'Phone',
    value: '+62-819-0634-0877',
    href: 'tel:+6281906340877',
  },
  {
    id: 'contact-github-link',
    icon: GitBranch,
    label: 'GitHub',
    value: 'github.com/JU5T4F0X',
    href: 'https://github.com/JU5T4F0X',
  },
  {
    id: 'contact-linkedin-link',
    icon: ExternalLink,
    label: 'LinkedIn',
    value: 'linkedin.com/in/denis-hendri',
    href: 'https://linkedin.com/in/denis-hendri-wawo',
  },
  {
    id: 'contact-location-link',
    icon: MapPin,
    label: 'Location',
    value: 'Jakarta Pusat, Indonesia',
    href: 'https://maps.google.com/?q=Jakarta+Pusat',
  },
]

const handleSubmit = () => {
  if (!form.value.name || !form.value.email || !form.value.message) return
  const subject = encodeURIComponent(`Portfolio Contact from ${form.value.name}`)
  const body = encodeURIComponent(`Name: ${form.value.name}\nEmail: ${form.value.email}\n\nMessage:\n${form.value.message}`)
  window.open(`mailto:hendrikdenis3@gmail.com?subject=${subject}&body=${body}`, '_blank')
  submitted.value = true
  setTimeout(() => { submitted.value = false }, 3000)
}
</script>

<style scoped>
.contact-layout {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 48px;
  align-items: start;
}

.contact-terminal .terminal-body { padding: 20px 24px; }

.ct-line {
  font-family: var(--font-mono);
  font-size: 0.83rem;
  line-height: 2;
  color: var(--text-primary);
}

.ct-comment { color: var(--text-dim); font-style: italic; }
.ct-key { color: var(--arch-blue); font-weight: 600; }
.ct-str { color: var(--green-terminal); }

.ct-input {
  background: transparent;
  border: none;
  border-bottom: 1px solid var(--border-arch);
  color: var(--green-terminal);
  font-family: var(--font-mono);
  font-size: 0.83rem;
  outline: none;
  padding: 0 4px;
  width: 140px;
  transition: border-color var(--transition);
}

.ct-input-wide { width: 200px; }

.ct-input:focus {
  border-bottom-color: var(--arch-blue);
}

.ct-input::placeholder { color: var(--text-dim); }

.ct-run-btn {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  background: var(--arch-blue-dim);
  border: 1px solid var(--border-arch);
  border-radius: 6px;
  padding: 8px 16px;
  font-family: var(--font-mono);
  font-size: 0.83rem;
  color: var(--arch-blue);
  cursor: pointer;
  transition: var(--transition);
  margin-top: 8px;
}

.ct-run-btn:hover {
  background: rgba(23, 147, 209, 0.16);
}

.ct-success {
  font-family: var(--font-mono);
  font-size: 0.8rem;
  color: var(--green-terminal);
  margin-top: 8px;
  display: flex;
  align-items: center;
  gap: 6px;
  animation: fadeIn 0.4s ease;
}

.contact-intro {
  font-size: 0.95rem;
  color: var(--text-secondary);
  line-height: 1.7;
  margin-bottom: 28px;
}

.hl { color: var(--arch-blue); font-weight: 500; }

.contact-links { display: flex; flex-direction: column; gap: 12px; margin-bottom: 28px; }

.contact-link-card {
  display: flex;
  align-items: center;
  gap: 14px;
  padding: 14px 18px;
  background: var(--bg-card);
  border: 1px solid var(--border-dim);
  border-radius: 10px;
  text-decoration: none;
  transition: var(--transition);
  color: inherit;
}

.contact-link-card:hover {
  border-color: var(--border-arch);
  background: var(--bg-card-hover);
}

.cl-icon-wrap {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 36px;
  height: 36px;
  border-radius: 8px;
  background: var(--arch-blue-dim);
  border: 1px solid var(--border-arch);
  flex-shrink: 0;
}

.cl-icon { color: var(--arch-blue); }

.cl-info { flex: 1; display: flex; flex-direction: column; gap: 2px; }

.cl-label {
  font-family: var(--font-mono);
  font-size: 0.68rem;
  color: var(--text-dim);
  text-transform: uppercase;
  letter-spacing: 0.1em;
}

.cl-value {
  font-size: 0.85rem;
  color: var(--text-primary);
}

.cl-arrow {
  color: var(--arch-blue);
  opacity: 0.6;
  transition: transform var(--transition);
}

.contact-link-card:hover .cl-arrow {
  opacity: 1;
  transform: translateX(4px);
}

.arch-footer-hint {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  font-family: var(--font-mono);
  font-size: 0.78rem;
  color: var(--text-dim);
}

@media (max-width: 768px) {
  .contact-layout { grid-template-columns: 1fr; }
  .ct-input, .ct-input-wide { width: 100px; }
}
</style>

<script setup lang="ts">
import { ref, reactive, onMounted, onUnmounted } from 'vue'

import img1 from '../assets/mockups/mypetpal/1.png'
import img2 from '../assets/mockups/mypetpal/2.png'
import img3 from '../assets/mockups/mypetpal/3.png'
import img4 from '../assets/mockups/mypetpal/4.png'
import img5 from '../assets/mockups/mypetpal/5.png'

import geo1 from '../assets/mockups/geoaura/1.png'
import geo2 from '../assets/mockups/geoaura/2.png'
import geo3 from '../assets/mockups/geoaura/3.png'
import geo4 from '../assets/mockups/geoaura/4.png'
import geo5 from '../assets/mockups/geoaura/5.png'

import logoAngular from '../assets/logos/Angular.svg'
import logoFastAPI from '../assets/logos/FastAPI.svg'
import logoFigma from '../assets/logos/Figma.svg'
import logoNET from '../assets/logos/NET.svg'
import logoTypeScript from '../assets/logos/TypeScript.svg'
import logoSignalR from '../assets/logos/signalr.svg'

interface Project {
  id: string
  title: string
  tagline: string
  description: string
  images: string[]
  techStack: { name: string; icon: string; isImage?: boolean }[]
  appUrl?: string
  githubLinks?: { label: string; url: string }[]
}

const projects: Project[] = [
  {
    id: 'mypetpal',
    title: 'My Pet Pal',
    tagline: 'A cozy virtual pet game. Create your own world of retro calm.',
    description:
      'MyPetPal is an virtual pet simulation where players design and manage their own digital pet sanctuaries. The web based game features unlimited customisation, allowing users to build environments by placing furniture, constructing custom areas with walls, and arranging decor. Beyond environment building, the game includes interactive pet care, social features like adding friends for real-time connection, and mini-games.',
    images: [img1, img2, img3, img4, img5],
    techStack: [
      { name: '.NET', icon: logoNET, isImage: true },
      { name: 'Entity Framework Core', icon: '🗄️' },
      { name: 'SignalR', icon: logoSignalR, isImage: true },
      { name: 'Angular', icon: logoAngular, isImage: true },
      { name: 'TypeScript', icon: logoTypeScript, isImage: true },
      { name: 'REST API', icon: '🔗' },
    ],
    appUrl: 'https://mypetpal.aswanth.net',
    githubLinks: [
      { label: 'API', url: 'https://github.com/Ash66hub/mypetpal-api' },
      { label: 'UI', url: 'https://github.com/Ash66hub/mypetpal-ui' },
    ],
  },
  {
    id: 'geoaura',
    title: 'GeoAura NZ',
    tagline: 'Agentic Urban Risk Analysis for NZ.',
    description:
      'GeoAura NZ is an AI-powered geospatial due‑diligence platform for New Zealand property and compliance. Acting as a professional precursor to a LIM report, it unifies fragmented data into instant, legally-cited risk assessments. The platform features an interactive map with specialized layers including suburb-level rent data, historic seismic events, Police crime incidents, flooding areas, and traffic volume statistics. Using agentic workflows to reason over these spatial layers, the system generates clear, actionable risk narratives to evaluate site feasibility faster than manual research.',
    images: [geo1, geo2, geo3, geo4, geo5],
    techStack: [
      { name: 'Angular 21', icon: logoAngular, isImage: true },
      { name: 'MapLibre GL JS', icon: '🗺️' },
      { name: 'FastAPI', icon: logoFastAPI, isImage: true },
      { name: 'Gemini 1.5 Flash', icon: '✨' },
      { name: 'Supabase', icon: '🔒' },
    ],
    appUrl: 'https://geoaura.aswanth.net',
    githubLinks: [
      { label: 'Monorepo', url: 'https://github.com/Ash66hub/geoaura-nz' },
    ],
  },
]

// Per-project carousel state
const carouselState = reactive<Record<string, { index: number; transitioning: boolean }>>(
  Object.fromEntries(projects.map((p) => [p.id, { index: 0, transitioning: false }]))
)

const timers: Record<string, ReturnType<typeof setInterval>> = {}

function goTo(projectId: string, index: number) {
  const state = carouselState[projectId]
  if (state.transitioning) return
  state.transitioning = true
  state.index = index
  resetAutoplay(projectId)
  setTimeout(() => { state.transitioning = false }, 500)
}

function next(projectId: string) {
  const project = projects.find((p) => p.id === projectId)!
  goTo(projectId, (carouselState[projectId].index + 1) % project.images.length)
}

function prev(projectId: string) {
  const project = projects.find((p) => p.id === projectId)!
  const len = project.images.length
  goTo(projectId, (carouselState[projectId].index - 1 + len) % len)
}

function resetAutoplay(projectId: string) {
  if (timers[projectId]) clearInterval(timers[projectId])
  timers[projectId] = setInterval(() => next(projectId), 5000)
}

onMounted(() => {
  projects.forEach((p) => resetAutoplay(p.id))
})

onUnmounted(() => {
  Object.values(timers).forEach(clearInterval)
})
</script>

<template>
  <div class="projects-page">
    <div class="projects-scroll">

      <template
        v-for="(project, pi) in projects"
        :key="project.id"
      >
        <div
          class="project-card"
          :style="{ animationDelay: `${pi * 0.15}s` }"
        >
          <!-- Carousel -->
          <div class="carousel">
            <div class="carousel-viewport">
              <div
                class="carousel-track"
                :style="{ transform: `translateX(-${carouselState[project.id].index * 100}%)` }"
              >
                <div
                  v-for="(img, i) in project.images"
                  :key="i"
                  class="carousel-slide"
                >
                  <img :src="img" :alt="`${project.title} screenshot ${i + 1}`" />
                </div>
              </div>

              <!-- Nav arrows -->
              <button class="carousel-btn carousel-btn--prev" @click="prev(project.id)" aria-label="Previous image">
                <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round">
                  <polyline points="15 18 9 12 15 6" />
                </svg>
              </button>
              <button class="carousel-btn carousel-btn--next" @click="next(project.id)" aria-label="Next image">
                <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round">
                  <polyline points="9 18 15 12 9 6" />
                </svg>
              </button>
            </div>

            <!-- Dots -->
            <div class="carousel-dots">
              <button
                v-for="(_, i) in project.images"
                :key="i"
                :class="['dot', { active: carouselState[project.id].index === i }]"
                @click="goTo(project.id, i)"
                :aria-label="`Go to image ${i + 1}`"
              />
            </div>
          </div>

          <!-- Project Info -->
          <div class="project-info">
            <h2 class="project-title">{{ project.title }}</h2>
            <p class="project-tagline">{{ project.tagline }}</p>
            <p class="project-description">{{ project.description }}</p>

            <div class="tech-section">
              <h3 class="tech-heading">Tech Stack</h3>
              <div class="tech-grid">
                <span v-for="tech in project.techStack" :key="tech.name" class="tech-badge">
                  <span class="tech-icon">
                    <img v-if="tech.isImage" :src="tech.icon" :alt="tech.name" class="tech-logo" />
                    <template v-else>{{ tech.icon }}</template>
                  </span>
                  {{ tech.name }}
                </span>
              </div>
            </div>

            <!-- Project Links -->
            <div class="project-links">
              <a
                v-if="project.appUrl"
                :href="project.appUrl"
                target="_blank"
                rel="noopener noreferrer"
                class="link-btn link-btn--primary"
              >
                <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                  <path d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6" />
                  <polyline points="15 3 21 3 21 9" />
                  <line x1="10" y1="14" x2="21" y2="3" />
                </svg>
                Open App
              </a>
              <a
                v-for="link in project.githubLinks"
                :key="link.url"
                :href="link.url"
                target="_blank"
                rel="noopener noreferrer"
                class="link-btn link-btn--github"
              >
                <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor">
                  <path d="M12 0C5.37 0 0 5.37 0 12c0 5.31 3.435 9.795 8.205 11.385.6.105.825-.255.825-.57 0-.285-.015-1.23-.015-2.235-3.015.555-3.795-.735-4.035-1.41-.135-.345-.72-1.41-1.23-1.695-.42-.225-1.02-.78-.015-.795.945-.015 1.62.87 1.845 1.23 1.08 1.815 2.805 1.305 3.495.99.105-.78.42-1.305.765-1.605-2.67-.3-5.46-1.335-5.46-5.925 0-1.305.465-2.385 1.23-3.225-.12-.3-.54-1.53.12-3.18 0 0 1.005-.315 3.3 1.23.96-.27 1.98-.405 3-.405s2.04.135 3 .405c2.295-1.56 3.3-1.23 3.3-1.23.66 1.65.24 2.88.12 3.18.765.84 1.23 1.905 1.23 3.225 0 4.605-2.805 5.625-5.475 5.925.435.375.81 1.095.81 2.22 0 1.605-.015 2.895-.015 3.3 0 .315.225.69.825.57A12.02 12.02 0 0 0 24 12c0-6.63-5.37-12-12-12z" />
                </svg>
                GitHub · {{ link.label }}
              </a>
            </div>
          </div>
        </div>

        <!-- Divider between projects -->
        <div v-if="pi < projects.length - 1" class="project-divider"></div>
      </template>

    </div>
  </div>
</template>

<style scoped>
.projects-page {
  flex: 1;
  background-color: var(--bg-dark);
  height: 100%;
  overflow: hidden;
}

.projects-scroll {
  height: 100%;
  overflow-y: auto;
  padding: 2.5rem 3rem;
  scrollbar-width: thin;
  scrollbar-color: var(--border-color) transparent;
}

.projects-scroll::-webkit-scrollbar {
  width: 6px;
}

.projects-scroll::-webkit-scrollbar-track {
  background: transparent;
}

.projects-scroll::-webkit-scrollbar-thumb {
  background: var(--border-color);
  border-radius: 3px;
}

/* ── Project Card ── */
.project-card {
  max-width: 900px;
  margin: 0 auto;
  display: flex;
  gap: 3.5rem;
  align-items: flex-start;
  animation: cardFadeIn 0.6s ease-out both;
}

.project-divider {
  margin: 3rem auto;
  max-width: 900px;
  height: 1px;
  background: linear-gradient(
    90deg,
    transparent 0%,
    var(--border-color) 20%,
    var(--border-color) 80%,
    transparent 100%
  );
}

@keyframes cardFadeIn {
  from { opacity: 0; transform: translateY(24px); }
  to   { opacity: 1; transform: translateY(0); }
}

/* ── Carousel ── */
.carousel {
  display: flex;
  flex-direction: column;
  gap: 0.6rem;
  width: 370px;
  min-width: 370px;
}

.carousel-viewport {
  position: relative;
  width: 100%;
  aspect-ratio: 1 / 1;
  border-radius: 0.85rem;
  overflow: hidden;
  background: var(--card-bg);
  border: 1px solid var(--border-color);
}

.carousel-track {
  display: flex;
  height: 100%;
  transition: transform 0.5s cubic-bezier(0.16, 1, 0.3, 1);
}

.carousel-slide {
  min-width: 100%;
  height: 100%;
}

.carousel-slide img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
}

/* Arrow buttons */
.carousel-btn {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  width: 38px;
  height: 38px;
  border-radius: 50%;
  background: rgba(0, 0, 0, 0.45);
  backdrop-filter: blur(8px);
  color: #fff;
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  transition: all 0.3s ease;
  border: 1px solid rgba(255, 255, 255, 0.1);
}

.carousel-viewport:hover .carousel-btn {
  opacity: 1;
}

.carousel-btn:hover {
  background: rgba(0, 0, 0, 0.7);
  transform: translateY(-50%) scale(1.08);
}

.carousel-btn--prev { left: 12px; }
.carousel-btn--next { right: 12px; }

/* Dots */
.carousel-dots {
  display: flex;
  justify-content: center;
  gap: 0.4rem;
}

.dot {
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background: var(--border-color);
  transition: all 0.35s ease;
  padding: 0;
}

.dot.active {
  background: #ffaf61;
  width: 24px;
  border-radius: 4px;
}

/* ── Project Info ── */
.project-info {
  padding: 0.25rem 0 0;
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
  flex: 1;
  min-width: 0;
}

.project-title {
  font-size: 1.8rem;
  font-weight: 700;
  letter-spacing: -0.03em;
  background: var(--color-accent);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.project-tagline {
  font-size: 1rem;
  color: var(--text-secondary);
  font-style: italic;
  font-weight: 300;
}

.project-description {
  font-size: 0.9rem;
  line-height: 1.75;
  color: var(--text-secondary);
}

/* ── Tech Stack ── */
.tech-section {
  margin-top: 0.5rem;
}

.tech-heading {
  font-size: 0.72rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.12em;
  color: var(--text-secondary);
  margin-bottom: 0.7rem;
}

.tech-grid {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.tech-badge {
  display: inline-flex;
  align-items: center;
  gap: 0.4rem;
  padding: 0.35rem 0.85rem;
  background: var(--card-bg);
  border: 1px solid var(--border-color);
  border-radius: 9999px;
  font-size: 0.78rem;
  font-weight: 500;
  color: var(--text-primary);
  transition: all 0.3s ease;
}

.tech-badge:hover {
  background: var(--card-hover-bg);
  border-color: var(--text-secondary);
  transform: translateY(-2px);
}

.tech-icon {
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 0.9rem;
  line-height: 1;
}

.tech-logo {
  width: 16px;
  height: 16px;
  object-fit: contain;
}

/* ── Project Links ── */
.project-links {
  display: flex;
  flex-wrap: wrap;
  gap: 0.6rem;
  margin-top: 0.75rem;
}

.link-btn {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.5rem 1.1rem;
  border-radius: 0.5rem;
  font-size: 0.82rem;
  font-weight: 600;
  text-decoration: none;
  transition: all 0.3s cubic-bezier(0.16, 1, 0.3, 1);
  cursor: pointer;
}

.link-btn--primary {
  background: var(--color-accent);
  color: var(--bg-dark);
  box-shadow: 0 3px 12px rgba(255, 175, 97, 0.2);
}

.link-btn--primary:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(255, 175, 97, 0.4);
  background: var(--color-accent-hover);
}

.link-btn--primary svg {
  stroke: var(--bg-dark);
}

.link-btn--github {
  background: transparent;
  border: 1px solid var(--border-color);
  color: var(--text-primary);
}

.link-btn--github:hover {
  background: rgba(255, 255, 255, 0.05);
  border-color: var(--text-secondary);
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
}

/* ── Responsive ── */
@media (max-width: 1100px) {
  .carousel {
    width: 320px;
    min-width: 320px;
  }

  .project-card {
    gap: 3rem;
  }
}

@media (max-width: 900px) {
  .projects-scroll {
    padding: 2rem 1.5rem;
  }

  .project-card {
    flex-direction: column;
    max-width: 500px;
    gap: 0;
  }

  .carousel {
    width: 100%;
    min-width: 0;
  }

  .project-info {
    padding: 1.5rem 0 2rem;
  }

  .project-title {
    font-size: 1.5rem;
  }

  .project-tagline {
    font-size: 0.9rem;
  }

  .project-description {
    font-size: 0.85rem;
  }

  .carousel-viewport {
    border-radius: 0.75rem;
  }

  .carousel-btn {
    width: 32px;
    height: 32px;
    opacity: 1;
  }

  .carousel-btn--prev { left: 8px; }
  .carousel-btn--next { right: 8px; }

  .carousel-btn svg {
    width: 14px;
    height: 14px;
  }

  .tech-badge {
    font-size: 0.72rem;
    padding: 0.3rem 0.7rem;
  }

  .project-divider {
    margin: 2rem 0;
  }

  .link-btn {
    font-size: 0.75rem;
    padding: 0.4rem 0.9rem;
  }
}

@media (max-width: 480px) {
  .projects-scroll {
    padding: 1rem;
  }

  .project-card {
    max-width: 100%;
  }

  .project-title {
    font-size: 1.3rem;
  }

  .project-info {
    padding: 1.25rem 0 1.5rem;
    gap: 0.5rem;
  }

  .tech-grid {
    gap: 0.35rem;
  }

  .tech-badge {
    font-size: 0.68rem;
    padding: 0.25rem 0.6rem;
  }

  .project-links {
    gap: 0.4rem;
  }

  .link-btn {
    font-size: 0.7rem;
    padding: 0.35rem 0.75rem;
    gap: 0.35rem;
  }

  .link-btn svg {
    width: 13px;
    height: 13px;
  }
}
</style>

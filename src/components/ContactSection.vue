<script setup lang="ts">
  import resumeUrl from '../assets/resume/CV_Aswanth.pdf';
  const contacts = [
    {
      name: 'Email',
      value: 'hi@aswanth.net',
      url: 'mailto:hi@aswanth.net',
      icon: 'M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z M22 6l-10 7L2 6',
    },
    {
      name: 'LinkedIn',
      value: 'Aswanth H B',
      url: 'https://www.linkedin.com/in/aswanth-hb/',
      icon: 'M16 8a6 6 0 0 1 6 6v7h-4v-7a2 2 0 0 0-2-2 2 2 0 0 0-2 2v7h-4v-7a6 6 0 0 1 6-6z M2 9h4v12H2z M4 2a2 2 0 1 1-2 2 2 2 0 0 1 2-2z',
    },
    {
      name: 'GitHub',
      value: 'Ash66hub',
      url: 'https://github.com/Ash66hub',
      icon: 'M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 0 0-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0 0 20 4.77 5.07 5.07 0 0 0 19.91 1S18.73.65 16 2.48a13.38 13.38 0 0 0-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 0 0 5 4.77a5.44 5.44 0 0 0-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 0 0 9 18.13V22',
    }
  ]

  const socials = [
    {
      name: 'Instagram',
      value: '@__sic___',
      url: 'https://www.instagram.com/__sic___/',
      icon: 'M17 2H7a5 5 0 0 0-5 5v10a5 5 0 0 0 5 5h10a5 5 0 0 0 5-5V7a5 5 0 0 0-5-5z M12 7a5 5 0 1 1 0 10 5 5 0 0 1 0-10z M17.5 6.5a1.5 1.5 0 1 1 0 3 1.5 1.5 0 0 1 0-3z',
    },
    {
      name: 'YouTube',
      value: '@AswanthHB',
      url: 'https://www.youtube.com/@AswanthHB',
      icon: 'M22.54 6.42a2.78 2.78 0 0 0-1.94-2C18.88 4 12 4 12 4s-6.88 0-8.6.46a2.78 2.78 0 0 0-1.94 2A29 29 0 0 0 1 11.75a29 29 0 0 0 .46 5.33A2.78 2.78 0 0 0 3.4 19.1c1.72.46 8.6.46 8.6.46s6.88 0 8.6-.46a2.78 2.78 0 0 0 1.94-2 29 29 0 0 0 .46-5.25 29 29 0 0 0-.46-5.43z M9.75 15.02V8.48L15.45 11.75l-5.7 3.27z',
    }
  ]
</script>

<template>
  <div class="section-container">
    <div class="contact-block">
      <div class="header">
        <h1 class="title">Get in Touch</h1>
        <p class="subtitle">Always open to chat - tech or otherwise!</p>
        <div class="resume-cta">
          <a :href="resumeUrl" download="CV_Aswanth.pdf" target="_blank" class="btn-resume">
            <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v4"/><polyline points="7 10 12 15 17 10"/><line x1="12" y1="15" x2="12" y2="3"/></svg>
            Download CV
          </a>
        </div>
      </div>

      <div class="grid">
        <a 
          v-for="contact in contacts" 
          :key="contact.name" 
          :href="contact.url" 
          target="_blank" 
          class="card"
        >
          <div class="icon-wrapper">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
              <path :d="contact.icon" />
            </svg>
          </div>
          <div class="info">
            <span class="label">{{ contact.name }}</span>
            <span class="value">{{ contact.value }}</span>
          </div>
        </a>
      </div>
    </div>

    <div class="contact-block">
      <div class="header">
        <h2 class="section-title">Personal</h2>
        <p class="subtitle">Outside of work and web dev fun, I make instrumental noises and other randomities.</p>
      </div>

      <div class="grid">
        <a 
          v-for="social in socials" 
          :key="social.name" 
          :href="social.url" 
          target="_blank" 
          class="card"
        >
          <div class="icon-wrapper">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
              <path :d="social.icon" />
            </svg>
          </div>
          <div class="info">
            <span class="label">{{ social.name }}</span>
            <span class="value">{{ social.value }}</span>
          </div>
        </a>
      </div>
    </div>
  </div>
</template>

<style scoped src="../assets/styles/sections.css"></style>

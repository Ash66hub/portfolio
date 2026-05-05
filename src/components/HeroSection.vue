<script setup lang="ts">
const resumeUrl = 'https://awntqvnovwpwyxiqexfr.supabase.co/storage/v1/object/public/portfolio-CV/CV_Aswanth.pdf';
defineEmits(['navigate']);
</script>

<template>
  <section class="hero">
    <div class="hero-content">
      <h3 class="subtitle">Hi, I am</h3>
      <h1 class="title">
        <span class="first-name">Aswanth</span>
        <span class="full-name">Harilal Bindhu</span>
      </h1>
      <h2 class="role">Full Stack Web Developer</h2>
      
      <div class="cta-group">
        <div class="primary-actions">
          <button class="btn btn-primary" @click="$emit('navigate', 'Projects')">Projects</button>
          <button class="btn btn-primary" @click="$emit('navigate', 'Contact')">Contact</button>
        </div>
        <div class="secondary-actions">
          <a :href="resumeUrl" download="CV_Aswanth.pdf" target="_blank" class="btn btn-outline resume-btn">
            <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="icon"><path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v4"/><polyline points="7 10 12 15 17 10"/><line x1="12" y1="15" x2="12" y2="3"/></svg>
            Download CV
          </a>
        </div>
      </div>
    </div>
    
    <div class="hero-image-container">
      <img src="../assets/photo.png" class="hero-photo">
    </div>
  </section>
</template>

<style scoped src="../assets/styles/hero.css"></style>

<script setup lang="ts">
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
        <button class="btn btn-primary" @click="$emit('navigate', 'Projects')">Projects</button>
        <button class="btn btn-primary" @click="$emit('navigate', 'Contact')">Contact</button>
      </div>
    </div>
    
    <div class="hero-image-container">
      <img src="../assets/photo.png" class="hero-photo">
    </div>
  </section>
</template>

<style scoped src="../assets/styles/hero.css"></style>

<script setup lang="ts">
  import './assets/base.css'
  import VerticalSidebar from './components/VerticalSidebar.vue'
  import HeroSection from './components/HeroSection.vue'
</script>

<template>
  <div class="app-container">
    <VerticalSidebar label="Main" :isActive="true" />
    
    <HeroSection />
    
    <div class="sidebars-right">
      <VerticalSidebar label="Projects" />
      <VerticalSidebar label="Contact" />
    </div>
  </div>
</template>

<style>
  .app-container {
    display: flex;
    width: 100vw;
    height: 100vh;
    overflow: hidden;
  }

  .sidebars-right {
    display: flex;
  }


  @media (max-width: 768px) {
  .app-container {
    flex-direction: column;
  }
  
  .sidebars-right {
    display: none; 
  }
}
</style>

<script setup lang="ts">
  import { ref, computed } from 'vue'
  import './assets/base.css'
  import VerticalSidebar from './components/VerticalSidebar.vue'
  import HeroSection from './components/HeroSection.vue'
  import ProjectsSection from './components/ProjectsSection.vue'
  import ContactSection from './components/ContactSection.vue'

  const sections = ['Main', 'Projects', 'Contact']
  const activeSection = ref('Main')

  const currentComponent = computed(() => {
    switch (activeSection.value) {
      case 'Projects': return ProjectsSection
      case 'Contact': return ContactSection
      default: return HeroSection
    }
  })

  // We define the full sequence of items to render in the TransitionGroup
  const orderedItems = computed(() => {
    const activeIndex = sections.indexOf(activeSection.value)
    const left = sections.slice(0, activeIndex + 1)
    const right = sections.slice(activeIndex + 1)
    return [...left, 'CONTENT', ...right]
  })

  const setSection = (section: string) => {
    activeSection.value = section
  }
</script>

<template>
  <TransitionGroup 
    name="stack" 
    tag="div" 
    class="app-container"
  >
    <div 
      v-for="item in orderedItems" 
      :key="item"
      :class="['layout-item', item === 'CONTENT' ? 'content-item' : 'sidebar-item']"
    >
      <VerticalSidebar 
        v-if="item !== 'CONTENT'"
        :label="String(item)" 
        :isActive="activeSection === item" 
        @select="setSection"
      />
      
      <div v-else class="main-content">
        <Transition name="slide-fade" mode="out-in">
          <component 
            :is="currentComponent" 
            @navigate="setSection"
            :key="activeSection"
          />
        </Transition>
      </div>
    </div>
  </TransitionGroup>
</template>

<style src="./assets/styles/layout.css"></style>

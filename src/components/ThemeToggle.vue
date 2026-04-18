<script setup lang="ts">
import { ref, onMounted } from 'vue'

const isDark = ref(true)
const isPulling = ref(false)

const toggleTheme = () => {
  if (isPulling.value) return
  
  isPulling.value = true
  
  // Toggle theme
  isDark.value = !isDark.value
  const theme = isDark.value ? 'dark' : 'light'
  document.documentElement.setAttribute('data-theme', theme)
  localStorage.setItem('theme', theme)

  // Reset pulling state after animation
  setTimeout(() => {
    isPulling.value = false
  }, 200)
}

onMounted(() => {
  const savedTheme = localStorage.getItem('theme')
  if (savedTheme) {
    isDark.value = savedTheme === 'dark'
    document.documentElement.setAttribute('data-theme', savedTheme)
  } else {
    document.documentElement.setAttribute('data-theme', 'dark')
  }
})
</script>

<template>
  <div class="chord-container" :class="{ 'pulling': isPulling }">
    <div class="chord-knob"></div>
    <div class="chord-line"></div>
    <button 
      class="chord-handle" 
      @click="toggleTheme" 
      :title="isDark ? 'Switch to Light Mode' : 'Switch to Dark Mode'"
      aria-label="Toggle theme"
    >
      <div class="handle-inner"></div>
    </button>
  </div>
</template>

<style scoped>
.chord-container {
  position: fixed;
  top: 0;
  left: 75%;
  transform: translateX(-50%);
  z-index: 1000;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.chord-knob {
  width: 8px;
  height: 4px;
  background: var(--border-color);
  border-radius: 0 0 2px 2px;
  flex-shrink: 0;
}

.chord-line {
  width: 1px;
  height: 40px;
  background: var(--text-secondary);
  opacity: 0.4;
  transition: height 0.2s cubic-bezier(0.17, 0.67, 0.83, 0.67);
  transform-origin: top;
}

.pulling .chord-line {
  height: 55px;
}

.chord-handle {
  width: 16px;
  height: 32px;
  background: #f1f3f5;
  border: 1.5px solid var(--border-color);
  border-radius: 8px;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 0;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.15);
  transition: all 0.3s ease, transform 0.2s cubic-bezier(0.17, 0.67, 0.83, 0.67);
  position: relative;
  overflow: hidden;
  margin-top: -1px;
}

[data-theme='light'] .chord-handle {
  background: #fff;
  box-shadow: 0 0 15px rgba(255, 255, 255, 0.6), 0 2px 6px rgba(0, 0, 0, 0.1);
  border-color: #fff;
}

[data-theme='light'] .handle-inner {
  background: #f59e0b;
  box-shadow: 0 0 8px #f59e0b;
  opacity: 1;
}

.handle-inner {
  width: 5px;
  height: 14px;
  background: #555;
  border-radius: 2px;
  opacity: 0.4;
  transition: all 0.3s ease;
}

.chord-handle:hover {
  transform: scale(1.1);
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
}

.pulling .chord-handle {
  transform: scale(1);
}

/* On mobile, move it a bit higher or adjust size and position */
@media (max-width: 768px) {
  .chord-container {
    left: 75%;
  }

  .chord-line {
    height: 30px;
  }
  
  .pulling .chord-line {
    height: 45px;
  }
}
</style>

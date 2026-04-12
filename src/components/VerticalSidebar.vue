<script setup lang="ts">
defineProps<{
  label: string;
  isActive?: boolean;
}>();
</script>

<template>
  <div class="sidebar" :class="{ active: isActive }">
    <div class="label-container">
      <span class="label">{{ label }}</span>
    </div>
  </div>
</template>

<style scoped>
.sidebar {
  width: 60px;
  height: 100vh;
  background-color: var(--bg-sidebar);
  border-left: 1px solid var(--border-color);
  border-right: 1px solid var(--border-color);
  display: flex;
  align-items: center;
  justify-content: center;
  transition: background-color 0.3s ease;
}

.sidebar.active {
  background-color: var(--bg-sidebar-active);
}

.label-container {
  transform: rotate(90deg);
  white-space: nowrap;
}

.label {
  color: var(--text-primary);
  font-size: 1.5rem;
  font-weight: 600;
  letter-spacing: 1px;
  text-transform: capitalize;
}

/* For sidebars on the left/right, we might want to tweak borders */
</style>

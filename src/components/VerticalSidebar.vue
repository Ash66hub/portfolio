<script setup lang="ts">
defineProps<{
  label: string;
  isActive?: boolean;
}>();

defineEmits(['select']);
</script>

<template>
  <div 
    class="sidebar" 
    :class="{ active: isActive }"
    @click="$emit('select', label)"
  >
    <div class="label-container">
      <span class="label">{{ label }}</span>
    </div>
  </div>
</template>

<style scoped src="../assets/styles/sidebar.css"></style>

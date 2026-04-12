<script setup lang="ts"></script>

<template>
  <section class="hero">
    <div class="hero-content">
      <h3 class="subtitle">Hello, I am</h3>
      <h1 class="title">
        <span class="first-name">Aswanth</span>
        <span class="full-name">Harilal Bindhu</span>
      </h1>
      <h2 class="role">Full Stack Web Developer</h2>
      
      <div class="cta-group">
        <button class="btn btn-primary">Projects</button>
        <button class="btn btn-primary">Contact</button>
      </div>
    </div>
  </section>
</template>

<style scoped>
.hero {
  flex: 1;
  display: flex;
  align-items: center;
  padding-left: 10%;
  background-color: var(--bg-dark);
}

.hero-content {
  max-width: 90%;
  animation: fadeIn 1s ease-out;
}

.subtitle {
  color: var(--text-secondary);
  font-size: 2.5rem;
  font-weight: 400;
  margin-bottom: 1rem;
}

.title {
  color: #ffb76b;
  font-size: 6rem;
  font-weight: 700;
  line-height: 1;
  margin-bottom: 2rem;
  letter-spacing: -2px;
  cursor: default;
  display: flex;
  align-items: baseline;
  white-space: nowrap;
  transition: font-size 0.6s cubic-bezier(0.4, 0, 0.2, 1);
}

.title:hover {
  font-size: 3.8rem;
}

.first-name {
  display: inline-block;
}

.full-name {
  display: inline-block;
  max-width: 0;
  overflow: hidden;
  opacity: 0;
  white-space: nowrap;
  transition: all 0.6s cubic-bezier(0.4, 0, 0.2, 1);
  padding-left: 0;
}

.title:hover .full-name {
  max-width: 800px;
  opacity: 1;
  padding-left: 1.5rem;
}

.role {
  color: var(--text-primary);
  font-size: 2.5rem;
  font-weight: 700;
  margin-bottom: 3rem;
}

.cta-group {
  display: flex;
  gap: 1.5rem;
}

.btn {
  padding: 0.8rem 2.5rem;
  font-size: 1.2rem;
  font-weight: 600;
  border-radius: 4px;
  background: var(--color-accent);
  color: #111;
  box-shadow: 0 4px 15px rgba(255, 175, 97, 0.3);
}

.btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(255, 175, 97, 0.5);
  background: var(--color-accent-hover);
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@media (max-width: 768px) {
  .hero {
    padding-left: 5%;
  }
  .title {
    font-size: 4rem;
  }
  .subtitle, .role {
    font-size: 1.8rem;
  }
}
</style>

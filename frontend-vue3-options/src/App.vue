<template>
  <div>
    <nav class="nav">
      <div class="nav-container">
        <div class="nav-brand">
          <router-link to="/" class="brand-link">
            <span class="brand-text">Vue3 + Laravel</span>
          </router-link>
        </div>
        <div class="nav-links">
          <router-link to="/" class="nav-link">Home</router-link>
          <router-link to="/posts" class="nav-link">Posts</router-link>
        </div>
      </div>
    </nav>
    <main class="container">
      <router-view />
    </main>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style scoped>
.nav {
  background: var(--white);
  border-bottom: 1px solid var(--gray-200);
  box-shadow: var(--shadow-sm);
  position: sticky;
  top: 0;
  z-index: 100;
  backdrop-filter: blur(8px);
  background-color: rgba(255, 255, 255, 0.95);
}

.nav-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 var(--spacing-6);
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 4rem;
}

.nav-brand {
  display: flex;
  align-items: center;
}

.brand-link {
  display: flex;
  align-items: center;
  gap: var(--spacing-3);
  font-weight: 700;
  font-size: var(--font-size-lg);
  color: var(--gray-900);
  text-decoration: none;
  transition: all var(--transition-fast);
}

.brand-link:hover {
  color: var(--primary-color);
  text-decoration: none;
  transform: translateY(-1px);
}

.brand-icon {
  font-size: var(--font-size-2xl);
  filter: drop-shadow(0 2px 4px rgba(0, 0, 0, 0.1));
}

.brand-text {
  background: linear-gradient(135deg, var(--primary-color), var(--info-color));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.nav-links {
  display: flex;
  align-items: center;
  gap: var(--spacing-8);
}

.nav-link {
  color: var(--gray-600);
  font-weight: 500;
  text-decoration: none;
  padding: var(--spacing-2) var(--spacing-3);
  border-radius: var(--border-radius);
  transition: all var(--transition-fast);
  position: relative;
}

.nav-link:hover {
  color: var(--primary-color);
  background-color: var(--gray-100);
  text-decoration: none;
}

.nav-link.router-link-active {
  color: var(--primary-color);
  background-color: var(--primary-color);
  color: var(--white);
}

.nav-link.router-link-active::before {
  content: '';
  position: absolute;
  bottom: -1px;
  left: 50%;
  transform: translateX(-50%);
  width: 20px;
  height: 2px;
  background-color: var(--primary-color);
  border-radius: 1px;
}

.container {
  max-width: 1000px;
  margin: 0 auto;
  padding: var(--spacing-8) var(--spacing-6);
  min-height: calc(100vh - 4rem);
}

/* Responsividade */
@media (max-width: 768px) {
  .nav-container {
    padding: 0 var(--spacing-4);
    height: 3.5rem;
  }
  
  .container {
    padding: var(--spacing-6) var(--spacing-4);
  }
  
  .nav-links {
    gap: var(--spacing-4);
  }
  
  .brand-text {
    display: none;
  }
  
  .brand-icon {
    font-size: var(--font-size-xl);
  }
}

@media (max-width: 480px) {
  .nav-container {
    padding: 0 var(--spacing-3);
  }
  
  .container {
    padding: var(--spacing-4) var(--spacing-3);
  }
  
  .nav-links {
    gap: var(--spacing-3);
  }
  
  .nav-link {
    padding: var(--spacing-1) var(--spacing-2);
    font-size: var(--font-size-sm);
  }
}
</style>

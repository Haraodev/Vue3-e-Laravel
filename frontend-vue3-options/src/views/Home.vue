<template>
  <section class="home">
    <div class="hero">
      <div class="hero-content">
        <h1 class="hero-title">
          <span class="gradient-text">Vue3</span> + 
          <span class="gradient-text">Laravel</span>
        </h1>
        <p class="hero-subtitle">
          Uma aplicação moderna construída com Vue 3 (Options API) conectada ao backend Laravel robusto.
        </p>
        <div class="hero-features">
          <div class="feature">
            <span class="feature-icon">⚡</span>
            <span>Performance</span>
          </div>
          <div class="feature">
            <span class="feature-icon">🔒</span>
            <span>Segurança</span>
          </div>
          <div class="feature">
            <span class="feature-icon">📱</span>
            <span>Responsivo</span>
          </div>
        </div>
        <div class="hero-actions">
          <router-link to="/posts" class="btn btn-primary btn-lg">
            Ver Posts
            <span class="btn-icon">→</span>
          </router-link>
          <button class="btn btn-secondary btn-lg">
            Saiba Mais
          </button>
        </div>
      </div>
      <div class="hero-visual">
        <div class="code-block">
          <div class="code-header">
            <span class="code-dot"></span>
            <span class="code-dot"></span>
            <span class="code-dot"></span>
          </div>
          <div class="code-content">
            <pre><code>// Vue 3 Component
export default {
  name: 'App',
  data() {
    return {
      message: 'Hello World!'
    }
  }
}</code></pre>
          </div>
        </div>
      </div>
    </div>

    <div class="tech-stack">
      <h2 class="section-title">Tecnologias Utilizadas</h2>
      <div class="tech-grid">
        <div class="tech-card">
          <div class="tech-icon">🎨</div>
          <h3>Vue 3</h3>
          <p>Framework progressivo para interfaces de usuário</p>
        </div>
        <div class="tech-card">
          <div class="tech-icon">🚀</div>
          <h3>Laravel</h3>
          <p>Framework PHP elegante para desenvolvimento web</p>
        </div>
        <div class="tech-card">
          <div class="tech-icon">⚡</div>
          <h3>Vite</h3>
          <p>Build tool rápida para desenvolvimento moderno</p>
        </div>
        <div class="tech-card">
          <div class="tech-icon">🎯</div>
          <h3>API REST</h3>
          <p>Comunicação eficiente entre frontend e backend</p>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'Home'
}
</script>

<style scoped>
.home {
  animation: fadeIn 0.6s ease-out;
}

.hero {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: var(--spacing-16);
  align-items: center;
  margin-bottom: var(--spacing-16);
  padding: var(--spacing-8) 0;
}

.hero-content {
  max-width: 500px;
}

.hero-title {
  font-size: var(--font-size-4xl);
  font-weight: 800;
  line-height: 1.1;
  margin-bottom: var(--spacing-6);
  color: var(--gray-900);
}

.gradient-text {
  background: linear-gradient(135deg, var(--primary-color), var(--info-color));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.hero-subtitle {
  font-size: var(--font-size-lg);
  color: var(--gray-600);
  margin-bottom: var(--spacing-8);
  line-height: 1.6;
}

.hero-features {
  display: flex;
  gap: var(--spacing-6);
  margin-bottom: var(--spacing-8);
}

.feature {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: var(--spacing-2);
  color: var(--gray-600);
  font-size: var(--font-size-sm);
}

.feature-icon {
  font-size: var(--font-size-2xl);
  filter: drop-shadow(0 2px 4px rgba(0, 0, 0, 0.1));
}

.hero-actions {
  display: flex;
  gap: var(--spacing-4);
}

.btn-lg {
  padding: var(--spacing-4) var(--spacing-6);
  font-size: var(--font-size-lg);
  font-weight: 600;
}

.btn-icon {
  margin-left: var(--spacing-2);
  transition: transform var(--transition-fast);
}

.btn:hover .btn-icon {
  transform: translateX(4px);
}

.hero-visual {
  display: flex;
  justify-content: center;
  align-items: center;
}

.code-block {
  background: var(--gray-900);
  border-radius: var(--border-radius-xl);
  overflow: hidden;
  box-shadow: var(--shadow-xl);
  max-width: 400px;
  width: 100%;
}

.code-header {
  background: var(--gray-800);
  padding: var(--spacing-3);
  display: flex;
  gap: var(--spacing-2);
}

.code-dot {
  width: 12px;
  height: 12px;
  border-radius: 50%;
  background: var(--gray-500);
}

.code-dot:nth-child(1) { background: #ef4444; }
.code-dot:nth-child(2) { background: #f59e0b; }
.code-dot:nth-child(3) { background: #10b981; }

.code-content {
  padding: var(--spacing-6);
}

.code-content pre {
  margin: 0;
  color: var(--gray-100);
  font-family: 'Fira Code', 'Monaco', 'Consolas', monospace;
  font-size: var(--font-size-sm);
  line-height: 1.5;
}

.tech-stack {
  margin-top: var(--spacing-16);
}

.section-title {
  text-align: center;
  margin-bottom: var(--spacing-12);
  font-size: var(--font-size-3xl);
  color: var(--gray-900);
}

.tech-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: var(--spacing-6);
}

.tech-card {
  background: var(--white);
  padding: var(--spacing-6);
  border-radius: var(--border-radius-lg);
  box-shadow: var(--shadow);
  border: 1px solid var(--gray-200);
  text-align: center;
  transition: all var(--transition-normal);
}

.tech-card:hover {
  transform: translateY(-4px);
  box-shadow: var(--shadow-lg);
  border-color: var(--primary-color);
}

.tech-icon {
  font-size: var(--font-size-4xl);
  margin-bottom: var(--spacing-4);
  display: block;
  filter: drop-shadow(0 4px 8px rgba(0, 0, 0, 0.1));
}

.tech-card h3 {
  font-size: var(--font-size-lg);
  color: var(--gray-900);
  margin-bottom: var(--spacing-3);
}

.tech-card p {
  color: var(--gray-600);
  font-size: var(--font-size-sm);
  margin: 0;
}

/* Responsividade */
@media (max-width: 768px) {
  .hero {
    grid-template-columns: 1fr;
    gap: var(--spacing-8);
    text-align: center;
  }
  
  .hero-content {
    max-width: none;
  }
  
  .hero-title {
    font-size: var(--font-size-3xl);
  }
  
  .hero-features {
    justify-content: center;
  }
  
  .hero-actions {
    justify-content: center;
    flex-direction: column;
    align-items: center;
  }
  
  .tech-grid {
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: var(--spacing-4);
  }
}

@media (max-width: 480px) {
  .hero {
    margin-bottom: var(--spacing-8);
    padding: var(--spacing-4) 0;
  }
  
  .hero-title {
    font-size: var(--font-size-2xl);
  }
  
  .hero-subtitle {
    font-size: var(--font-size-base);
  }
  
  .hero-features {
    flex-direction: column;
    gap: var(--spacing-4);
  }
  
  .tech-grid {
    grid-template-columns: 1fr;
  }
  
  .tech-card {
    padding: var(--spacing-4);
  }
}
</style>




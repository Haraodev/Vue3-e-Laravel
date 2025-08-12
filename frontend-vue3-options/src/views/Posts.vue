<template>
  <section class="posts-page">
    <div class="page-header">
      <h1 class="page-title">Gerenciar Posts</h1>
      <p class="page-subtitle">Crie, edite e gerencie seus posts de forma simples e eficiente.</p>
    </div>

    <!-- Formulário de criação -->
    <div class="create-post-section">
      <h2 class="section-title">Criar Novo Post</h2>
      <form @submit.prevent="createPost" class="create-form">
        <div class="form-group">
          <label for="title" class="form-label">Título</label>
          <input 
            id="title"
            v-model="form.title" 
            type="text"
            placeholder="Digite o título do post..." 
            required 
            class="form-input"
          />
        </div>
        <div class="form-group">
          <label for="body" class="form-label">Conteúdo</label>
          <textarea 
            id="body"
            v-model="form.body" 
            placeholder="Digite o conteúdo do post..." 
            required 
            rows="4"
            class="form-textarea"
          ></textarea>
        </div>
        <div class="form-actions">
          <button type="submit" class="btn btn-primary" :disabled="loading">
            <span v-if="loading" class="loading-spinner"></span>
            {{ loading ? 'Criando...' : 'Criar Post' }}
          </button>
          <button type="button" @click="clearForm" class="btn btn-secondary">
            Limpar
          </button>
        </div>
      </form>
    </div>

    <!-- Lista de posts -->
    <div class="posts-section">
      <div class="section-header">
        <h2 class="section-title">Posts Existentes</h2>
        <div class="posts-count">
          <span class="count-badge">{{ posts.length }} post{{ posts.length !== 1 ? 's' : '' }}</span>
        </div>
      </div>

      <!-- Loading state -->
      <div v-if="loading" class="loading-state">
        <div class="loading-spinner large"></div>
        <p>Carregando posts...</p>
      </div>

      <!-- Error message -->
      <div v-else-if="errorMessage" class="error-message">
        <span class="error-icon">⚠️</span>
        <p>{{ errorMessage }}</p>
        <button @click="loadPosts" class="btn btn-secondary btn-sm">
          Tentar Novamente
        </button>
      </div>

      <!-- Posts list -->
      <div v-else-if="posts.length" class="posts-grid">
        <article 
          v-for="post in posts" 
          :key="post.id" 
          class="post-card"
          :class="{ 'editing': editingPost?.id === post.id }"
        >
          <!-- Modo de edição -->
          <div v-if="editingPost?.id === post.id" class="edit-mode">
            <h3 class="edit-title">Editando Post</h3>
            <div class="edit-form">
              <div class="form-group">
                <label class="form-label">Título</label>
                <input 
                  v-model="editingPost.title" 
                  type="text"
                  placeholder="Título do post" 
                  required 
                  class="form-input"
                />
              </div>
              <div class="form-group">
                <label class="form-label">Conteúdo</label>
                <textarea 
                  v-model="editingPost.body" 
                  placeholder="Conteúdo do post" 
                  required 
                  rows="3"
                  class="form-textarea"
                ></textarea>
              </div>
              <div class="edit-actions">
                <button @click="saveEdit" type="button" class="btn btn-success">
                  <span class="btn-icon">✓</span>
                  Salvar
                </button>
                <button @click="cancelEdit" type="button" class="btn btn-secondary">
                  Cancelar
                </button>
              </div>
            </div>
          </div>

          <!-- Modo de visualização -->
          <div v-else class="post-content">
            <div class="post-header">
              <h3 class="post-title">{{ post.title }}</h3>
              <div class="post-meta">
                <span class="post-id">#{{ post.id }}</span>
                <span class="post-date">{{ formatDate(post.created_at) }}</span>
              </div>
            </div>
            <p class="post-body">{{ post.body }}</p>
            <div class="post-actions">
              <button @click="startEdit(post)" class="btn btn-primary btn-sm">
                <span class="btn-icon">✏️</span>
                Editar
              </button>
              <button @click="deletePost(post.id)" class="btn btn-danger btn-sm">
                <span class="btn-icon">🗑️</span>
                Excluir
              </button>
            </div>
          </div>
        </article>
      </div>

      <!-- Empty state -->
      <div v-else class="empty-state">
        <div class="empty-icon">📝</div>
        <h3>Nenhum post encontrado</h3>
        <p>Crie seu primeiro post usando o formulário acima!</p>
      </div>
    </div>
  </section>
</template>

<script>
import api from '../services/api'

export default {
  name: 'Posts',
  data() {
    return {
      posts: [],
      form: { title: '', body: '' },
      editingPost: null,
      loading: false,
      errorMessage: ''
    }
  },
  methods: {
    async loadPosts() {
      this.loading = true
      this.errorMessage = ''
      try {
        const { data } = await api.get('/posts')
        this.posts = data
      } catch (error) {
        this.errorMessage = 'Falha ao carregar posts. Verifique sua conexão e tente novamente.'
        console.error('Erro ao carregar posts:', error)
      } finally {
        this.loading = false
      }
    },
    async createPost() {
      if (!this.form.title.trim() || !this.form.body.trim()) return
      
      this.loading = true
      try {
        const { data } = await api.post('/posts', this.form)
        this.posts.unshift(data)
        this.clearForm()
        this.showSuccessMessage('Post criado com sucesso!')
      } catch (error) {
        this.errorMessage = 'Falha ao criar post. Tente novamente.'
        console.error('Erro ao criar post:', error)
      } finally {
        this.loading = false
      }
    },
    async deletePost(id) {
      if (!confirm('Tem certeza que deseja excluir este post?')) return
      
      try {
        await api.delete(`/posts/${id}`)
        this.posts = this.posts.filter(p => p.id !== id)
        this.showSuccessMessage('Post excluído com sucesso!')
      } catch (error) {
        this.errorMessage = 'Falha ao excluir post. Tente novamente.'
        console.error('Erro ao excluir post:', error)
      }
    },
    startEdit(post) {
      this.editingPost = { ...post }
    },
    cancelEdit() {
      this.editingPost = null
    },
    async saveEdit() {
      if (!this.editingPost?.title?.trim() || !this.editingPost?.body?.trim()) return
      
      try {
        const { data } = await api.put(`/posts/${this.editingPost.id}`, {
          title: this.editingPost.title,
          body: this.editingPost.body
        })
        
        const index = this.posts.findIndex(p => p.id === this.editingPost.id)
        if (index !== -1) {
          this.posts[index] = data
        }
        
        this.editingPost = null
        this.showSuccessMessage('Post atualizado com sucesso!')
      } catch (error) {
        this.errorMessage = 'Falha ao atualizar post. Tente novamente.'
        console.error('Erro ao atualizar post:', error)
      }
    },
    clearForm() {
      this.form.title = ''
      this.form.body = ''
    },
    formatDate(dateString) {
      if (!dateString) return 'Data não disponível'
      return new Date(dateString).toLocaleDateString('pt-BR', {
        day: '2-digit',
        month: '2-digit',
        year: 'numeric',
        hour: '2-digit',
        minute: '2-digit'
      })
    },
    showSuccessMessage(message) {
      // Implementar toast notification se desejar
      console.log(message)
    }
  },
  mounted() {
    this.loadPosts()
  }
}
</script>

<style scoped>
.posts-page {
  animation: fadeIn 0.6s ease-out;
}

.page-header {
  text-align: center;
  margin-bottom: var(--spacing-12);
}

.page-title {
  font-size: var(--font-size-4xl);
  font-weight: 800;
  color: var(--gray-900);
  margin-bottom: var(--spacing-4);
}

.page-subtitle {
  font-size: var(--font-size-lg);
  color: var(--gray-600);
  max-width: 600px;
  margin: 0 auto;
}

/* Seção de criação */
.create-post-section {
  background: var(--white);
  border-radius: var(--border-radius-xl);
  padding: var(--spacing-8);
  margin-bottom: var(--spacing-12);
  box-shadow: var(--shadow);
  border: 1px solid var(--gray-200);
}

.section-title {
  font-size: var(--font-size-2xl);
  color: var(--gray-900);
  margin-bottom: var(--spacing-6);
  font-weight: 700;
}

.create-form {
  display: grid;
  gap: var(--spacing-6);
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-2);
}

.form-label {
  font-weight: 600;
  color: var(--gray-700);
  font-size: var(--font-size-sm);
}

.form-input, .form-textarea {
  border: 2px solid var(--gray-200);
  transition: all var(--transition-fast);
}

.form-input:focus, .form-textarea:focus {
  border-color: var(--primary-color);
  box-shadow: 0 0 0 3px rgb(59 130 246 / 0.1);
}

.form-textarea {
  resize: vertical;
  min-height: 100px;
}

.form-actions {
  display: flex;
  gap: var(--spacing-4);
  align-items: center;
}

/* Seção de posts */
.posts-section {
  margin-top: var(--spacing-12);
}

.section-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: var(--spacing-8);
}

.posts-count {
  display: flex;
  align-items: center;
}

.count-badge {
  background: var(--primary-color);
  color: var(--white);
  padding: var(--spacing-2) var(--spacing-4);
  border-radius: var(--border-radius-2xl);
  font-size: var(--font-size-sm);
  font-weight: 600;
}

/* Grid de posts */
.posts-grid {
  display: grid;
  gap: var(--spacing-6);
}

.post-card {
  background: var(--white);
  border-radius: var(--border-radius-lg);
  padding: var(--spacing-6);
  box-shadow: var(--shadow);
  border: 2px solid var(--gray-200);
  transition: all var(--transition-normal);
  position: relative;
}

.post-card:hover {
  transform: translateY(-2px);
  box-shadow: var(--shadow-lg);
  border-color: var(--gray-300);
}

.post-card.editing {
  border-color: var(--primary-color);
  box-shadow: 0 0 0 3px rgb(59 130 246 / 0.1);
}

.post-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: var(--spacing-4);
}

.post-title {
  font-size: var(--font-size-xl);
  color: var(--gray-900);
  font-weight: 700;
  margin: 0;
  flex: 1;
  margin-right: var(--spacing-4);
}

.post-meta {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  gap: var(--spacing-1);
}

.post-id {
  background: var(--gray-100);
  color: var(--gray-600);
  padding: var(--spacing-1) var(--spacing-2);
  border-radius: var(--border-radius-sm);
  font-size: var(--font-size-xs);
  font-weight: 600;
}

.post-date {
  color: var(--gray-500);
  font-size: var(--font-size-xs);
}

.post-body {
  color: var(--gray-600);
  line-height: 1.6;
  margin-bottom: var(--spacing-6);
  margin: 0 0 var(--spacing-6) 0;
}

.post-actions {
  display: flex;
  gap: var(--spacing-3);
}

.btn-sm {
  padding: var(--spacing-2) var(--spacing-3);
  font-size: var(--font-size-sm);
  min-height: 2rem;
}

.btn-icon {
  margin-right: var(--spacing-1);
}

/* Modo de edição */
.edit-mode {
  padding: var(--spacing-4);
  background: var(--gray-50);
  border-radius: var(--border-radius);
  border: 1px solid var(--gray-200);
}

.edit-title {
  font-size: var(--font-size-lg);
  color: var(--gray-700);
  margin-bottom: var(--spacing-4);
  font-weight: 600;
}

.edit-form {
  display: grid;
  gap: var(--spacing-4);
}

.edit-actions {
  display: flex;
  gap: var(--spacing-3);
  justify-content: flex-end;
}

/* Estados especiais */
.loading-state {
  text-align: center;
  padding: var(--spacing-12);
  color: var(--gray-600);
}

.loading-spinner {
  width: 24px;
  height: 24px;
  border: 2px solid var(--gray-300);
  border-top: 2px solid var(--primary-color);
  border-radius: 50%;
  animation: spin 1s linear infinite;
  margin: 0 auto var(--spacing-4);
}

.loading-spinner.large {
  width: 48px;
  height: 48px;
  border-width: 3px;
}

.error-message {
  background: #fef2f2;
  border: 1px solid #fecaca;
  border-radius: var(--border-radius);
  padding: var(--spacing-6);
  text-align: center;
  color: #dc2626;
}

.error-icon {
  font-size: var(--font-size-2xl);
  display: block;
  margin-bottom: var(--spacing-3);
}

.error-message p {
  margin-bottom: var(--spacing-4);
  color: #dc2626;
}

.empty-state {
  text-align: center;
  padding: var(--spacing-12);
  color: var(--gray-500);
}

.empty-icon {
  font-size: var(--font-size-4xl);
  margin-bottom: var(--spacing-4);
  opacity: 0.5;
}

.empty-state h3 {
  color: var(--gray-600);
  margin-bottom: var(--spacing-2);
}

.empty-state p {
  color: var(--gray-500);
  margin: 0;
}

/* Responsividade */
@media (max-width: 768px) {
  .page-title {
    font-size: var(--font-size-3xl);
  }
  
  .create-post-section {
    padding: var(--spacing-6);
  }
  
  .section-header {
    flex-direction: column;
    gap: var(--spacing-4);
    align-items: flex-start;
  }
  
  .form-actions {
    flex-direction: column;
    align-items: stretch;
  }
  
  .post-header {
    flex-direction: column;
    gap: var(--spacing-3);
  }
  
  .post-meta {
    align-items: flex-start;
  }
  
  .edit-actions {
    flex-direction: column;
  }
}

@media (max-width: 480px) {
  .create-post-section {
    padding: var(--spacing-4);
  }
  
  .post-card {
    padding: var(--spacing-4);
  }
  
  .post-actions {
    flex-direction: column;
  }
  
  .btn-sm {
    width: 100%;
    justify-content: center;
  }
}
</style>



# 🎨 Frontend Vue 3 - Aplicação Moderna

Frontend da aplicação Vue3 + Laravel construído com **Vue 3 (Options API)**, apresentando um design moderno e responsivo.

## 🚀 Início Rápido

### Pré-requisitos
- **Node.js** >= 16.0
- **npm** >= 8.0

### Instalação e Execução

```bash
# Instalar dependências
npm install

# Executar em modo de desenvolvimento
npm run dev

# Build para produção
npm run build

# Preview do build de produção
npm run preview
```

## 📱 Funcionalidades

### 🏠 Página Home
- **Hero Section**: Apresentação moderna com gradientes
- **Tech Stack**: Grid de tecnologias utilizadas
- **Call-to-Action**: Botões para navegação
- **Design Responsivo**: Adaptação para todos os dispositivos

### 📝 Página Posts
- **CRUD Completo**: Criar, Ler, Atualizar, Deletar posts
- **Formulários Modernos**: Inputs com validação e estados visuais
- **Cards Interativos**: Hover effects e animações
- **Estados de Loading**: Feedback visual durante operações
- **Tratamento de Erros**: Mensagens amigáveis para o usuário

## 🎨 Sistema de Design

### Variáveis CSS
```css
/* Cores */
--primary-color: #3b82f6
--success-color: #10b981
--warning-color: #f59e0b
--danger-color: #ef4444

/* Espaçamento */
--spacing-4: 1rem
--spacing-6: 1.5rem
--spacing-8: 2rem

/* Tipografia */
--font-size-lg: 1.125rem
--font-size-xl: 1.25rem
--font-size-2xl: 1.5rem
```

### Componentes Disponíveis
- **Botões**: `.btn`, `.btn-primary`, `.btn-success`, `.btn-danger`
- **Cards**: `.card` com hover effects
- **Formulários**: `.form-input`, `.form-textarea`, `.form-label`
- **Utilitários**: `.flex`, `.grid`, `.text-center`, etc.

## 📁 Estrutura do Projeto

```
src/
├── App.vue                 # Componente principal
├── main.js                 # Ponto de entrada
├── router/
│   └── index.js           # Configuração de rotas
├── services/
│   └── api.js             # Configuração do Axios
├── views/
│   ├── Home.vue           # Página inicial
│   └── Posts.vue          # Gerenciamento de posts
├── style.css              # Estilos base e variáveis
└── components.css         # Componentes reutilizáveis
```

## 🔧 Configuração

### API Backend
Configure a URL da API no arquivo `src/services/api.js`:

```javascript
import axios from 'axios'

const api = axios.create({
  baseURL: 'http://localhost:8000/api', // URL do seu backend
  headers: {
    'Content-Type': 'application/json',
    'Accept': 'application/json'
  }
})

export default api
```

### Variáveis de Ambiente
Crie um arquivo `.env` na raiz do projeto:

```env
VITE_API_URL=http://localhost:8000/api
```

## 🎯 Tecnologias Utilizadas

- **Vue 3**: Framework JavaScript progressivo
- **Options API**: Sintaxe tradicional do Vue
- **Vue Router**: Roteamento de páginas
- **Axios**: Cliente HTTP para requisições
- **Vite**: Build tool rápida e moderna
- **CSS Custom Properties**: Sistema de design moderno

## 📱 Responsividade

A aplicação é totalmente responsiva com breakpoints:

- **Mobile**: < 480px
- **Tablet**: 480px - 768px
- **Desktop**: > 768px

## 🎭 Animações

- **Fade In**: Entrada suave de elementos
- **Hover Effects**: Micro-interações nos botões e cards
- **Loading Spinners**: Indicadores de carregamento
- **Transições**: Mudanças suaves entre estados

## 🛠️ Comandos de Desenvolvimento

```bash
# Instalar dependência
npm install nome-do-pacote

# Executar lint
npm run lint

# Build para produção
npm run build

# Preview build
npm run preview

# Limpar cache
npm run clean
```

## 🔍 Debugging

### Vue DevTools
Instale a extensão Vue DevTools no seu navegador para debugging avançado.

### Console do Navegador
Use `console.log()` para debugging JavaScript:

```javascript
// Exemplo de debug
console.log('Posts carregados:', this.posts)
```

### Network Tab
Monitore as requisições para a API no DevTools do navegador.

## 🚨 Solução de Problemas

### Erro de CORS
Se encontrar erros de CORS, verifique se o backend está configurado corretamente.

### Porta Já em Uso
```bash
npm run dev -- --port=5174
```

### Erro de Build
```bash
# Limpar cache e node_modules
rm -rf node_modules package-lock.json
npm install
```

## 📚 Recursos Adicionais

- [Documentação Vue 3](https://vuejs.org/guide/)
- [Vue Router](https://router.vuejs.org/)
- [Axios](https://axios-http.com/)
- [Vite](https://vitejs.dev/)

## 🎨 Personalização

### Alterando Cores
Modifique as variáveis CSS em `src/style.css`:

```css
:root {
  --primary-color: #your-color;
  --primary-hover: #your-hover-color;
}
```

### Adicionando Novos Componentes
Crie novos componentes seguindo o padrão estabelecido:

```vue
<template>
  <div class="meu-componente">
    <!-- Conteúdo -->
  </div>
</template>

<script>
export default {
  name: 'MeuComponente'
}
</script>

<style scoped>
.meu-componente {
  /* Use as variáveis CSS existentes */
  background: var(--white);
  padding: var(--spacing-6);
  border-radius: var(--border-radius-lg);
}
</style>
```

## 🤝 Contribuição

1. Mantenha a consistência com o sistema de design
2. Use as variáveis CSS disponíveis
3. Teste em diferentes dispositivos
4. Documente novos componentes

---

**Desenvolvido com ❤️ usando Vue 3**

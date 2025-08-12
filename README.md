#  Vue3 + Laravel

## Clonar repositório

### 1. Backend Laravel (Terminal 1)

```bash
# Navegar para o backend
cd backend-laravel

# Instalar dependências
composer install

# Configurar ambiente
cp .env.example .env
php artisan key:generate

# Configurar banco de dados no .env
#DB_CONNECTION=pgsql
#DB_HOST=127.0.0.1
#DB_PORT=5432
#DB_DATABASE=laravel
#DB_USERNAME=postgres
#DB_PASSWORD=

# Executar migrações
php artisan migrate

# Iniciar servidor
php artisan serve
```

**Backend rodando em:** http://localhost:8000

### 2. Frontend Vue 3 (Terminal 2)

```bash
# Navegar para o frontend
cd frontend-vue3-options

# Instalar dependências
npm install

# Iniciar servidor
npm run dev
```

**Frontend rodando em:** http://localhost:5173

## 🌐 Acessar a Aplicação

1. Abra o navegador
2. Acesse: **http://localhost:5173**
3. Navegue entre as páginas Home e Posts

## 🚨 Problemas Comuns

### Erro de CORS
- Verifique se o backend está rodando em http://localhost:8000
- Confirme se o frontend está rodando em http://localhost:5173

### Erro de Banco de Dados
- Verifique se o MySQL está rodando
- Confirme as credenciais no arquivo `.env`
- Teste: `php artisan tinker`

### Porta Já em Uso
- Backend: `php artisan serve --port=8001`
- Frontend: `npm run dev -- --port=5174`

## 📱 Funcionalidades para Testar

### Página Home
- Visualizar landing page moderna
- Ver seção de tecnologias
- Testar responsividade

### Página Posts
- Criar novo post
- Editar post existente
- Excluir post
- Ver estados de loading

## 🔧 Comandos Úteis

```bash
# Backend
php artisan migrate:fresh    # Resetar banco
php artisan route:list      # Ver rotas
php artisan tinker          # Console interativo

# Frontend
npm run build              # Build para produção
npm run preview            # Preview do build
```

---

**✅ Aplicação funcionando! Aproveite! 🚀**

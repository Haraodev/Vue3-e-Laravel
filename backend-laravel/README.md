# 🚀 Backend Laravel - API REST

Backend da aplicação Vue3 + Laravel construído com **Laravel 10**, fornecendo uma API REST robusta e escalável.

## 🚀 Início Rápido

### Pré-requisitos
- **PHP** >= 8.1
- **Composer** >= 2.0
- **MySQL** >= 8.0 ou **PostgreSQL** >= 13.0

### Instalação e Configuração

```bash
# Instalar dependências PHP
composer install

# Copiar arquivo de configuração
cp .env.example .env

# Gerar chave da aplicação
php artisan key:generate

# Configurar banco de dados no .env
# DB_CONNECTION=mysql
# DB_HOST=127.0.0.1
# DB_PORT=3306
# DB_DATABASE=vue3_laravel_db
# DB_USERNAME=seu_usuario
# DB_PASSWORD=sua_senha

# Executar migrações
php artisan migrate

# (Opcional) Executar seeders
php artisan db:seed

# Iniciar servidor
php artisan serve
```

O backend estará disponível em: **http://localhost:8000**

## 📡 Endpoints da API

### Posts

| Método | Endpoint | Descrição |
|--------|----------|-----------|
| `GET` | `/api/posts` | Listar todos os posts |
| `POST` | `/api/posts` | Criar novo post |
| `GET` | `/api/posts/{id}` | Buscar post específico |
| `PUT` | `/api/posts/{id}` | Atualizar post |
| `DELETE` | `/api/posts/{id}` | Excluir post |

### Exemplos de Uso

#### Listar Posts
```bash
curl -X GET http://localhost:8000/api/posts
```

#### Criar Post
```bash
curl -X POST http://localhost:8000/api/posts \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Meu Post",
    "body": "Conteúdo do post"
  }'
```

#### Atualizar Post
```bash
curl -X PUT http://localhost:8000/api/posts/1 \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Post Atualizado",
    "body": "Novo conteúdo"
  }'
```

#### Excluir Post
```bash
curl -X DELETE http://localhost:8000/api/posts/1
```

## 📁 Estrutura do Projeto

```
app/
├── Http/Controllers/Api/
│   └── PostController.php    # Controller da API
├── Models/
│   └── Post.php             # Modelo Post
└── Providers/
    └── AppServiceProvider.php

database/
├── migrations/
│   └── 2025_08_07_193904_create_posts_table.php
└── seeders/
    └── DatabaseSeeder.php

routes/
└── api.php                  # Rotas da API
```

## 🗄️ Banco de Dados

### Migração Posts
```php
Schema::create('posts', function (Blueprint $table) {
    $table->id();
    $table->string('title');
    $table->text('body');
    $table->timestamps();
});
```

### Modelo Post
```php
class Post extends Model
{
    protected $fillable = ['title', 'body'];
}
```

## 🔧 Configuração

### Arquivo .env
```env
APP_NAME="Vue3 + Laravel"
APP_ENV=local
APP_KEY=base64:sua_chave_aqui
APP_DEBUG=true
APP_URL=http://localhost:8000

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=vue3_laravel_db
DB_USERNAME=seu_usuario
DB_PASSWORD=sua_senha

CORS_ALLOWED_ORIGINS=http://localhost:5173
```

### CORS Configuration
```php
// config/cors.php
return [
    'paths' => ['api/*'],
    'allowed_methods' => ['*'],
    'allowed_origins' => ['http://localhost:5173'],
    'allowed_headers' => ['*'],
    'exposed_headers' => [],
    'max_age' => 0,
    'supports_credentials' => false,
];
```

## 🛠️ Comandos Artisan

```bash
# Criar novo controller
php artisan make:controller Api/NovoController

# Criar nova migração
php artisan make:migration create_nova_tabela

# Criar novo modelo
php artisan make:model NovoModelo

# Executar migrações
php artisan migrate

# Reverter migrações
php artisan migrate:rollback

# Ver rotas
php artisan route:list

# Limpar cache
php artisan cache:clear
php artisan config:clear
php artisan route:clear

# Tinker (console interativo)
php artisan tinker
```

## 🔍 Debugging

### Logs
- Arquivo de logs: `storage/logs/laravel.log`
- Debug mode: `APP_DEBUG=true` no `.env`

### Tinker
```bash
php artisan tinker

# Exemplo de uso
>>> Post::all();
>>> Post::create(['title' => 'Teste', 'body' => 'Conteúdo']);
```

### Validação de Dados
```php
// PostController.php
public function store(Request $request)
{
    $validated = $request->validate([
        'title' => 'required|string|max:255',
        'body' => 'required|string'
    ]);
    
    return Post::create($validated);
}
```

## 🚨 Solução de Problemas

### Erro de CORS
Verifique se o CORS está configurado corretamente em `config/cors.php`.

### Erro de Conexão com Banco
```bash
# Testar conexão
php artisan tinker
>>> DB::connection()->getPdo();

# Verificar configurações
php artisan config:cache
```

### Erro de Permissões
```bash
# Dar permissões para storage
chmod -R 775 storage bootstrap/cache
```

### Porta Já em Uso
```bash
php artisan serve --port=8001
```

## 📊 Respostas da API

### Sucesso
```json
{
  "id": 1,
  "title": "Meu Post",
  "body": "Conteúdo do post",
  "created_at": "2025-01-15T10:30:00.000000Z",
  "updated_at": "2025-01-15T10:30:00.000000Z"
}
```

### Erro
```json
{
  "message": "The given data was invalid.",
  "errors": {
    "title": ["The title field is required."]
  }
}
```

## 🔒 Segurança

### Validação
- Validação de entrada em todos os endpoints
- Sanitização de dados
- Proteção contra SQL injection

### CORS
- Configuração específica para origens permitidas
- Headers de segurança configurados

## 📚 Recursos Adicionais

- [Documentação Laravel](https://laravel.com/docs)
- [Eloquent ORM](https://laravel.com/docs/eloquent)
- [API Resources](https://laravel.com/docs/api-resources)
- [Validation](https://laravel.com/docs/validation)

## 🧪 Testes

```bash
# Executar testes
php artisan test

# Criar teste
php artisan make:test PostTest
```

### Exemplo de Teste
```php
public function test_can_create_post()
{
    $response = $this->postJson('/api/posts', [
        'title' => 'Test Post',
        'body' => 'Test content'
    ]);

    $response->assertStatus(201)
             ->assertJsonStructure(['id', 'title', 'body']);
}
```

## 🚀 Deploy

### Produção
```bash
# Otimizar para produção
composer install --optimize-autoloader --no-dev

# Cache de configurações
php artisan config:cache
php artisan route:cache
php artisan view:cache

# Configurar APP_ENV=production no .env
```

---

**Desenvolvido com ❤️ usando Laravel**

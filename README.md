<h1 align="center">🚀 Vue + Laravel CRUD</h1>

<p align="center">
  <b>Um projeto fullstack simples com Laravel e Vue.js</b><br>
  CRUD completo (Create, Read, Update, Delete) demonstrando a integração entre back-end e front-end.
</p>

---

<h2 align="center">🧩 Tecnologias Utilizadas

---

| Camada | Tecnologia | Descrição |
|:-------|:------------|:-----------|
| **Back-end** | 🧱 Laravel (PHP) | Framework principal do servidor |
| **Front-end** | ⚡ Vue.js | Interface reativa e modular |
| **Build Tool** | 🔧 Vite | Compilação e hot reload integrados |
| **Banco de Dados** | 🗄️ MySQL / SQLite / outro compatível | Persistência de dados |
| **API** | 🔗 Laravel API padrão | Comunicação com o front-end Vue |

---

<h2 align="left">🧱 Estrutura típica do projeto:

---

- resources/js/ → componentes Vue
- routes/web.php → rotas web Laravel
- routes/api.php → rotas de API

<h2 align="center">⚙️ COMO EXECUTAR O PROJETO</h2>

### 📋 Pré-requisitos

- PHP (versão compatível com o Laravel)
- Composer
- Node.js + npm ou yarn
- Banco de dados configurado

---

## 🪜 Passo a Passo

### 1️⃣ Clonar o repositório
```bash
git clone https://github.com/Luan-5ilva/Vue-Laravel-CRUD.git
cd Vue-Laravel-CRUD
```

### 2️⃣ Instalar dependências do Laravel
```bash
composer install
```

### 3️⃣ Configurar o ambiente
```bash
cp .env.example .env
php artisan key:generate
```

### 4️⃣ Executar as migrações do banco de dados
```bash
php artisan migrate
```

### 5️⃣ Instalar dependências do Vue
```bash
npm install
```

### 6️⃣ Compilar o front-end
```bash
npm run dev
```

### 7️⃣ Iniciar o servidor Laravel
```bash
php artisan serve
```

<h2 align="center">💡 Observações

---

- Certifique-se de que a rota da API usada pelo front-end está corretamente configurada.
- Ideal para estudos sobre integração entre Laravel + Vue com um CRUD funcional.
- Pode ser expandido com autenticação, upload de arquivos, ou componentes adicionais.

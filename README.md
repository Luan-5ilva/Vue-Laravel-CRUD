                                         # Vue-Laravel-CRUD

Este projeto é um **desafio técnico** desenvolvido com as tecnologias Laravel e Vue.js, onde foi criado um sistema CRUD (Create, Read, Update, Delete) simples para demonstração de integração entre back-end em Laravel e front-end em Vue.

---

## Tecnologias utilizadas

- Back-end: Laravel (PHP)  
- Front-end: Vue.js  
- Build tools / bundler: Vite (incluído na estrutura Laravel + Vue)  
- Banco de dados: qualquer compatível com Laravel (MySQL, SQLite, etc)  
- Autenticação/API: utilização padrão do Laravel para rotas e controllers, com consumo via Vue  
- Estrutura de pastas típica:  
  - `resources/js` -> arquivos Vue, componentes, etc  
  - `routes/web.php`, `routes/api.php` para definir rotas do Laravel

---

                                        ## COMO EXECUTAR O PROJETO

### Pré-requisitos
- PHP (versão compatível com Laravel)  
- Composer  
- Node.js e npm ou yarn  
- Banco de dados configurado  

## PASSOS

1. Clone o repositório  
   bash
   git clone https://github.com/Luan-5ilva/Vue-Laravel-CRUD.git
   cd Vue-Laravel-CRUD

2. Instale as dependências do back-end (Laravel)
   bash
   composer install

3. Copie o arquivo de ambiente e configure as variáveis de ambiente (como banco de dados, chave de aplicativo, etc)
   bash
   cp .env.example .env
   php artisan key:generate

4. Execute as migrações do banco de dados
   bash
   php artisan migrate

5. Instale as dependências do front-end (Vue)
   npm install

6. Compile os assets front-end
   npm run dev

7. Inicie o servidor Laravel
   bash
   php artisan serve

   O servidor normalmente estará disponível em http://127.0.0.1:8000.

## OBSERVAÇÕES
   - Certifique-se de que a rota de API usada pelo front-end está corretamente apontada.
     (no arquivo Vue ou configuração de ambiente).
   - Este projeto é ideal para estudar a integração Laravel + Vue de forma simples, com estrutura CRUD básica.

# SER - Sistema de Requisição de Equipamentos

<div align="center">
  <h3>Projeto Final do Curso EFA - CESAE</h3>
  <p><strong>Sistema completo de gestão e requisição de equipamentos</strong></p>
</div>

---

## Índice

- [Sobre o Projeto](#sobre-o-projeto)
- [Funcionalidades](#funcionalidades)
- [Tecnologias Utilizadas](#tecnologias-utilizadas)
- [Pré-requisitos](#pré-requisitos)
- [Instalação](#instalação)
- [Configuração](#configuração)
- [Utilização](#utilização)
- [Estrutura do Projeto](#estrutura-do-projeto)
- [Equipa](#equipa)
- [Notas Técnicas](#notas-técnicas)
- [Licença](#licença)

---

## Sobre o Projeto

O **SER (Sistema de Requisição de Equipamentos)** é uma aplicação web desenvolvida como projeto final do curso EFA da CESAE. O sistema foi projetado para facilitar a gestão e requisição de equipamentos dentro de uma organização educacional.

A aplicação oferece uma solução completa que permite:
- Controlo total sobre o inventário de equipamentos
- Processo estruturado de requisição com múltiplos estados
- Gestão de utilizadores com diferentes níveis de acesso
- Sistema de notificações por email
- Rastreamento completo do histórico de equipamentos

---

## Funcionalidades

### Gestão de Utilizadores
- Sistema de autenticação com login e registo
- Três níveis de acesso:
  - **Administrador**: Acesso completo ao sistema
  - **Técnico**: Gestão de requisições e equipamentos
  - **Utilizador**: Submissão e consulta de requisições
- Painel de gestão de contas para administradores
- Gestão de tipos e funções de utilizadores
- Soft delete para preservação de dados

### Gestão de Equipamentos
- CRUD completo de equipamentos
- Gestão de marcas e modelos
- Sistema de referências para agrupar equipamentos similares
- Controlo de stock em tempo real
- Números de série únicos (opcional)
- Histórico completo de utilização de cada equipamento
- Importação em massa via ficheiro Excel
- Imagens de equipamentos

### Sistema de Requisições
- **8 Estados de Requisição**:
  1. Temporário - Rascunho não guardado
  2. Submetido - Pendente de aprovação
  3. Aguarda Levantamento - Aprovado, aguarda recolha
  4. Requisitado - Equipamento em utilização
  5. Expirado - Requisição expirada
  6. Cancelado - Cancelado por utilizador ou técnico
  7. Rejeitado - Rejeitado por técnico
  8. Devolvido - Equipamento devolvido

- Múltiplos equipamentos por requisição
- Duração configurável de requisições
- Possibilidade de extensão de requisições
- Filtros avançados por estado
- Associação a curso, turma, UFCD e professor
- Técnicos podem editar requisições pendentes
- Utilizadores podem cancelar requisições pendentes
- Registo de entrega e devolução de equipamentos

### Sistema de Notificações
- Notificações por email para:
  - Aprovação/rejeição de requisições
  - Requisições expiradas
  - Stock reduzido
  - Entregas e devoluções
- Alertas configuráveis via painel de administração
- SweetAlert para feedback visual em tempo real

### Configurações da Aplicação
- Painel de configurações parametrizáveis:
  - Email para alertas
  - Percentagem de stock baixo
  - Dias padrão de requisição
  - Minutos de expiração para requisições temporárias
  - Chave API para integrações externas
- Cada parâmetro pode ser ativado/desativado individualmente

---

## Tecnologias Utilizadas

### Backend
- **Framework**: Laravel 7.x
- **Linguagem**: PHP 7.4+
- **Base de Dados**: MySQL 5.7+
- **Autenticação**: Laravel Authentication + Sistema de Permissões
- **Email**: SMTP (configurável)

### Frontend
- **Template Admin**: AdminLTE 3.8
- **CSS Framework**: Bootstrap 4.0
- **JavaScript**: Vue.js 2.5.17 + jQuery 3.2
- **Build Tool**: Laravel Mix + Webpack

### Bibliotecas Principais
- **jeroennoten/laravel-adminlte**: Interface administrativa
- **maatwebsite/excel**: Importação/exportação Excel
- **realrashid/sweet-alert**: Alertas e notificações
- **guzzlehttp/guzzle**: Cliente HTTP

---

## Pré-requisitos

Antes de começar, certifique-se de ter instalado:

- PHP >= 7.4
- Composer
- MySQL >= 5.7
- Node.js >= 12.x
- npm ou yarn

---

## Instalação

### 1. Clonar o repositório

```bash
git clone https://github.com/seu-usuario/Projeto-Final---EFA-Cesae_rev.git
cd Projeto-Final---EFA-Cesae_rev
```

### 2. Instalar dependências PHP

```bash
composer install
```

### 3. Instalar dependências Node.js

```bash
npm install
```

### 4. Configurar ambiente

```bash
cp .env.example .env
php artisan key:generate
```

### 5. Configurar base de dados

Edite o ficheiro `.env` com as suas credenciais de base de dados:

```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=nome_da_base_dados
DB_USERNAME=seu_usuario
DB_PASSWORD=sua_password
```

### 6. Executar migrações e seeders

```bash
php artisan migrate
php artisan db:seed
```

### 7. Compilar assets

```bash
npm run dev
```

Para ambiente de produção:

```bash
npm run prod
```

### 8. Iniciar servidor

```bash
php artisan serve
```

A aplicação estará disponível em `http://localhost:8000`

---

## Configuração

### Configuração de Email

Edite o ficheiro `.env` para configurar o envio de emails:

```env
MAIL_MAILER=smtp
MAIL_HOST=smtp.mailtrap.io
MAIL_PORT=2525
MAIL_USERNAME=seu_username
MAIL_PASSWORD=sua_password
MAIL_ENCRYPTION=tls
MAIL_FROM_ADDRESS=noreply@seudominio.com
MAIL_FROM_NAME="${APP_NAME}"
```

### Timezone

O sistema está configurado para o fuso horário de Portugal:

```env
APP_TIMEZONE=Europe/Lisbon
```

### Credenciais Padrão

Após executar os seeders, utilize as seguintes credenciais:

**Administrador:**
- Email: (verificar no seeder)
- Password: (verificar no seeder)

---

## Utilização

### Acesso Administrador
- Gestão completa de utilizadores
- Configuração de parâmetros da aplicação
- Acesso a todos os relatórios e estatísticas
- Gestão de tipos e funções de utilizadores

### Acesso Técnico
- Aprovar/rejeitar requisições
- Registar entregas e devoluções
- Editar requisições pendentes
- Gestão de equipamentos e stock
- Acesso a filtros avançados de requisições

### Acesso Utilizador
- Submeter novas requisições
- Consultar requisições próprias
- Cancelar requisições pendentes
- Visualizar stock disponível
- Solicitar extensão de requisições

---

## Estrutura do Projeto

```
pgre/
├── app/
│   ├── Http/
│   │   ├── Controllers/        # Controladores da aplicação
│   │   ├── Middleware/         # Middlewares personalizados
│   │   └── Requests/           # Validação de formulários
│   ├── Mail/                   # Classes de envio de email
│   ├── Models/                 # Modelos Eloquent
│   └── Console/                # Comandos Artisan
├── config/                     # Ficheiros de configuração
├── database/
│   ├── migrations/             # Migrações da base de dados
│   └── seeds/                  # Seeders de dados iniciais
├── public/                     # Ficheiros públicos (CSS, JS, imagens)
├── resources/
│   ├── views/                  # Templates Blade
│   ├── js/                     # Ficheiros JavaScript
│   └── sass/                   # Ficheiros SASS/CSS
├── routes/
│   ├── web.php                 # Rotas web
│   └── api.php                 # Rotas API
├── storage/                    # Ficheiros gerados e uploads
└── tests/                      # Testes automatizados
```

---

## Equipa

**Equipa S - CESAE**

- **Sérgio Fernandes**
- **Paulo Pinto**
- **Deivid Vieira**

---

## Notas Técnicas

### Chamar parâmetros da AppConfig nos templates Blade

```php
{{ App\App_config::GetAppConfig() }}
```

### Incluir alertas nas páginas

Na linha seguinte a `@section('content')`:

```php
@include('sweetalert::alert')
```

### Adicionar traduções nas DataTables

```php
$config['language'] = ['url' => 'https://cdn.datatables.net/plug-ins/1.13.1/i18n/pt-PT.json'];
```

No componente da tabela:
```blade
:config="$config"
```

### Comandos Úteis

```bash
# Limpar cache
php artisan cache:clear
php artisan config:clear
php artisan view:clear

# Executar testes
php artisan test

# Modo watch para desenvolvimento
npm run watch

# Gerar dados de teste
php artisan db:seed
```

---

## Requisitos do Projeto

Este projeto cumpre todos os requisitos estabelecidos:

- Portal com página de login e registo
- Backoffice de gestão de utilizadores, equipamentos e requisições
- 3 tipos de utilizadores (Administrador, Técnico e Utilizador)
- Conta de Administrador com acessos totais
- Sistema completo de requisições com workflow de aprovação
- Painel de gestão de utilizadores para administrador
- Gestão avançada de requisições com filtros de estado
- Controlo de stock e disponibilidade
- Sistema de notificações por email
- Parâmetros configuráveis (email de alertas, stock baixo, etc.)
- Importação em massa de equipamentos via Excel
- Layout com cores do CESAE
- Histórico completo de equipamentos
- Sistema de extensão de requisições
- Soft deletes para integridade de dados

---

## Licença

Este projeto foi desenvolvido como trabalho académico para o curso EFA da CESAE.

---

<div align="center">
  <p>Desenvolvido com dedicação pela Equipa S</p>
  <p>CESAE - 2024</p>
</div>




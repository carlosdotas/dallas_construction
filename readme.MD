# 🏗️ Dallas Construction – Orçamentador de Galpões

Sistema Full-Stack com aplicativo móvel (React Native) e backend (Node.js) para automação e gerenciamento completo de orçamentos de galpões metálicos.

## 🚀 Visão Geral

O Orçamentador Dallas é uma ferramenta interna desenvolvida para otimizar e agilizar o fluxo de trabalho da equipe comercial. Ele permite:

*   Criar, visualizar e duplicar orçamentos de forma rápida e intuitiva.
*   Gerar PDFs profissionais automaticamente a partir dos dados inseridos.
*   Acessar um histórico completo de orçamentos no celular (Android & iOS).
*   Garantir a segurança com um sistema de autenticação robusto.

**Link para o ambiente de demonstração:** [dallas-construction.run.app](https://dallas-construction-or-amentador-de-galp-es-960155395693.us-west1.run.app)

## 🛠️ Tecnologias Utilizadas

| Camada | Tecnologia |
| :--- | :--- |
| **Mobile (Frontend)** | React Native (Expo), Expo Router, TypeScript, NativeWind, React Query |
| **Backend (API)** | Node.js, Express, TypeScript, Prisma ORM, Zod, JWT |
| **Banco de Dados** | MySQL 8 |
| **Geração de PDF** | Puppeteer (Renderização de HTML no servidor) |
| **Contêineres & CI/CD** | Docker, Docker Compose, GitHub Actions, EAS Build |

## 📁 Estrutura do Projeto

O projeto utiliza um **monorepo** gerenciado com `pnpm` para centralizar o código do frontend e backend.

```
monorepo/
├── mobile/                # React Native App (Expo)
│   ├── app/               # Rotas (Expo Router)
│   ├── components/
│   ├── hooks/
│   └── ...
├── api/                   # Backend API em Node.js
│   ├── src/
│   │   ├── routes/
│   │   ├── controllers/
│   │   ├── services/      # Lógica de cálculo e PDF
│   │   └── prisma/        # Schema do DB
│   └── ...
├── docker-compose.yml     # Orquestração dos contêineres
└── README.md
```

## ✨ Funcionalidades

#### 📝 Gestão Completa de Orçamentos
CRUD completo (Criar, Ler, Atualizar, Deletar) para orçamentos. Inclui uma funcionalidade de "duplicar" para agilizar a criação de cotações similares.

#### 📄 Geração de PDF no Backend
Um endpoint dedicado recebe o ID de um orçamento, renderiza um template HTML com os dados e o converte para um PDF otimizado, pronto para download e compartilhamento.

#### 📱 Dashboard Móvel Intuitivo
A tela principal do app exibe uma lista paginada de todos os orçamentos, com filtros por cliente ou status e ações rápidas (excluir, duplicar) acessíveis por gestos.

#### 🔐 Autenticação e Segurança
Fluxo de login com JWT para proteger as rotas da API. No app mobile, o token é armazenado de forma segura usando o `SecureStore` do Expo.

## 🖥️ Telas do Sistema

1.  **Tela de Login**
    *   Campos para email e senha.
    *   Autenticação segura via API e armazenamento do token de sessão.

2.  **Dashboard (Lista de Orçamentos)**
    *   Listagem de todos os orçamentos com informações essenciais.
    *   Filtros e busca.
    *   Botão de acesso rápido para criar um novo orçamento.

3.  **Formulário de Criação/Edição**
    *   Formulário multi-etapas para preenchimento de dados do cliente e especificações do galpão.
    *   Validação em tempo real e máscaras de campo.

4.  **Visualizador de PDF**
    *   Tela que utiliza um WebView para exibir o PDF gerado pela API.
    *   Opções de download e compartilhamento nativo.

## 👥 Equipe e Prazo do Projeto

O desenvolvimento foi planejado para **15 dias úteis**, com uma equipe enxuta e especializada.

| Cargo | Alocação | Responsabilidades Principais |
| :--- | :--- | :--- |
| **Dev Full-Stack Sênior** | 100% | Backend (API, DB, PDF), arquitetura e DevOps. |
| **Dev Mobile React Native**| 80% | Desenvolvimento das telas e lógica do app React Native. |
| **Designer UI/UX** | 40% | Wireframes, protótipo navegável e design system. |
| **QA (Quality Assurance)** | 25% | Testes funcionais, e2e e validação dos builds. |

## 📦 Docker Compose (multi-contêiner)

```yaml
version: '3.8'

services:
  api:
    build: ./api
    ports:
      - "4000:4000"
    env_file:
      - ./api/.env
    depends_on:
      - db

  db:
    image: mysql:8.0
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: dallas_construction_db
    ports:
      - "3306:3306"

  adminer:
    image: adminer
    restart: always
    ports:
      - "8080:8080"
```

## 📊 API – Endpoints Principais

| Método | Endpoint | Função |
| :--- | :--- | :--- |
| POST | `/auth/login` | Autentica um usuário e retorna um token JWT. |
| GET | `/orcamentos` | Lista todos os orçamentos (com filtros e paginação). |
| POST | `/orcamentos` | Cria um novo orçamento. |
| PUT | `/orcamentos/:id` | Atualiza um orçamento existente. |
| DELETE | `/orcamentos/:id` | Remove um orçamento. |
| POST | `/orcamentos/:id/duplicar`| Cria uma cópia exata de um orçamento. |
| GET | `/orcamentos/:id/pdf` | Gera e retorna o arquivo PDF de um orçamento. |

## 📆 Cronograma de Desenvolvimento (15 Dias Úteis)

| Semana | Entregas Principais |
| :--- | :--- |
| **1** | Kick-off, design system, arquitetura do monorepo, backend base (Auth, CRUD) e testes de cálculo. |
| **2** | Implementação da geração de PDF, desenvolvimento das telas do app (Login, Dashboard, Formulário) e integração com a API. |
| **3** | Geração dos builds (APK/IPA), testes e2e, rodada final de QA, documentação e handoff do projeto. |

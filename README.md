# Foodiary API

Esta é a API de backend para o aplicativo Foodiary, responsável por gerenciar dados de usuários, refeições e integrações com serviços de nuvem. A API é construída utilizando **Node.js** e **Serverless Framework**, otimizada para implantação em ambientes **AWS Lambda**.

## Visão Geral

A Foodiary API oferece um conjunto de endpoints para autenticação de usuários, registro e consulta de refeições, e processamento de dados relacionados a fotos e informações nutricionais. Ela foi projetada para ser escalável e eficiente, aproveitando os serviços serverless da AWS.

## Funcionalidades Principais

- **Autenticação de Usuários:** Endpoints para `signin` e `signup`.
- **Gerenciamento de Refeições:** CRUD (Create, Read, Update, Delete) de refeições, incluindo `createMeal`, `listMeals` e `getMealById`.
- **Upload de Arquivos:** Integração com S3 para upload de imagens de refeições.
- **Processamento Assíncrono:** Utilização de SQS para processamento em segundo plano de dados de refeições (ex: análise de imagem).
- **Integração com IA:** Utiliza OpenAI para serviços de inteligência artificial (provavelmente para análise de refeições).

## Tecnologias Utilizadas

- **Backend:** Node.js
- **Framework Serverless:** Serverless Framework
- **Provedor de Nuvem:** AWS (Lambda, S3, SQS)
- **Banco de Dados:** Drizzle ORM com Neon Database (PostgreSQL compatível)
- **Autenticação:** JWT (JSON Web Tokens) e bcryptjs para hashing de senhas.
- **Validação:** Zod para validação de esquemas.
- **Inteligência Artificial:** OpenAI API.

## Estrutura do Projeto

O projeto da API é organizado da seguinte forma:

- `src/controllers/`: Contém a lógica de controle para cada endpoint da API.
- `src/functions/`: Funções Lambda que são os handlers dos eventos da API.
- `src/db/`: Configuração do banco de dados e esquemas com Drizzle ORM.
- `src/clients/`: Clientes para serviços AWS como S3 e SQS.
- `src/services/`: Serviços de negócio, incluindo a integração com a API da OpenAI.
- `src/queues/`: Definições de filas SQS.
- `src/types/`: Definições de tipos TypeScript.
- `src/utils/`: Funções utilitárias.

## Endpoints da API

A API expõe os seguintes endpoints via HTTP API Gateway:

- `POST /signin`: Autentica um usuário existente.
- `POST /signup`: Registra um novo usuário.
- `GET /me`: Retorna informações do usuário autenticado.
- `POST /meals`: Cria uma nova refeição.
- `GET /meals`: Lista todas as refeições do usuário autenticado.
- `GET /meals/{mealId}`: Retorna os detalhes de uma refeição específica pelo ID.

## Configuração e Implantação

### Pré-requisitos

- Node.js (versão 22.x ou superior)
- npm ou yarn
- Credenciais AWS configuradas
- Serverless Framework CLI instalado globalmente (`npm install -g serverless`)

### Variáveis de Ambiente

As seguintes variáveis de ambiente são necessárias para o funcionamento da API:

- `DATABASE_URL`: URL de conexão com o banco de dados PostgreSQL (Neon).
- `JWT_SECRET`: Chave secreta para assinatura e verificação de JWTs.
- `OPENAI_API_KEY`: Chave da API da OpenAI.
- `BUCKET_NAME`: Nome do bucket S3 para uploads de imagens.
- `MEALS_QUEUE_URL`: URL da fila SQS para processamento de refeições.

### Instalação

1. Clone o repositório:
   ```bash
   https://github.com/joaocarlosms/api-foodiary-app.git
   cd api-foodiary-app
   ```

2. Instale as dependências:
   ```bash
   npm install
   ```

### Desenvolvimento Local

Para rodar a API localmente usando `serverless-offline`:

```bash
sls offline start --reloadHandler
```

### Implantação

Para implantar a API na AWS:

```bash
sls deploy
```

## Banco de Dados

A API utiliza Drizzle ORM para interagir com um banco de dados PostgreSQL. O esquema do banco de dados é definido em `src/db/schema.ts`.



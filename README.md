# node-do-zero

Projeto de estudos de Node.js puro, criado para praticar os fundamentos da plataforma: criação de servidor HTTP, rotas, CRUD e persistência de dados — primeiro em memória e depois com um banco de dados PostgreSQL real.

A API gerencia um cadastro simples de **vídeos**, com operações de criar, listar (com busca), atualizar e deletar.

## Tecnologias

- [Node.js](https://nodejs.org/) (ESM / `type: module`)
- [Fastify](https://fastify.dev/) — framework HTTP
- [PostgreSQL](https://www.postgresql.org/) via [Neon Serverless](https://neon.tech/) (`@neondatabase/serverless`)
- [postgres](https://github.com/porsager/postgres) — client SQL
- [dotenv](https://github.com/motdotla/dotenv) — variáveis de ambiente

## Estrutura do projeto

```
server.js              # Servidor Fastify e definição das rotas
db.js                  # Conexão com o banco (Neon/Postgres)
database-postgres.js   # Implementação do CRUD usando PostgreSQL
database-memory.js     # Implementação do CRUD em memória (Map)
create-table.js        # Script para criar a tabela "videos"
rotas.http             # Exemplos de requisições (REST Client)
```

> O projeto suporta duas implementações de banco de dados (`DatabaseMemory` e `DatabasePostgres`). A escolha é feita importando a classe desejada em [server.js](server.js).

## Pré-requisitos

- Node.js 18+
- Uma instância PostgreSQL (ex: [Neon](https://neon.tech/))

## Configuração

1. Instale as dependências:

   ```bash
   npm install
   ```

2. Crie um arquivo `.env` na raiz do projeto com a string de conexão do banco:

   ```
   DATABASE_URL=postgresql://usuario:senha@host/banco
   ```

3. Crie a tabela `videos` no banco:

   ```bash
   node create-table.js
   ```

## Executando

```bash
npm run dev    # modo desenvolvimento (com --watch)
npm start      # modo produção
```

O servidor inicia na porta definida em `PORT` (padrão: `3333`).

## Rotas da API

| Método | Rota          | Descrição                              |
| ------ | ------------- | --------------------------------------- |
| POST   | `/videos`     | Cria um novo vídeo                      |
| GET    | `/videos`     | Lista vídeos (aceita `?search=` no título) |
| PUT    | `/videos/:id` | Atualiza um vídeo existente             |
| DELETE | `/videos/:id` | Remove um vídeo                         |

### Exemplo de corpo (POST/PUT)

```json
{
  "title": "Video node",
  "description": "Este é o primeiro vídeo",
  "duration": 180
}
```

Exemplos completos de requisições estão disponíveis em [rotas.http](rotas.http) (compatível com a extensão [REST Client](https://marketplace.visualstudio.com/items?itemName=humao.rest-client) do VSCode).

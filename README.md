# Fullstack Starter

## Run locally

### Prerequisites

- Node.js `24.15.0` (see `.nvmrc`)
- pnpm `10.33.0`
- Docker Desktop or another Docker-compatible runtime for PostgreSQL

### 1. Install dependencies

```bash
pnpm install
```

### 2. Configure environment files

```bash
cp .env.example .env
cp apps/server/.env.example apps/server/.env
cp apps/web/.env.example apps/web/.env
```

Set `HOST=127.0.0.1` in `apps/server/.env`, then use the
[Better Auth secret generator](https://www.better-auth.com/docs/installation#secret-key)
to create a secure `BETTER_AUTH_SECRET` of at least 32 characters.

Keep the database name, credentials, and port in `.env` and
`apps/server/.env` aligned. Google client variables are optional; add real OAuth
credentials before enabling Google sign-in.

### 3. Start and initialize PostgreSQL

```bash
pnpm db:up
pnpm db:migrate
```

Apply committed Drizzle migrations whenever you create or update a local
database. When the schema changes, generate a migration with `pnpm db:generate`,
review and commit it, then apply it with `pnpm db:migrate`.

### 4. Start the app

```bash
pnpm dev
```

- Web app: <http://localhost:5173>
- API/auth server: <http://localhost:3000>

Useful database commands:

```bash
pnpm db:logs
pnpm db:studio
pnpm db:down
```

### Quality checks

```bash
pnpm typecheck
pnpm lint
pnpm build
```

### Production migration policy

Commit reviewed Drizzle migrations and run `pnpm db:migrate` during deployment
before starting the API. Do not use `pnpm db:push` against a production database.
Build with `pnpm build`, serve `apps/web/dist` as static files, and start the API
with `pnpm --filter @acme/server start`.

## Monorepo Structure

```
.vscode
  └─ Recommended extensions and settings for VSCode users
apps
  ├─ web
  │   ├─ React 19
  │   ├─ Tanstack Router and Query
  │   ├─ Tanstack Form and Table
  │   ├─ tRPC client
  │   └─ Tailwind CSS v4
  └─ server
      ├─ Fastify v5
      └─ tRPC server
packages
  ├─ api
  │   └─ tRPC v11 router definition
  ├─ auth
  │   └─ Better Auth
  ├─ db
  │   └─ Drizzle & PostresQL
  └─ ui
      └─ Base UI components (right now these live in web)
tooling
  ├─ eslint
  │   └─ shared eslint presets
  ├─ prettier
  │   └─ shared prettier configuration
  └─ typescript
      └─ shared tsconfig you can extend from
```

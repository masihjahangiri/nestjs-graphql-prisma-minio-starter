# NestJS GraphQL Prisma MinIO Starter

Production-ready NestJS starter project with GraphQL (Apollo Server 4), Prisma ORM, MinIO object storage, PgBouncer connection pooling, and JWT authentication. Fully Dockerized for both development and production.

## Stack

| Component | Technology |
|---|---|
| Framework | NestJS 10 |
| API | GraphQL with Apollo Server 4 |
| ORM | Prisma 5 |
| Database | PostgreSQL 15 with PgBouncer |
| Object Storage | MinIO |
| Authentication | Passport JWT + bcrypt |
| Language | TypeScript |
| Runtime | Node.js 18 |
| Container | Docker + Docker Compose |

## Features

- **GraphQL API** with Apollo Server 4 and code-first schema generation
- **Prisma ORM** with migrations, seeding, and Prisma Studio
- **MinIO integration** for S3-compatible object storage with auto-provisioned buckets
- **PgBouncer** connection pooling (transaction mode, 200 max clients, pool size 50)
- **JWT authentication** with Passport.js
- **Docker Compose configs** for production, development (hot reload), database, and object storage
- **ESLint + Prettier** code quality tooling
- **Jest** testing setup

## Quick Start

### Development

1. Clone and configure:

```bash
git clone https://github.com/masihjahangiri/nestjs-graphql-prisma-minio-starter.git
cd nestjs-graphql-prisma-minio-starter
cp .env.example .env
```

2. Start the database and MinIO:

```bash
docker compose -f docker-compose.db.yml up -d
docker compose -f docker-compose.minio.yml up -d
```

3. Install dependencies and run migrations:

```bash
pnpm install
pnpm prisma:migrate
pnpm prisma:generate
pnpm prisma:seed
```

4. Start the development server:

```bash
pnpm start:dev
```

The GraphQL playground is available at `http://localhost:3333/graphql`.

### Production

```bash
docker compose up -d
```

This builds the app, starts it behind the configured port, and connects to the external Docker network.

## Docker Compose Files

| File | Purpose |
|---|---|
| `docker-compose.yml` | Production deployment |
| `docker-compose.dev.yml` | Development with hot reload and volume mounts |
| `docker-compose.db.yml` | PostgreSQL + PgBouncer |
| `docker-compose.minio.yml` | MinIO + auto-configured bucket |

## Available Scripts

| Command | Description |
|---|---|
| `pnpm start:dev` | Development server with watch mode |
| `pnpm start:debug` | Debug mode |
| `pnpm build` | Production build |
| `pnpm start` | Start production build |
| `pnpm prisma:migrate` | Run database migrations |
| `pnpm prisma:generate` | Generate Prisma client |
| `pnpm prisma:studio` | Open Prisma Studio |
| `pnpm prisma:seed` | Seed the database |
| `pnpm lint` | Run ESLint |
| `pnpm test` | Run tests |

## Configuration

All configuration is via environment variables. See `.env.example` for the full list.

| Variable | Description |
|---|---|
| `PORT` | Application port (default: 3333) |
| `JWT_ACCESS_SECRET` / `JWT_REFRESH_SECRET` | JWT signing keys |
| `POSTGRES_USER` / `POSTGRES_PASSWORD` / `POSTGRES_DB` | Database credentials |
| `DATABASE_URL` | Prisma connection string (routes through PgBouncer) |
| `MINIO_ENDPOINT` / `MINIO_PORT` / `MINIO_BUCKET` | MinIO configuration |
| `MINIO_ACCESS_KEY` / `MINIO_SECRET_KEY` | MinIO credentials |

## License

MIT

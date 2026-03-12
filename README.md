# Prisma Studio with Railway PostgreSQL

A quick setup to browse and manage your [Railway](https://railway.app) PostgreSQL database using [Prisma Studio](https://www.prisma.io/studio), while routing application queries through [Prisma Accelerate](https://www.prisma.io/accelerate).

## Prerequisites

- [Node.js](https://nodejs.org/) (v18 or later)
- A Railway PostgreSQL database
- A Prisma Accelerate API key (get one at [console.prisma.io](https://console.prisma.io))

## Connection Setup

This project uses **two connection strings** for different purposes:

| Variable | Protocol | Used By | Purpose |
|---|---|---|---|
| `DATABASE_URL` | `prisma://` | Application (`src/index.ts`) | Routes queries through Prisma Accelerate for connection pooling and caching |
| `DIRECT_DATABASE_URL` | `postgresql://` | Prisma Studio, migrations | Connects directly to the Railway PostgreSQL database |

Prisma Studio does not support Accelerate (`prisma://`) URLs, so it connects directly to the database. The application benefits from Accelerate's connection pooling, caching, and global edge network.

## Getting Started

### 1. Install dependencies

```bash
npm install
```

### 2. Configure your database connection

Copy the example env file and fill in your values:

```bash
cp .env.example .env
```

Set `DIRECT_DATABASE_URL` to your Railway PostgreSQL connection string (found under your service's **Variables** or **Connect** tab) and `DATABASE_URL` to your Prisma Accelerate connection string.

### 3. Pull your database schema

Introspect your Railway database to generate a Prisma schema that reflects your existing tables:

```bash
npx prisma db pull
```

This updates `prisma/schema.prisma` with models matching the tables in your database.

### 4. Generate Prisma Client

```bash
npx prisma generate
```

### 5. Launch Prisma Studio

```bash
npx prisma studio
```

Studio connects via `DIRECT_DATABASE_URL` and opens in your browser (default: http://localhost:5555). From there you can view, create, edit, and delete records.

### 6. Run the application

```bash
npm start
```

The app connects via `DATABASE_URL` (Prisma Accelerate) to execute queries.

## Project Structure

```
├── .env                  # Your connection strings (not committed)
├── .env.example          # Example env file (safe to commit)
├── package.json
├── prisma.config.ts      # Prisma config — uses DIRECT_DATABASE_URL for Studio & migrations
├── tsconfig.json
├── prisma/
│   └── schema.prisma     # Data model
└── src/
    └── index.ts          # Application entry point — uses DATABASE_URL via Accelerate
```

## Resources

- [Prisma Accelerate docs](https://www.prisma.io/docs/accelerate)
- [Prisma Studio docs](https://www.prisma.io/docs/orm/tools/prisma-studio)
- [Prisma ORM docs](https://www.prisma.io/docs)
- [Railway docs](https://docs.railway.app)

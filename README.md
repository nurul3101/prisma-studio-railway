# Prisma Studio with Railway PostgreSQL

A quick setup to browse and manage your [Railway](https://railway.app) PostgreSQL database using [Prisma Studio](https://www.prisma.io/studio).

## Prerequisites

- [Node.js](https://nodejs.org/) (v18 or later)
- A Railway PostgreSQL database and its connection string

## Getting Started

### 1. Install dependencies

```bash
npm install
```

### 2. Configure your database connection

Create a `.env` file in the project root:

```bash
touch .env
```

Open it and add your Railway database connection string:

```
DATABASE_URL="postgresql://USER:PASSWORD@HOST:PORT/DATABASE"
```

You can find your connection string in the Railway dashboard under your PostgreSQL service's **Variables** or **Connect** tab.

### 3. Pull your database schema

Introspect your Railway database to generate a Prisma schema that reflects your existing tables:

```bash
npx prisma db pull
```

This updates `prisma/schema.prisma` with models matching the tables in your database.

### 4. Launch Prisma Studio

```bash
npx prisma studio
```

Prisma Studio will open in your browser (default: http://localhost:5555). From there you can view, create, edit, and delete records in your Railway database.

## Project Structure

```
├── .env                  # Your database connection string (not committed)
├── package.json
├── prisma.config.ts      # Prisma config — reads DATABASE_URL from .env
├── tsconfig.json
├── prisma/
│   └── schema.prisma     # Data model
└── src/
    └── index.ts          # Sample script to test the connection
```

## Resources

- [Prisma Studio docs](https://www.prisma.io/docs/orm/tools/prisma-studio)
- [Prisma ORM docs](https://www.prisma.io/docs)
- [Railway docs](https://docs.railway.app)

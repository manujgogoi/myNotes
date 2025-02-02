# Basics

```bash
npm init -y
npm install express dotenv cors helmet morgan compression zod
npm install @prisma/client pg
npm install --save-dev prisma jest supertest ts-jest @types/jest @types/supertest
npm i --save-dev @types/express @types/cors @types/morgan @types/compression

npm install bcrypt
npm install --save-dev @types/bcrypt
npx tsc --init

# Install postgresql on Mac
brew install postgresql
brew services start postgresql
psql --version
psql postgres # Start the PostgreSQL shell
\q # Exit from `psql` shell
```

Run the following SQL commands to create a new database and user:

```sh
psql postgres # Start PostgreSQL Shell
CREATE DATABASE testdb;
\c testdb; # Switch to testdb
CREATE USER testuser WITH ENCRYPTED PASSWORD 'testpassword';
GRANT ALL PRIVILEGES ON DATABASE testdb TO testuser;
ALTER ROLE testuser WITH CREATEDB;
```

## (Optional) How to delete a database and database user

```sql
DROP DATABASE IF EXISTS testdb;
DROP ROLE IF EXISTS testuser;
ERROR:  role "testuser" cannot be dropped because some objects depend on it
DETAIL:  privileges for schema public
privileges for default privileges on new relations belonging to role manuj in schema public

REVOKE ALL PRIVILEGES ON SCHEMA public FROM testuser;
REVOKE ALL PRIVILEGES ON DATABASE postgres FROM testuser;

ALTER DEFAULT PRIVILEGES FOR ROLE manuj IN SCHEMA public REVOKE ALL ON TABLES FROM testuser;
ALTER DEFAULT PRIVILEGES FOR ROLE manuj IN SCHEMA public REVOKE ALL ON SEQUENCES FROM testuser;
ALTER DEFAULT PRIVILEGES FOR ROLE manuj IN SCHEMA public REVOKE ALL ON FUNCTIONS FROM testuser;

DROP ROLE IF EXISTS testuser;

SELECT nspname, pg_catalog.pg_get_userbyid(nspowner)
FROM pg_catalog.pg_namespace
WHERE nspname = 'public';
```

## Config Typescrpt

File: `tsconfig.json`

```json
{
  "compilerOptions": {
    "outDir": "./dist",
    "rootDir": "./src",
    "moduleResolution": "node",
    "esModuleInterop": true,
    "strict": true
  }
}
```

## Config Prisma and Postgres

```sh
npx prisma init
```

This creates a `.env` file and a `prisma/schema.prisma` file.

Update `.env`:

```ini
DATABASE_URL="postgresql://testuser:testpassword@localhost:5432/testdb?schema=public"
```

### Define Prisma Schema (`prisma/schema.prisma`)

```prisma
generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

model User {
  id        String @id @default(uuid())
  email     String @unique
  password  String
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt

  @@map("users")  // Ensures PostgreSQL table name is "users"
}

```

## Configure code formatter for prisma in vscode

- **Code** -> **Settings** -> **Settings** -> on Right Top Corner click **Open Settings (JSON)**
- Update/ Add the following line:

```json
{
  // Other settings
  "[prisma]": {
    "editor.defaultFormatter": "Prisma.prisma",
    "editor.formatOnSave": true
  }
}
```

## Setup the dev server

### 1. `src/config/db.ts`

```ts
import { PrismaClient } from "@prisma/client";

const prisma = new PrismaClient();

export default prisma;
```

### 2. `src/script.ts`

```ts
import prisma from "./config/db";

async function main() {
  const user = await prisma.user.create({
    data: { email: "manujgogoi2@gmail.com", password: "123456" },
  });
  //   const users = await prisma.user.findMany();
  console.log("User: ", users);
}

main()
  .catch((e) => {
    console.error(e.message);
  })
  .finally(async () => {
    await prisma.$disconnect(); // Optional
  });
```

### 3. Update the `package.json` file

```json
{
  // Other codes
  "main": "server.ts", // Update this
  "scripts": {
    "dev": "nodemon src/script.ts", // Add this
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  // Other codes
  "dependencies": {
    // Other codes
  },
  "devDependencies": {
    // Other codes
  }
}
```

### 4. Run the dev server

```sh
npm run dev
```

### 5. (Optional)

Generate Prisma Code for code auto completion

```sh
npx prisma generate
```

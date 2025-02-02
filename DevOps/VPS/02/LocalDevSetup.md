# Express.js, Postgresql, Prisma Setup

## 1. Initialize Project

```bash
npm init -y
npm install express dotenv cors helmet morgan compression zod
npm install @prisma/client pg
npm install --save-dev prisma jest supertest ts-jest @types/jest @types/supertest
npm i --save-dev @types/express @types/cors @types/morgan @types/compression
npm install bcrypt
npm install --save-dev @types/bcrypt
npx tsc --init
```

## 2. TypeScript config

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

## 3. Configure Prisma & Postgres

```sh
npx prisma init
```

This creates a `.env` file and a `prisma/schema.prisma` file.

Update `.env`:

```sh
DATABASE_URL="postgresql://user:password@localhost:5432/mydb"
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
}

```

### Set up PostgreSQL Connection

On macOS, install PostgreSQL using Homebrew:

```sh
brew install postgresql
brew services start postgresql
psql --version
psql postgres # Start the PostgreSQL shell
```

Run the following SQL commands to create a new database and user:

```sh
CREATE DATABASE testdb;
CREATE USER testuser WITH ENCRYPTED PASSWORD 'testpassword';
GRANT ALL PRIVILEGES ON DATABASE testdb TO testuser;
ALTER ROLE testuser WITH CREATEDB;
```

Exit the `psql` shell:

```sh
\q
```

### Configure Database Connection

Edit the `.env` file and update `DATABASE_URL`:

```ini
DATABASE_URL="postgresql://testuser:testpassword@localhost:5432/testdb?schema=public"
```

### Delete a database and database user

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

### Run prisma migrate

```sh
npx prisma migrate dev --name init
```

## Directory structure

```sh
src/
│── config/        # Configuration files
│── controllers/   # Route handlers
│── middleware/    # Custom middleware
│── routes/        # API routes
│── services/      # Business logic
│── tests/         # Unit tests
│── app.ts         # Main Express app
│── server.ts      # Entry point
prisma/
│── schema.prisma  # Database schema
```

### 1. `src/config/db.ts`

```ts
import { PrismaClient } from "@prisma/client";

const prisma = new PrismaClient();

export default prisma;
```

### 2. `src/app.ts`

```ts
import express from "express";
import cors from "cors";
import helmet from "helmet";
import morgan from "morgan";
import compression from "compression";
import userRoutes from "./routes/user.routes";

const app = express();

app.use(cors());
app.use(helmet());
app.use(morgan("dev"));
app.use(compression());
app.use(express.json());

app.use("/api/users", userRoutes);

export default app;
```

### 3. `src/server.ts`

```ts
import app from "./app";
import dotenv from "dotenv";

dotenv.config();

const PORT = process.env.PORT || 5000;

app.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`);
});
```

### 4. User Authentication

`src/controllers/user.controller.ts`

```ts
import { Request, Response } from "express";
import prisma from "../config/db";
import bcrypt from "bcrypt";

export const registerUser = async (req: Request, res: Response) => {
  try {
    const { email, password } = req.body;
    const hashedPassword = await bcrypt.hash(password, 10);

    const user = await prisma.user.create({
      data: { email, password: hashedPassword },
    });

    res.status(201).json({ message: "User created", userId: user.id });
  } catch (error) {
    res.status(500).json({ error: "Internal Server Error" });
  }
};
```

`src/routes/user.routes.ts`

```ts
import { Router } from "express";
import { registerUser } from "../controllers/user.controller";

const router = Router();

router.post("/register", registerUser);

export default router;
```

### 5. Start Developing

- Install `nodemon`

```sh
npm install --save-dev nodemon
npm install --save-dev ts-node
```

Update `package.json` file

```json
{
  // Other codes
  "main": "server.ts", // Add this
  "scripts": {
    "dev": "nodemon src/script.ts", // Add this
    "test": "echo \"Error: no test specified\" && exit 1"
  }
  // Other codes
}
```

Create a temporary `script.ts` file

```ts
import prisma from "./config/db";

async function main() {
  //   const user = await prisma.user.create({
  //     data: { email: "manujgogoi2@gmail.com", password: "123456" },
  //   });
  const users = await prisma.user.findMany();
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

Run the dev server:

```sh
npm run dev
```

### 6. Testing with Jest

`jest.config.js`

```js
module.exports = {
  preset: "ts-jest",
  testEnvironment: "node",
};
```

`src/tests/user.test.ts`

```ts
import request from "supertest";
import app from "../app";

describe("User Registration", () => {
  it("should create a new user", async () => {
    const res = await request(app)
      .post("/api/users/register")
      .send({ email: "test@example.com", password: "password123" });

    expect(res.status).toBe(201);
    expect(res.body).toHaveProperty("userId");
  });
});
```

```sh
npx jest
```

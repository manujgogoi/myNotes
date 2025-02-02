# Prisma File

## 1. Provider

## 2. Data Source

## 3. Model

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

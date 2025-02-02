# Model

```prisma
// Other code

model User {
    id Int @id @default(autoincrement())
    name String? // name is optional
    email String
    isAdmin Boolean
    preferences Json
    ratings Float
}
```

Model consists of 4 parts

- Name (id)
- Data Type (Int)
- Field type Modifiers (`?` in name field - optional)
- Attributes (@id)

Another Example Model

```prisma
model User {
  id          String          @id @default(uuid())
  email       String          @unique
  password    String
  isAdmin     Boolean
  largeNumber BigInt
  balance     Decimal
  preference  Json
  blob        Bytes
  rating      Float           @default(0)
  createdAt   DateTime        @default(now())
  updatedAt   DateTime        @updatedAt
  unknown     Unsupported("")

  @@map("users") // Ensures PostgreSQL table name is "users"
}
```

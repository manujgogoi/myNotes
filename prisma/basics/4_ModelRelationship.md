# Relationship

## 1. One to Many Relationship

```prisma
model User {
  id        String   @id @default(uuid())
  name      String
  isAdmin   Boolean
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
  Post      Post[]

  @@map("users") // Ensures PostgreSQL table name is "users"
}

model Post {
  id          String   @id @default(uuid())
  title       String
  description String
  rating      Float
  createdAt   DateTime @default(now())
  updatedAt   DateTime @updatedAt
  author      User     @relation(fields: [userId], references: [id])
  userId      String

  @@map("posts")
}
```

### Version 2

```prisma
model User {
  id             String   @id @default(uuid())
  name           String
  isAdmin        Boolean
  createdAt      DateTime @default(now())
  updatedAt      DateTime @updatedAt
  writtenPosts   Post[]   @relation("WrittenPosts")
  favouritePosts Post[]   @relation("FavoritePosts")

  @@map("users") // Ensures PostgreSQL table name is "users"
}

model Post {
  id            String   @id @default(uuid())
  title         String
  description   String
  rating        Float
  createdAt     DateTime @default(now())
  updatedAt     DateTime @updatedAt
  author        User     @relation("WrittenPosts", fields: [userId], references: [id])
  userId        String
  favoritedBy   User     @relation("FavoritePosts", fields: [favoritedById], references: [id])
  favoritedById String

  @@map("posts")
}
```

## 2. Many to Many Relationship

```prisma
model User {
  id             String   @id @default(uuid())
  name           String
  isAdmin        Boolean
  createdAt      DateTime @default(now())
  updatedAt      DateTime @updatedAt
  writtenPosts   Post[]   @relation("WrittenPosts")
  favouritePosts Post[]   @relation("FavoritePosts")

  @@map("users") // Ensures PostgreSQL table name is "users"
}

model Post {
  id            String     @id @default(uuid())
  title         String
  description   String
  rating        Float
  createdAt     DateTime   @default(now())
  updatedAt     DateTime   @updatedAt
  author        User       @relation("WrittenPosts", fields: [authorId], references: [id])
  authorId      String
  favoritedBy   User       @relation("FavoritePosts", fields: [favoritedById], references: [id])
  favoritedById String
  categories    Category[]

  @@map("posts")
}

model Category {
  id    String @id @default(uuid())
  name  String
  posts Post[]

  @@map("categories")
}
```

## 3. One to One Relationship

```prisma
model User {
  id             String          @id @default(uuid())
  name           String
  isAdmin        Boolean
  createdAt      DateTime        @default(now())
  updatedAt      DateTime        @updatedAt
  writtenPosts   Post[]          @relation("WrittenPosts")
  favouritePosts Post[]          @relation("FavoritePosts")
  UserPreference UserPreference?

  @@map("users") // Ensures PostgreSQL table name is "users"
}

model UserPreference {
  id           String  @id @default(uuid())
  emailUpdates Boolean
  user         User    @relation(fields: [userId], references: [id])
  userId       String  @unique

  @@map("user_preferences")
}
```

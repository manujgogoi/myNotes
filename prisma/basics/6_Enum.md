# ENUM

```prisma
model User {
  id             String          @id @default(uuid())
  name           String
  age            Int
  email          String          @unique
  role           Role            @default(BASIC)
  createdAt      DateTime        @default(now())
  updatedAt      DateTime        @updatedAt
  writtenPosts   Post[]          @relation("WrittenPosts")
  favoritePosts  Post[]          @relation("FavoritePosts")
  UserPreference UserPreference?

  @@unique([name, age])
  @@index([email])
  @@map("users") // Ensures PostgreSQL table name is "users"
}

enum Role {
  BASIC
  ADMIN
}
```

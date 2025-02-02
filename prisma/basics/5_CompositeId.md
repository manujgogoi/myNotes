# Composite Id

```prisma
model Post {
  // id            String     @id @default(uuid())
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

  @@id([title, authorId])
  @@map("posts")
}
```

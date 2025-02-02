# Uses

```ts
// 1. Create user
const user = await prisma.user.create({
  data: { name: "Manuj Gogoi", age: 39, email: "manujgogoi2@gmail.com" },
});

// 2. Find All Users
const users = await prisma.user.findMany();
console.log("User: ", users);

// 3. Delete All Users
const users = await prisma.user.deleteMany();
console.log("Deleted Users: ", users);
```

## Get Relational data

Update `.prisma` file to achieve this

```prisma
model User {
//   Other fields
  userPreference   UserPreference? @relation(fields: [userPreferenceId], references: [id])
  userPreferenceId String?         @unique
// Ohter fields
}

model UserPreference {
// Other fields
  User   User?
}
```

Run the migration

```sh
npx prisma migrate dev --name update_preference_column
```

```ts
const user = await prisma.user.create({
  data: {
    name: "Manuj Gogoi",
    age: 39,
    email: "manujgogoi2@gmail.com",
    userPreference: {
      create: {
        emailUpdates: true,
      },
    },
  },
  include: {
    userPreference: true,
  },
});
```

```sh
npm run dev
```

```ts
const user = await prisma.user.create({
  data: {
    name: "Manuj Gogoi",
    age: 39,
    email: "manujgogoi2@gmail.com",
    userPreference: {
      create: {
        emailUpdates: true,
      },
    },
  },
  select: {
    name: true,
    userPreference: true,
  },
});
```

```ts
const user = await prisma.user.create({
  data: {
    name: "Manuj Gogoi",
    age: 39,
    email: "manujgogoi2@gmail.com",
    userPreference: {
      create: {
        emailUpdates: true,
      },
    },
  },
  select: {
    name: true,
    userPreference: {
      select: { id: true },
    },
  },
});
```

```ts
const users = await prisma.user.createMany({
  data: [
    {
      name: "Manuj Gogoi",
      age: 39,
      email: "manujgogoi2@gmail.com",
    },
    {
      name: "Dinesh Gowala",
      age: 38,
      email: "dinesh123@gmail.com",
    },
  ],
});
```

```ts

```

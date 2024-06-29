# TypeScript Integration with Supabase

1. In the project root terminal

```sh
npx supabase login

# output:
#-------------------------------

# Need to install the following packages:
# supabase@1.178.2
#Ok to proceed? (y) y

# Hello from Supabase! Press Enter to open browser and login automatically.

# Here is your login link in case browser did not open https://supabase.com/dashboard/cli/login?session_id=0a78d006-0f40-40d4-a0c1-b4c4265ad182&token_name=cli_manuj@Manujs-MacBook-Air.local_1719659320&public_key=042733fdc2ef8e5aab408edfa3cf91b333eb84c5d23d13486e9dd9657830830d850808e2948517b38497f7407f9542e9bbbaa8df7bd8ee90fbdb7bdc5d338acedf

# Token cli_manuj@Manujs-MacBook-Air.local_1719659320 created successfully.

# You are now logged in. Happy coding!
```

2. Find the project id
   In supabase dashboard -> Project Settings -> In General Settings section you will see the Reference Id -> copy it

In project root terminal

```sh
npx supabase gen types typescript --project-id <your-project-id> > src/types/database.types.ts
```

3. Replace the project-id with the copied id and run the command
   Example:

```sh
npx supabase gen types typescript --project-id yxeebedbieeyudmgmmxl > src/types/database.types.ts
```

4. Now Go to project_root -> lib/supabase.ts file [It is provided by supabase]
5. Import this

```ts
import { Database } from "@/src/types/database.types";
```

6. Add the `Database` type to following code (last section)

```ts
// See the line below: <Database> is newly added
export const supabase = createClient<Database>(supabaseUrl, supabaseAnonKey, {
  auth: {
    storage: new LargeSecureStore(),
    autoRefreshToken: true,
    persistSession: true,
    detectSessionInUrl: false,
  },
});
```

- Next time if any changes in DB, then run the supabase cli command again to update the file.

[Done]

## Use database types instead of custom types

1. In `types/index.ts` file add the following at the top

```ts
import { Database } from "@/src/types/database.types";

// Postgress Database Types
export type Tables<T extends keyof Database["public"]["Tables"]> =
  Database["public"]["Tables"][T]["Row"];
export type Enums<T extends keyof Database["public"]["Enums"]> =
  Database["public"]["Enums"][T];
```

2. Consume DB types
   In `/src/components/ProductListItem.tsx` file:

```ts
import { Product, Tables } from "@/src/types";
// Remove Product and import Tables instead

type ProductListItemProps = {
  product: Product; // Remove this
  product: Tables<"products">; // Add this
};
```

### Update all `Product` occurances (References)

- In `src/providers/CartProvider.tsx` file

# What is an ORM ? 
## Objet relational map

Note: I will probrably keep to using pydantic and fastapi though, but this is some usesfull shit to learn, because if I need to create an application using these shit ass tecnologies I will know how to use this crap.


Its just a way for you to interact with your database without needing to use sql, it makes it easiear to interact with the db.


## I am learning DrizzleORM right now, which is a ORM for typescript, these are some functionalities of it:

### How to set it up ono a next js typescript project:
First we start by creating our db folder inside the lib directory, then we create the index.ts file which will contain our db connection and the drizzle ORM function.

To use Drizzle we'll also need a schema file which will contain the schema for our database. This schema.ts file also goes inside the db folder and it will keep our models for the db.

this is the code inside the index.ts file:
```
import {neon,neonConfig} from '@neondatabase/serverless'
import {drizzle} from 'drizzle-orm/neon-http'


neonConfig.fetchConnectionCache = true

if (!process.env.DATABASE_URL){
    throw new Error('database url is not found')
}


const sql = neon(process.env.DATABASE_URL)

```
This is the code inside the schema.ts file for a simple project:

```
import {
  pgTable,
  serial,
  text,
  timestamp,
  varchar,
  integer,
  pgEnum,
} from "drizzle-orm/pg-core";

export const userSystemEnum = pgEnum("user_system_enum", ["system", "user"]);

export const chats = pgTable("chats", {
  id: serial("id").primaryKey(),
  pdfName: text("pdf_name").notNull(),
  pdfUrl: text("pdf_url").notNull(),
  createdAt: timestamp("created_at").notNull().defaultNow(),
  userId: varchar("user_id", { length: 256 }).notNull(),
  fileKey: text("file_key").notNull(),
});

export const messages = pgTable("messages", {
  id: serial("id").primaryKey(),
  chatId: integer("chat_id")
    .references(() => chats.id)
    .notNull(),
  content: text("content").notNull(),
  createdAt: timestamp("created_at").notNull().defaultNow(),
  role: userSystemEnum("role").notNull(),
});

```

to migrate the database schema to the actual neon database, we can use the drizzle-kit. To use the drizzle kit, we first need to create a drizzle.config.ts file insidei the root of our project and paste this code inside of it:

```
import type { Config } from "drizzle-kit";
import * as dotenv from "dotenv";
dotenv.config({ path: ".env" });
export default {
  driver: "pg",
  schema: "./src/lib/db/schema.ts",
  dbCredentials: {
    connectionString: process.env.DATABASE_URL!,
  },
} satisfies Config;


```
(note: We need to go into the tsconfig and change the target from es5 to es6)
After all this is done we can do a :

```
npx drizzle-kit push:pg

```

after that I can run :
```
npx drizzle-kit studio
```

which will open a server database for me to mess around.





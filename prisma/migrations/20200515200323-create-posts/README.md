# Migration `20200515200323-create-posts`

This migration has been generated by Alexsandro at 5/15/2020, 8:03:23 PM.
You can check out the [state of the schema](./schema.prisma) after the migration.

## Database Steps

```sql
CREATE TABLE "public"."Post" (
"authorId" integer  NOT NULL ,"id" SERIAL,"title" text  NOT NULL ,
    PRIMARY KEY ("id"))

ALTER TABLE "public"."Post" ADD FOREIGN KEY ("authorId")REFERENCES "public"."User"("id") ON DELETE CASCADE  ON UPDATE CASCADE
```

## Changes

```diff
diff --git schema.prisma schema.prisma
migration 20200515195910-create-users..20200515200323-create-posts
--- datamodel.dml
+++ datamodel.dml
@@ -2,9 +2,9 @@
 // learn more about it in the docs: https://pris.ly/d/prisma-schema
 datasource db {
   provider = "postgresql"
-  url = "***"
+  url      = env("DATABASE_URL")
 }
 generator client {
   provider = "prisma-client-js"
@@ -13,5 +13,13 @@
 model User {
   id     Int      @id @default(autoincrement())
   name   String?
   email  String   @unique
+  posts  Post[]
+}
+
+model Post {
+  id         Int      @id @default(autoincrement())
+  title      String
+  authorId   Int
+  author     User     @relation(fields: [authorId], references: [id])
 }
```



# Migration `20201007025648`

This migration has been generated by Devin Matte at 10/6/2020, 10:56:48 PM.
You can check out the [state of the schema](./schema.prisma) after the migration.

## Database Steps

```sql
Begin;
CREATE TYPE "public"."jobtype_new" AS ENUM ('co_op', 'full_time');
ALTER TABLE "public"."Position" ALTER COLUMN "job_type" TYPE "jobtype_new" USING ("job_type"::text::"jobtype_new");
ALTER TYPE "jobtype" RENAME TO "jobtype_old";
ALTER TYPE "jobtype_new" RENAME TO "jobtype";
DROP TYPE "jobtype_old";
Commit
```

## Changes

```diff
diff --git schema.prisma schema.prisma
migration 20201006032053-adding-position..20201007025648
--- datamodel.dml
+++ datamodel.dml
@@ -3,9 +3,9 @@
 }
 datasource db {
   provider = "postgresql"
-  url = "***"
+  url = "***"
 }
 model City {
   id       Int       @id @default(autoincrement())
@@ -76,10 +76,10 @@
   stipend
 }
 enum jobtype {
-  co_op @map("co-op")
-  full_time @map("full-time")
+  co_op
+  full_time
 }
 enum paytype {
   hourly
```


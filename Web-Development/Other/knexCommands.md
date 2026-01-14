```
knex init
knex migrate:make <name>
knex migrate:latest
knex migrate:up
knex migrate:down
knex migrate:rollback
knex migrate:rollback --all
knex migrate:status
knex migrate:currentVersion

knex seed:make <name>
knex seed:run

knex db:create
knex db:drop

knex help
knex --version
```





The **range of `BIGINT` (BigInteger)** depends on whether it is **signed** or **unsigned**, and on the database.

---

## 1️⃣ Signed `BIGINT` (default)

Used when you **don’t** specify `unsigned()`.

### Range

```
-9,223,372,036,854,775,808
to
 9,223,372,036,854,775,807
```

➡️ This is a **64-bit signed integer** (`2^63`).

### In databases

* **MySQL / MariaDB**: `BIGINT`
* **PostgreSQL**: `BIGINT`
* **Knex**: `table.bigInteger()`

---

## 2️⃣ Unsigned `BIGINT`

Used when you add `.unsigned()`.

### Range

```
0
to
18,446,744,073,709,551,615
```

➡️ This is a **64-bit unsigned integer** (`2^64 - 1`).

### In databases

* **MySQL / MariaDB**: `BIGINT UNSIGNED` ✅
* **PostgreSQL**: ❌ No native unsigned support

  * Knex silently ignores `.unsigned()`

---

## Quick comparison

| Type            | Min      | Max     |
| --------------- | -------- | ------- |
| BIGINT (signed) | -9.22e18 | 9.22e18 |
| BIGINT UNSIGNED | 0        | 1.84e19 |

---

## Why IDs often use `BIGINT UNSIGNED`

* IDs are **never negative**
* Doubles the positive range
* Safe for:

  * High-scale systems
  * Long-running databases
  * Distributed ID generators

Example:

```ts
table.bigInteger('id').unsigned().primary();
```

---

## Knex + PostgreSQL note (important)

If you are using **PostgreSQL**:

* `.unsigned()` has **no effect**
* Range is always **signed BIGINT**

So this is fine:

```ts
table.bigInteger('coupon_id');
```

But this is mainly for **MySQL compatibility**:

```ts
table.bigInteger('coupon_id').unsigned();
```

---

### Summary

* `BIGINT` = **64-bit integer**
* Signed range: **±9.22 quintillion**
* Unsigned range: **0 to 18.44 quintillion**
* `.unsigned()` matters in **MySQL**, ignored in **Postgres**

If you want, I can also explain `INT`, `SMALLINT`, or when **BIGINT is overkill**.



`unsigned` means **the column cannot store negative values**.

### In your code

```ts
table
  .bigInteger('coupon_id')
  .unsigned()
```

This tells the database:

➡️ `coupon_id` can only contain **0 or positive numbers**
➡️ **Negative values are not allowed**

### Why it’s used here

Foreign keys usually reference **ID columns**, and ID columns are almost always:

* Auto-incremented
* Positive numbers only

So if `coupons.id` is `UNSIGNED`, then `coupon_id` **must also be UNSIGNED** to match it.

### Example

| Value | Allowed? |
| ----- | -------- |
| `1`   | ✅ Yes    |
| `0`   | ✅ Yes    |
| `-1`  | ❌ No     |

### Database-level meaning

In **MySQL / MariaDB**:

* `BIGINT UNSIGNED`

  * Range: `0` to `18446744073709551615`

In **PostgreSQL**:

* There is **no native `UNSIGNED`**
* Knex ignores `.unsigned()` or maps it safely

### Why this matters for foreign keys

If parent column is:

```sql
id BIGINT UNSIGNED
```

Child column **must match type exactly**:

```sql
coupon_id BIGINT UNSIGNED
```

Otherwise:

* Foreign key creation can fail
* Or behave inconsistently across DBs

### Summary

* `unsigned` = **no negative numbers**
* Used for **IDs and foreign keys**
* Ensures **type compatibility** and **data integrity**
* Mostly relevant for **MySQL/MariaDB**

If you want, I can show how this behaves differently in MySQL vs PostgreSQL.




What is onDelete Cascade here?

import * as Knex from 'knex';
import { id, commonFields } from '../helpers';

export async function up(knex: Knex): Promise<void> {
  return knex.schema.createTable('coupon_customer_mapping', table => {
    id(table);

    table
      .bigInteger('coupon_id')
      .unsigned()
      .notNullable()
      .references('id')
      .inTable('coupons')
      .onDelete('CASCADE');

    table
      .bigInteger('customer_id')
      .notNullable()
      .references('id')
      .inTable('locofastroot')
      .onDelete('CASCADE');

    commonFields(knex, table);

    table.boolean('is_deleted').defaultTo(false);
  });
}

export async function down(knex: Knex): Promise<void> {
  return knex.schema.dropTableIfExists('coupon_customer_mapping');
}


`onDelete('CASCADE')` defines **what should happen to rows in this table when the referenced parent row is deleted**.

In your migration, it is part of a **foreign key constraint**.

### What it means here

```ts
.references('id')
.inTable('coupons')
.onDelete('CASCADE');
```

➡️ If a **row in `coupons` is deleted**, then **all rows in `coupon_customer_mapping` that reference that coupon** will be **automatically deleted by the database**.

Same for `customer_id`:

```ts
.references('id')
.inTable('locofastroot')
.onDelete('CASCADE');
```

➡️ If a **customer is deleted from `locofastroot`**, then **all mapping rows for that customer** will be deleted.

### In plain English

Your table is a **mapping / junction table**.

* Delete a coupon → related coupon-customer mappings are removed
* Delete a customer → related coupon-customer mappings are removed
* No orphan rows remain

### Why this is useful

Without `CASCADE`:

* Deleting a coupon/customer would fail due to foreign key constraint
* Or leave invalid (orphan) records if constraints were disabled

With `CASCADE`:

* Cleanup happens automatically
* Data integrity is maintained

### Important note (soft delete vs hard delete)

You also have:

```ts
table.boolean('is_deleted').defaultTo(false);
```

⚠️ `onDelete('CASCADE')` **only works for hard deletes** (`DELETE FROM coupons ...`).

If you **soft delete** (set `is_deleted = true`):

* Cascade **will NOT trigger**
* You must handle cleanup in application logic if needed

### Summary

* `onDelete('CASCADE')` = *delete child rows automatically when parent row is deleted*
* Applies at **database level**
* Best practice for **junction tables**
* Does **not** apply to soft deletes

If you want, I can explain `RESTRICT`, `SET NULL`, or when **not** to use `CASCADE`.



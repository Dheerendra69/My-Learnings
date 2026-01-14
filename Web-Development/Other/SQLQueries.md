```sql
ALTER TABLE fabric_order_invoice
ADD COLUMN Generated_By VARCHAR(255) NULL;
```
- Null Should be placed after varchar(255). Agar usko varchar ke pehle rakha toh syntax error aa jayega.

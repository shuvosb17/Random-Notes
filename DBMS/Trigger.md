
## What is a Trigger? 🛎️

A **trigger** is a special type of stored program in MySQL that automatically executes (fires) when a specific event occurs in a table.  
Events can be:  
- **INSERT** (adding new data)
- **UPDATE** (changing existing data)
- **DELETE** (removing data)

Triggers help automate tasks, enforce rules, and maintain data integrity without manual intervention.

---

## How Does a Trigger Work? ⚙️

- You define a trigger on a table for a specific event (before/after insert, update, or delete).
- When that event happens, MySQL automatically runs the trigger’s code.
- The trigger can access the data being changed using special keywords:
  - **NEW**: The new data (for INSERT/UPDATE)
  - **OLD**: The old data (for UPDATE/DELETE)

**Example Flow:**  
1. You insert a new row into the `users` table.
2. If there’s an `AFTER INSERT` trigger, MySQL runs the trigger code right after the row is added.

---

## Types of Triggers 🧩

- **BEFORE INSERT**: Runs before a new row is added.
- **AFTER INSERT**: Runs after a new row is added.
- **BEFORE UPDATE**: Runs before a row is updated.
- **AFTER UPDATE**: Runs after a row is updated.
- **BEFORE DELETE**: Runs before a row is deleted.
- **AFTER DELETE**: Runs after a row is deleted.

---

## How to Create a Trigger 📝

**Syntax:**
````sql
CREATE TRIGGER trigger_name
{BEFORE | AFTER} {INSERT | UPDATE | DELETE}
ON table_name
FOR EACH ROW
BEGIN
  -- SQL statements
END;
````

**Example:**  
Suppose you want to log every time a new user is added:

````sql
CREATE TRIGGER log_user_insert
AFTER INSERT ON users
FOR EACH ROW
BEGIN
  INSERT INTO user_log (user_id, action, log_time)
  VALUES (NEW.id, 'User Added', NOW());
END;
````

---

## How to Apply (Use) a Trigger 🚦

- Once created, triggers work automatically.
- You don’t call them directly.
- When you perform the event (e.g., insert a row), the trigger runs.

**Example Usage:**  
````sql
INSERT INTO users (name, email) VALUES ('Alice', 'alice@example.com');
````

**What happens?**  
- The new user is added.
- The trigger runs and adds a log entry to `user_log`.

---

## Output After Running Query 📋

- The main query (e.g., INSERT) does its job (adds/updates/deletes data).
- The trigger’s code also runs, which may:
  - Insert data into another table (like a log)
  - Update other rows
  - Check or modify values

**Example Output:**  
After inserting a user, you’ll see a new row in the `user_log` table:

| user_id | action      | log_time           |
|---------|-------------|--------------------|
| 1       | User Added  | 2025-08-17 10:00:00|

---

## Key Concepts & Rules 🧠

- Triggers are **automatic**—no need to call them.
- Each table can have only one trigger for each event type.
- Triggers can’t return values to the user.
- Use triggers for tasks like logging, validation, or enforcing business rules.

---

## Summary Table

| Concept         | Description                                  |
|-----------------|----------------------------------------------|
| What is it?     | Auto-executed code on table events           |
| Types           | BEFORE/AFTER INSERT, UPDATE, DELETE          |
| How to create   | `CREATE TRIGGER ...`                         |
| How it works    | Runs when event happens, uses NEW/OLD values |
| Output          | Main query + trigger’s actions               |

---

**In short:**  
Triggers are automatic helpers in MySQL that run when you change data in a table. They help keep your data correct, log changes, and enforce rules—all behind the scenes!

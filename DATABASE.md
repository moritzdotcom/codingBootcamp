# Databases

## What is a database?

A database is a collection of data. It is used to store data in a structured way. You can think of it like an excel spreadsheet. While we have different sheets in excel, a database has different tables. Each table has columns and rows. Each column represents a different type of data, and each row represents a single entry.

For example, we could have a table called `users`:

| id  | name   | email            |
| --- | ------ | ---------------- |
| 1   | Sebi   | sebi@gmail.com   |
| 2   | Moritz | moritz@gmail.com |

## How to interact with a database

When working with a SQL database, we can use SQL commands to interact with it. In development there is a concept called `CRUD` which stands for `Create`, `Read`, `Update`, `Delete`. These are the four basic operations that we can perform on a database.

### Read Data

```sql
-- Get all users
SELECT * FROM users;

-- Get a single user
SELECT * FROM users WHERE id = 1;

-- Get only the name of a user
SELECT name FROM users WHERE id = 1;
```

### Create Data

```sql
-- Create a new user
INSERT INTO users (name, email) VALUES ('Nina', 'nina@gmail.com');
```

### Update Data

```sql
-- Update a user
UPDATE users SET email = 'nina@gmx.de' WHERE id = 3;
```

### Delete Data

```sql
-- Delete a user
DELETE FROM users WHERE id = 3;
```

Lets try it out:

```bash
# Start the database
psql postgres

# Create a new database
CREATE DATABASE sebibootcamp;

# Connect to the new database
\c sebibootcamp

# Create a new table
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  name VARCHAR(255),
  email VARCHAR(255)
);

# List all tables
\dt

# Insert a new user
INSERT INTO users (name, email) VALUES ('Sebi', 'sebi@gmail.com');

# Get all users
SELECT * FROM users;
```

## Relations

Now lets imagine we want to build an app where a company can post job listings and users can refer people from their network to these jobs. We would need the following tables:

### Users

| id  | name   | email            |
| --- | ------ | ---------------- |
| 1   | Sebi   | sebi@gmail.com   |
| 2   | Moritz | moritz@gmail.com |
| 3   | Nina   | nina@gmail.com   |

### Companies

| id  | name   |
| --- | ------ |
| 1   | Google |
| 2   | Apple  |
| 3   | Tesla  |

### Jobs

| id  | title        | description     | company |
| --- | ------------ | --------------- | ------- |
| 1   | Software Dev | Build software  | Google  |
| 2   | Marketing    | Sell stuff      | Apple   |
| 3   | Sales        | Sell more stuff | Tesla   |

We could now already build an App that shows us all available jobs stored in the database. But there is a problem of how we store our data. We are storing the company name in the `jobs` table. This is not ideal because if we want to change the name of a company, we would have to update all jobs that are associated with that company. This is where relations come in.

## One to Many Relation

We can create a relation between two tables. In our case, we want to create a relation between the `companies` table and the `jobs` table. We can do this by adding a `company_id` column to the `jobs` table. This column will store the id of the company that the job belongs to.

### Jobs

| id  | title        | description     | company_id |
| --- | ------------ | --------------- | ---------- |
| 1   | Software Dev | Build software  | 1          |
| 2   | Marketing    | Sell stuff      | 2          |
| 3   | Sales        | Sell more stuff | 3          |

Now we can get the company of a job by using the `company_id` column. But we can also get all jobs of a company by using the `company_id` column. This is called a `one to many` relation because `one` company can have `many` jobs.

In an SQL statement we can use the `JOIN` keyword to join two tables together. We can then use the `ON` keyword to specify which columns we want to join on.

```sql
SELECT * FROM jobs
JOIN companies ON jobs.company_id = companies.id;
```

This will return all jobs with the company name like this:

| id  | title        | description     | company_id | company.id | company.name |
| --- | ------------ | --------------- | ---------- | ---------- | ------------ |
| 1   | Software Dev | Build software  | 1          | 1          | Google       |
| 2   | Marketing    | Sell stuff      | 2          | 2          | Apple        |
| 3   | Sales        | Sell more stuff | 3          | 3          | Tesla        |

## Many to Many Relation

Now lets imagine we want to add a feature where users can refer other users to jobs. We would need a new table called `referrals`:

### Referrals

| id  | user_id | job_id | referred           |
| --- | ------- | ------ | ------------------ |
| 1   | 1       | 1      | fridolin@gmail.com |
| 2   | 2       | 1      | norbert@gmail.com  |
| 3   | 3       | 2      | rolf@gmail.com     |

This table stores the `user_id` and the `job_id` of the referral. We can now get all referrals of a user by using the `user_id` column. We can also get all referrals of a job by using the `job_id` column. This is called a `many to many` relation because `many` users can refer `many` jobs.

Now if we want to show Google all referrals they got, we can use the following SQL statement:

```sql
SELECT * FROM referrals
JOIN jobs ON referrals.job_id = jobs.id
JOIN companies ON jobs.company_id = companies.id
WHERE companies.id = 1;
```

This will return all referrals for Google like this:

| id  | user_id | job_id | referred           | job.id | job.title    | job.description | job.company_id | company.id | company.name |
| --- | ------- | ------ | ------------------ | ------ | ------------ | --------------- | -------------- | ---------- | ------------ |
| 1   | 1       | 1      | fridolin@gmail.com | 1      | Software Dev | Build software  | 1              | 1          | Google       |
| 2   | 2       | 1      | norbert@gmail.com  | 1      | Software Dev | Build software  | 1              | 1          | Google       |

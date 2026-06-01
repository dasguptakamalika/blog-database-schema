# Blog Database Schema
    
## Why PostgreSQL
Why PostgreSQL
PostgreSQL is a good choice for this blog system because users, posts,
and comments have clear relationships. A user can create many posts, 
and a post can have many comments. SQL databases handle 
these relationships well using primary keys and foreign keys.

---
# users table

| Field        | Type        | Constraints |
|--------------|-------------|-------------|
| id           | BIGINT      | PRIMARY KEY |
| username | VARCHAR(50)  | UNIQUE, NOT NULL |
| email    | VARCHAR(100) | UNIQUE, NOT NULL |
| password_hash | VARCHAR(255) | NOT NULL    |
| created_at   | TIMESTAMP   | NOT NULL    |

---

# posts table


| Field      | Type         | Constraints                       |
|-------------|--------------|-----------------------------------|
| id          | BIGINT       | PRIMARY KEY                       |
| user_id     | BIGINT       | FOREIGN KEY REFERENCES users(id)  |
| title       | VARCHAR(255) | NOT NULL                          |
| content     | TEXT         | NOT NULL                          |
| created_at  | TIMESTAMP    | NOT NULL                          |
---


# comments table

| Field      | Type      | Constraints                         |
|-------------|-----------|-------------------------------------|
| id          | BIGINT    | PRIMARY KEY                         |
| post_id     | BIGINT    | FOREIGN KEY REFERENCES posts(id)    |
| user_id     | BIGINT    | FOREIGN KEY REFERENCES users(id)    |
| content     | TEXT      | NOT NULL                            |
| created_at  | TIMESTAMP | NOT NULL                            |


## Relationships
One user can create many posts.
Each post belongs to one user.
One post can have many comments.
Each comment belongs to one post.
One user can write many comments.
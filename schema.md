# Blog Database Schema


## Why PostgreSQL

I chose PostgreSQL because a blog system has structured and related data.
Users create posts, and posts can have comments, so a relational database
fits this use case well.
PostgreSQL is also free, reliable and easy to find help for online.

---

# users table

| Field        | Type         | Constraints            |
|--------------|--------------|------------------------|
| id           | BIGSERIAL    | PRIMARY KEY            |
| username | VARCHAR(50)  | UNIQUE, NOT NULL       |
| email    | VARCHAR(100) | UNIQUE, NOT NULL       |
| password_hash | VARCHAR(255) | NOT NULL               |
| created_at   | TIMESTAMP    | NOT NULL DEFAULT NOW() |

---

# posts table


| Field      | Type         | Constraints                                        |
|-------------|--------------|----------------------------------------------------|
| id          | BIGSERIAL    | PRIMARY KEY                                        |
| user_id     | BIGINT       | FOREIGN KEY REFERENCES users(id) ON DELETE CASCADE |
| title       | VARCHAR(255) | NOT NULL                                           |
| content     | TEXT         | NOT NULL                                           |
| created_at  | TIMESTAMP    | NOT NULL DEFAULT NOW()                             |

---


# comments table

| Field      | Type      | Constraints                                        |
|-------------|-----------|----------------------------------------------------|
| id          | BIGSERIAL | PRIMARY KEY                                        |
| post_id     | BIGINT    | FOREIGN KEY REFERENCES posts(id) ON DELETE CASCADE |
| user_id     | BIGINT    | FOREIGN KEY REFERENCES users(id) ON DELETE CASCADE |
| content     | TEXT      | NOT NULL                                           |
| created_at  | TIMESTAMP | NOT NULL DEFAULT NOW()                             |

---

## Relationships        

- One user can create many posts.
- Each post belongs to one user.
- One post can have many comments.
- Each comment belongs to one post.
- One user can write many comments.
- Each comment belongs to one user.
# Next.js Multi Author Platform

A multi-author blogging platform built with Next.js. Users create an account, write and edit their own posts, and get a public profile page. Visitors can search for authors and browse a ranking of the most active writers, while an admin moderates all content from a dedicated panel.

## Features

- **Accounts:** sign up and log in with passwords hashed with bcrypt and JWT-based sessions
- **Posts:** create, edit and delete your own posts
- **Author profiles:** a public page at `/u/[login]` with the author's bio and posts
- **Author search:** find writers by login
- **Most active authors:** a top 5 ranking by post count on the home page
- **Admin panel:** the `admin` account can edit or delete any post
- **REST API:** route handlers for users, posts and a health check

## Tech Stack

| Layer    | Technology                          |
| -------- | ----------------------------------- |
| Frontend | Next.js 16 (App Router), React 19, Tailwind CSS 4 |
| Backend  | Next.js Route Handlers               |
| Auth     | JWT, bcrypt                          |
| ORM / DB | Prisma, PostgreSQL                   |
| Language | TypeScript                           |

## API

| Method   | Endpoint                 | Description                         |
| -------- | ------------------------ | ----------------------------------- |
| `GET`    | `/api/health`            | Health check                        |
| `POST`   | `/api/users/register`    | Create an account                   |
| `POST`   | `/api/users/login`       | Log in and receive a JWT            |
| `GET`    | `/api/users/search`      | Search users by login               |
| `GET`    | `/api/users/top`         | Top 5 authors by post count         |
| `GET`    | `/api/users/[login]`     | Public profile with posts           |
| `GET`    | `/api/posts`             | List all posts                      |
| `POST`   | `/api/posts`             | Create a post (auth required)       |
| `PATCH`  | `/api/posts/[id]`        | Edit a post (author or admin)       |
| `DELETE` | `/api/posts/[id]`        | Delete a post (author or admin)     |

Protected endpoints expect an `Authorization: Bearer <token>` header.

## Getting Started

### Prerequisites

- Node.js 20+
- A PostgreSQL database

### Setup

```bash
git clone https://github.com/GPrzyborowski/inkspace.git
cd inkspace
npm install
```

Create a `.env` file in the project root:

```env
DATABASE_URL="postgresql://user:password@host:5432/db"
DIRECT_URL="postgresql://user:password@host:5432/db"
JWT_SECRET="your-secret-key"
```

Run the migrations and start the dev server:

```bash
npx prisma migrate dev
npm run dev
```

The app runs at [http://localhost:3000](http://localhost:3000).

To get admin access, register an account with the login `admin`.

## Project Structure

```
prisma/            # Prisma schema and migrations
src/
├── app/           # Pages and API route handlers (App Router)
│   ├── api/       # REST endpoints
│   ├── admin/     # Admin panel
│   ├── posts/     # Post view, create and edit pages
│   └── u/[login]/ # Public author profiles
├── components/    # UI components
└── lib/           # Prisma client and auth helpers
```

---

Originally built as a university project for the *Integracja systemów informatycznych* (Information Systems Integration) course.

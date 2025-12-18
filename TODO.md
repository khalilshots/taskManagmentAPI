
# Task Management API – TODO

## Phase 1: Design & Structure

### Core entities

**User**
- id
- name (optional)
- email (unique)
- password (hashed)

**Task**
- id
- user (FK -> User)
- title
- description (optional)
- created_at (auto)
- priority ("low" | "medium" | "high")
- completed (boolean, default false)

### Auth strategy
- JWT (access + refresh)

### Endpoints

**AUTH**
- POST /auth/register
- POST /auth/login
- POST /auth/refresh   (optional but recommended)

**TASKS (requires Authorization header)**
- GET    /tasks
- POST   /tasks
- GET    /tasks/{id}
- PATCH  /tasks/{id}
- DELETE /tasks/{id}

---

## API Contract Examples

### Register
POST /auth/register

Request (JSON):
{
  "email": "kmouhah1@gmail.com",
  "password": "example123"
}

Response (JSON):
{
  "id": 1,
  "email": "kmouhah1@gmail.com"
}

### Login
POST /auth/login

Request (JSON):
{
  "email": "kmouhah1@gmail.com",
  "password": "example123"
}

Response (JSON):
{
  "access": "JWT_ACCESS_TOKEN",
  "refresh": "JWT_REFRESH_TOKEN"
}

---

### Get tasks list
GET /tasks

Headers:
Authorization: Bearer <JWT_ACCESS_TOKEN>

Response (JSON):
{
  "count": 2,
  "results": [
    {
      "id": 1,
      "title": "shopping",
      "description": "buy potatoes",
      "created_at": "2025-01-01T07:01:00Z",
      "priority": "high",
      "completed": false
    },
    {
      "id": 2,
      "title": "stuff",
      "description": "detailed stuff",
      "created_at": "2025-01-01T07:02:00Z",
      "priority": "medium",
      "completed": true
    }
  ]
}

### Create task
POST /tasks

Headers:
Authorization: Bearer <JWT_ACCESS_TOKEN>

Request (JSON):
{
  "title": "somestuffidk",
  "description": "somedetailed stuff idk",
  "priority": "low"
}

Response (JSON):
{
  "id": 3,
  "title": "somestuffidk",
  "description": "somedetailed stuff idk",
  "created_at": "2025-01-01T07:02:00Z",
  "priority": "low",
  "completed": false
}

### Get specific task
GET /tasks/{id}

Headers:
Authorization: Bearer <JWT_ACCESS_TOKEN>

Response (JSON):
{
  "id": 3,
  "title": "somestuffidk",
  "description": "somedetailed stuff idk",
  "created_at": "2025-01-01T07:02:00Z",
  "priority": "low",
  "completed": false
}

### Update task (partial)
PATCH /tasks/{id}

Headers:
Authorization: Bearer <JWT_ACCESS_TOKEN>

Request (JSON):
{
  "title": "changedthisname",
  "completed": true
}

Response (JSON):
{
  "id": 3,
  "title": "changedthisname",
  "description": "somedetailed stuff idk",
  "created_at": "2025-01-01T07:02:00Z",
  "priority": "low",
  "completed": true
}

### Delete task
DELETE /tasks/{id}

Headers:
Authorization: Bearer <JWT_ACCESS_TOKEN>

Response:
204 No Content




## Phase 2: Backend Skeleton
- [ ] Create project folder structure
- [ ] Add Django/DRF placeholders
- [ ] Add serializers and views (no logic yet)

## Phase 3: Quality
- [ ] Add basic tests
- [ ] Improve README
- [ ] Prepare for deployment

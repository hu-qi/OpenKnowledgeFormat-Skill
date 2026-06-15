---
type: API Endpoint
title: Login API
description: API endpoint that authenticates users and returns session information.
resource: https://example.com/api/login
tags: [api, auth, login]
timestamp: 2026-06-16T00:00:00Z
---

# Overview

The Login API authenticates a user and returns session information used by the frontend application.

# Schema

| Field | Type | Description |
|---|---|---|
| `username` | string | User login identifier. |
| `password` | string | User password or credential. |
| `session_id` | string | Session identifier returned after successful authentication. |

# Examples

```http
POST /api/login
Content-Type: application/json

{
  "username": "demo@example.com",
  "password": "********"
}
```

# Relationships

- Called by [Frontend App](/systems/frontend_app.md).
- Creates [User Session](/concepts/user_session.md).

# Citations

[1] [API reference](https://example.com/api/login)

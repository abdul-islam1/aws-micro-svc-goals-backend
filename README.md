# Goals API Backend

A simple RESTful API built with Node.js, Express, and MongoDB for managing personal goals. The application allows users to create, retrieve, and delete goals while persisting data in MongoDB Atlas.

---

## Features

* Create new goals
* Retrieve all goals
* Delete goals by ID
* MongoDB Atlas integration using Mongoose
* Request logging with Morgan
* CORS support
* Environment variable configuration
* Persistent access logs

---

## Tech Stack

* Node.js
* Express.js
* MongoDB Atlas
* Mongoose
* Morgan
* Body Parser

---

## Project Structure

```text
.
├── app.js
├── models/
│   └── goal.js
├── logs/
│   └── access.log
├── .env
├── package.json
└── README.md
```

---

## Installation

### Clone the repository

```bash
git clone <repository-url>
cd micro-svc-goals-backend
```

### Install dependencies

```bash
npm install
```

---

## Environment Variables

Create a `.env` file in the project root.

```env
DATABASE_USERNAME=admin
DATABASE_PASSWORD=your_password
DATABASE_URL=cluster0.xxxxx.mongodb.net
DATABASE_NAME=goalsdb
```

### Variable Description

| Variable          | Description               |
| ----------------- | ------------------------- |
| DATABASE_USERNAME | MongoDB database username |
| DATABASE_PASSWORD | MongoDB database password |
| DATABASE_URL      | MongoDB Atlas cluster URL |
| DATABASE_NAME     | Database name             |

---

## Running the Application

### Development

```bash
npm start
```

The server starts after a successful database connection.

Default port:

```text
5001
```

Base URL:

```text
http://localhost:5001
```

---

## Database Connection

The application connects to MongoDB Atlas using:

```javascript
mongodb+srv://<username>:<password>@<cluster>/<database>?authSource=admin
```

Connection is established during application startup. If the connection fails, the application exits with a non-zero status code.

---

## API Endpoints

### Get All Goals

**Request**

```http
GET /goals
```

**Response**

```json
{
  "goals": [
    {
      "id": "64f0a1d0c1234567890abcd",
      "text": "Learn Docker"
    },
    {
      "id": "64f0a1d0c1234567890abce",
      "text": "Deploy to AWS"
    }
  ]
}
```

**Status Codes**

| Code | Description                  |
| ---- | ---------------------------- |
| 200  | Goals retrieved successfully |
| 500  | Server error                 |

---

### Create Goal

**Request**

```http
POST /goals
Content-Type: application/json
```

Request Body:

```json
{
  "text": "Learn Kubernetes"
}
```

**Successful Response**

```json
{
  "message": "Goal saved",
  "goal": {
    "id": "64f0a1d0c1234567890abcf",
    "text": "Learn Kubernetes"
  }
}
```

**Status Codes**

| Code | Description       |
| ---- | ----------------- |
| 201  | Goal created      |
| 422  | Invalid goal text |
| 500  | Server error      |

---

### Delete Goal

**Request**

```http
DELETE /goals/:id
```

Example:

```http
DELETE /goals/64f0a1d0c1234567890abcf
```

**Response**

```json
{
  "message": "Deleted goal!"
}
```

**Status Codes**

| Code | Description  |
| ---- | ------------ |
| 200  | Goal deleted |
| 500  | Server error |

---

## CORS Configuration

The API allows requests from any origin.

Allowed methods:

```text
GET
POST
DELETE
OPTIONS
```

Allowed headers:

```text
Content-Type
```

---

## Logging

Morgan is configured to write access logs to:

```text
logs/access.log
```

Example log entry:

```text
::1 - - [21/Jun/2026:15:45:22 +0000] "GET /goals HTTP/1.1" 200 124
```

### Ignore Log File in Git

Add the following to `.gitignore`:

```gitignore
logs/access.log
```

Optionally keep the directory using:

```text
logs/.gitkeep
```

---

## Example cURL Requests

### Create Goal

```bash
curl -X POST http://localhost:5001/goals -H "Content-Type: application/json" -d '{"text":"Learn AWS"}'
```

### Get Goals

```bash
curl http://localhost:5001/goals
```

### Delete Goal

```bash
curl -X DELETE http://localhost:5001/goals/<goal-id>
```

---

## Future Improvements

* Environment-based server port configuration
* Input validation middleware
* Authentication and authorization
* Pagination for goals
* Docker support
* Unit and integration tests
* API documentation with Swagger/OpenAPI

---

## License

ISC License

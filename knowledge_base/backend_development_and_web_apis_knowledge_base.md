# 07. Backend Development and Web APIs Knowledge Base

Welcome to the ultimate guide on backend development and web APIs! This knowledge base is designed for students, developers, and your Web Development Tutor RAG Chatbot. It takes you from absolute beginner to advanced foundational level using clear, simple English and practical examples.

---

## 1. What Backend Development Is vs. Frontend Development

- **Frontend (Client-Side):** Everything the user sees and interacts with directly in their browser or mobile app. Built with HTML, CSS, and JavaScript. It handles layouts, animations, user input collection, and immediate visual feedback.
- **Backend (Server-Side):** The "engine room" hidden behind the scenes. It runs on remote servers and handles business logic, database management, user authentication, security, and integration with third-party services.
- **Analogy:** Think of a restaurant. The **frontend** is the dining room, menus, and waiters where customers interact. The **backend** is the kitchen, inventory room, and chefs preparing orders out of sight.

---

## 2. Client-Server Architecture & Request-Response Communication

- **Client:** Any device or software (like a web browser, mobile app, or cURL command) that requests information or services.
- **Server:** A powerful computer connected to the internet that listens for requests, processes them, and sends back responses.
- **The Request-Response Cycle:**
  1. The client sends an HTTP Request (e.g., "Give me user profile #42").
  2. The server receives the request, processes it (talks to a database, runs checks), and generates an HTTP Response.
  3. The server sends back the response (e.g., status `200 OK` with JSON data containing user #42's details).

---

## 3. Servers, Hosting, Domains, DNS, Ports, HTTPS, and Deployment

- **Servers & Hosting:** A server is a computer running 24/7. Hosting refers to renting space on cloud providers (like AWS, Render, Heroku, or DigitalOcean) to run your backend application.
- **Domains & DNS:** Domain Name System (DNS) acts as the phonebook of the internet, translating human-friendly names (e.g., `example.com`) into computer-friendly IP addresses (e.g., `192.0.2.1`).
- **Ports:** A server can run multiple applications. Ports are virtual numbered doors (like port `80` for HTTP, `443` for HTTPS, or `3000` for local Node.js apps) that route incoming traffic to the correct application.
- **HTTPS & Deployment:** HTTPS encrypts data in transit using TLS/SSL certificates. Deployment is the process of moving your code from your local development machine to a live cloud server.

---

## 4. HTTP Fundamentals, Methods, Headers, Status Codes, and Bodies

HTTP (Hypertext Transfer Protocol) is the foundational protocol of the web.

- **Methods (Verbs):**
  - `GET`: Retrieve data.
  - `POST`: Create new data.
  - `PUT`: Replace an existing resource entirely.
  - `PATCH`: Update a resource partially.
  - `DELETE`: Remove a resource.
- **Headers:** Metadata sent with requests and responses (e.g., `Content-Type: application/json`, `Authorization: Bearer <token>`).
- **Status Codes:**
  - `200 OK`, `201 Created`: Success.
  - `400 Bad Request`, `401 Unauthorized`, `403 Forbidden`, `404 Not Found`: Client errors.
  - `500 Internal Server Error`, `502 Bad Gateway`: Server errors.
- **Request/Response Bodies:** The payload containing data (usually JSON) sent to or returned by the server.

---

## 5. REST APIs, REST Principles, Endpoints, Resources, and JSON

REST (Representational State Transfer) is an architectural style for designing networked applications.

- **Core Principles:**
  - **Statelessness:** Each request from client to server must contain all the information necessary to understand and process the request.
  - **Client-Server Separation:** Frontend and backend evolve independently.
  - **Uniform Interface:** Standardized use of HTTP methods and URIs.
- **Resources & Endpoints:** Resources are nouns (e.g., `/users`, `/products`). Endpoints are specific URLs where APIs can be accessed (e.g., `https://api.example.com/v1/products`).
- **JSON (JavaScript Object Notation):** The lightweight data-interchange format used universally in modern APIs.

---

## 6. CRUD Operations and Mapping to HTTP Methods

CRUD stands for Create, Read, Update, and Delete.

| Operation | HTTP Method | Example Endpoint | Description |
| :--- | :--- | :--- | :--- |
| **Create** | `POST` | `/api/posts` | Create a new post |
| **Read** | `GET` | `/api/posts` or `/api/posts/:id` | Retrieve all posts or one specific post |
| **Update** | `PUT` or `PATCH` | `/api/posts/:id` | Modify an existing post |
| **Delete** | `DELETE` | `/api/posts/:id` | Delete a post |

---

## 7. API Design: Naming Conventions, Filtering, Sorting, Pagination, Versioning

- **Naming Conventions:** Use plural nouns for resources (e.g., `/users`, not `/getUser`). Keep URIs lowercase with hyphens for multi-word paths (`/order-items`).
- **Filtering, Sorting, and Pagination:**
  - Filtering: `/api/products?category=electronics`
  - Sorting: `/api/products?sort=price_asc`
  - Pagination: `/api/products?page=2&limit=10`
- **Versioning:** Always version your API to prevent breaking existing clients (e.g., `/api/v1/users`).

---

## 8. Using JavaScript Fetch to Call APIs

The `fetch` API allows frontend JavaScript or Node.js clients to communicate with servers asynchronously.

```javascript
async function fetchUserData(userId) {
  try {
    const response = await fetch(`https://api.example.com/v1/users/${userId}`, {
      method: 'GET',
      headers: {
        'Content-Type': 'application/json',
        'Authorization': 'Bearer YOUR_TOKEN_HERE'
      }
    });

    if (!response.ok) {
      throw new Error(`HTTP error! Status: ${response.status}`);
    }

    const data = await response.json();
    console.log('User data:', data);
  } catch (error) {
    console.error('Failed to fetch user:', error.message);
  }
}
```

---

## 9. Building Simple APIs Conceptually & Node.js Basics

Node.js allows developers to execute JavaScript outside the browser using the V8 engine.
- **npm (Node Package Manager):** The ecosystem for installing community packages.
- **Modules:** CommonJS (`require()`) or ES Modules (`import/export`) for organizing code into reusable files.
- **Environment Configuration:** Keeping secrets and configuration variables in `.env` files using `dotenv`.

---

## 10. Express Fundamentals: Routes, Middleware, Controllers, and Error Handling

Express is a fast, minimalist web framework for Node.js.

### Practical Example: Simple Express Server & CRUD Endpoints
Here is a complete, educational example demonstrating an Express server with CRUD endpoints, request validation, and centralized error handling.

```javascript
// server.js
const express = require('express');
const app = express();

// Middleware to parse incoming JSON request bodies
app.use(express.json());

// In-memory database mock (Basic CRUD design with example data)
let todos = [
  { id: 1, title: 'Learn Node.js', completed: false },
  { id: 2, title: 'Master Express APIs', completed: false }
];

// --- Validation Middleware ---
const validateTodo = (req, res, next) => {
  const { title } = req.body;
  if (!title || typeof title !== 'string' || title.trim() === '') {
    const error = new Error('Validation Error: Title is required and must be a non-empty string.');
    error.status = 400;
    return next(error);
  }
  // Sanitize input
  req.body.title = title.trim();
  next();
};

// --- Routes & Controllers ---

// GET: Retrieve all todos
app.get('/api/todos', (req, res, next) => {
  res.json({ success: true, count: todos.length, data: todos });
});

// GET: Retrieve a single todo by ID
app.get('/api/todos/:id', (req, res, next) => {
  const todoId = parseInt(req.params.id, 10);
  const todo = todos.find(t => t.id === todoId);
  
  if (!todo) {
    const error = new Error('Todo not found.');
    error.status = 404;
    return next(error);
  }
  
  res.json({ success: true, data: todo });
});

// POST: Create a new todo
app.post('/api/todos', validateTodo, (req, res, next) => {
  const newTodo = {
    id: todos.length > 0 ? todos[todos.length - 1].id + 1 : 1,
    title: req.body.title,
    completed: false
  };
  
  todos.push(newTodo);
  res.status(201).json({ success: true, data: newTodo });
});

// PUT: Update an existing todo
app.put('/api/todos/:id', validateTodo, (req, res, next) => {
  const todoId = parseInt(req.params.id, 10);
  const todoIndex = todos.findIndex(t => t.id === todoId);
  
  if (todoIndex === -1) {
    const error = new Error('Todo not found.');
    error.status = 404;
    return next(error);
  }
  
  todos[todoIndex] = {
    id: todoId,
    title: req.body.title,
    completed: req.body.completed !== undefined ? Boolean(req.body.completed) : todos[todoIndex].completed
  };
  
  res.json({ success: true, data: todos[todoIndex] });
});

// DELETE: Remove a todo
app.delete('/api/todos/:id', (req, res, next) => {
  const todoId = parseInt(req.params.id, 10);
  const todoIndex = todos.findIndex(t => t.id === todoId);
  
  if (todoIndex === -1) {
    const error = new Error('Todo not found.');
    error.status = 404;
    return next(error);
  }
  
  const deletedTodo = todos.splice(todoIndex, 1);
  res.json({ success: true, message: 'Todo deleted successfully', data: deletedTodo[0] });
});

// --- Centralized Error Handling Middleware ---
app.use((err, req, res, next) => {
  const statusCode = err.status || 500;
  res.status(statusCode).json({
    success: false,
    error: {
      status: statusCode,
      message: err.message || 'Internal Server Error'
    }
  });
});

// Start Server
const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`);
});
```

*Production Note:* In production applications, replace in-memory arrays with persistent databases (like PostgreSQL or MongoDB) and implement robust validation libraries like `express-validator` or `Zod`.

---

## 11. Request Validation, Input Sanitization, and Structured API Errors

- **Validation:** Checking if incoming data meets business and structural rules (e.g., valid email format, password length).
- **Sanitization:** Cleaning input data to strip malicious code (e.g., removing HTML tags to prevent XSS).
- **Structured Errors:** Always return consistent error JSON shapes across all endpoints so clients can parse them easily.

---

## 12. Databases: Relational vs. NoSQL, Tables, Documents, Queries, Data Modeling

- **Relational Databases (SQL - e.g., PostgreSQL, MySQL):** Data is stored in strict tables with rows and columns. Uses SQL (Structured Query Language). Ideal for structured data with complex relationships.
- **NoSQL Databases (e.g., MongoDB, Redis):** Data is stored as flexible documents (JSON-like) or key-value pairs. Ideal for rapid prototyping and unstructured or semi-structured data.
- **Data Modeling:** Designing schemas to optimize read and write performance while avoiding data duplication.

---

## 13. Database Connection Concepts and Safe Handling of Credentials

- **Connection Pooling:** Managing a reusable pool of database connections to handle heavy concurrent traffic efficiently.
- **Safe Credentials:** Never hardcode database passwords or API keys in source code. Always load them from environment variables (`process.env.DB_PASSWORD`) and add `.env` to your `.gitignore` file.

---

## 14. Authentication vs. Authorization

- **Authentication (AuthN):** Verifying *who* a user is (e.g., "Are you John Doe?"). Login credentials confirm identity.
- **Authorization (AuthZ):** Determining *what* an authenticated user is allowed to do (e.g., "Can John edit this post?"). Permissions and roles control access.

---

## 15. Password Hashing, Sessions, Cookies, Tokens, and MFA

- **Password Hashing:** Never store plain-text passwords. Use cryptographic hashing algorithms with salts (e.g., `bcrypt` or `argon2`) to secure passwords.
- **Sessions & Cookies:** Server stores session state; browser stores a session ID cookie.
- **Tokens (JWT - JSON Web Tokens):** Stateless tokens signed by the server, passed in headers (`Authorization: Bearer <token>`).
- **MFA (Multi-Factor Authentication):** Requiring two or more verification factors (e.g., password + SMS/TOTP authenticator code).

---

## 16. API Keys, OAuth Concepts, Secret Management, and Rate Limiting

- **API Keys:** Simple tokens passed by clients to identify the calling application or track usage.
- **OAuth 2.0:** An industry-standard protocol for token-based authorization (e.g., "Sign in with Google" or "Sign in with GitHub").
- **Secret Management:** Using vault services (AWS Secrets Manager, HashiCorp Vault) in production to rotate and protect credentials.
- **Rate Limiting:** Restricting the number of requests a client can make within a given time window (e.g., 100 requests per 15 minutes) to prevent abuse and Denial of Service (DoS) attacks.

---

## 17. CORS (Cross-Origin Resource Sharing)

- **What it is:** A security mechanism implemented by browsers that restricts web pages from making requests to a different domain than the one that served the web page.
- **Why it exists:** Prevents malicious websites from reading sensitive data from another site on behalf of an authenticated user (CSRF-related protection).
- **Common Mistakes:** Using wildcard `Access-Control-Allow-Origin: *` blindly with credentials enabled, or failing to configure allowed methods and headers correctly.

---

## 18. Common Web Vulnerabilities (OWASP Top 10 Concepts)

1. **SQL Injection (SQLi):** Attackers insert malicious SQL fragments into input fields. *Prevention:* Use parameterized queries or ORMs.
2. **XSS (Cross-Site Scripting):** Attackers inject malicious client-side scripts into web pages viewed by other users. *Prevention:* Sanitize and escape output.
3. **CSRF (Cross-Site Request Forgery):** Forcing an authenticated user to execute unwanted actions on a web application. *Prevention:* Use Anti-CSRF tokens and `SameSite` cookies.
4. **Broken Access Control:** Users acting outside their permission levels. *Prevention:* Implement robust server-side authorization checks on every endpoint.
5. **Insecure Configuration:** Leaving default passwords, debug mode enabled, or exposed error stack traces in production.

---

## 19. Production Hardening: HTTPS, Secure Cookies, Least Privilege, Logging

- **HTTPS Everywhere:** Encrypt all web traffic.
- **Secure & HttpOnly Cookies:** Prevent JavaScript from reading sensitive session cookies (`HttpOnly`) and ensure cookies are only transmitted over HTTPS (`Secure`).
- **Least Privilege Principle:** Give database users and application processes only the minimum permissions necessary to function.
- **Safe Error Messages:** Never leak internal stack traces, database schema details, or server paths to end users in error responses. Log details securely on the server instead.

---

## 20. API Documentation, OpenAPI, Testing, and Debugging

- **Documentation:** Clear guides for API consumers using tools like Postman, Swagger, or ReadMe.
- **OpenAPI Specification (OAS):** Standard format for describing REST APIs in YAML or JSON.
- **Testing:** Writing unit and integration tests using frameworks like Jest, Supertest, or Mocha.
- **Debugging:** Using structured logging libraries (e.g., Winston, Pino) and debugging tools.

---

## 21. Webhooks vs. Ordinary API Requests

- **Ordinary API Request (Polling):** The client constantly asks the server, "Is there new data yet?"
- **Webhook (Reverse API):** An event-driven notification. When an event occurs on a server (e.g., a payment succeeds), the server makes an HTTP POST request to a pre-configured URL provided by the client.

---

## 22. File Uploads, Size Limits, Validation, and Storage

- **Request Size Limits:** Configure body parsers (e.g., multer or express limits) to reject oversized payloads to prevent memory exhaustion.
- **File Type Validation:** Verify file magic numbers/extensions rather than trusting client headers alone.
- **Safe Storage:** Never store uploaded files directly in the web server's local public directory. Upload them to secure cloud object storage (e.g., AWS S3, Google Cloud Storage) with randomized filenames.

---

## 23. Deployment, Environment Variables, Logs, Monitoring, and Production Considerations

- **Environment Variables:** Configuration separated from code (`NODE_ENV=production`).
- **Process Managers:** Using PM2, Docker, or Kubernetes to ensure server auto-restart on crashes.
- **Monitoring & Logging:** Real-time uptime tracking, error tracking (e.g., Sentry), and performance metrics.

---

## 24. Performance, Caching, Pagination, and Efficient Queries

- **Caching:** Storing frequently accessed data in memory using Redis or Memcached to reduce database load.
- **Efficient Queries:** Adding database indexes to foreign keys and frequently searched columns to avoid full-table scans.
- **Pagination:** Always paginate large database result sets (`LIMIT` and `OFFSET` or cursor-based pagination).

---

## 25. Common API Errors and Troubleshooting

- **504 Gateway Timeout:** Server took too long to respond (check slow database queries or external API calls).
- **429 Too Many Requests:** Client exceeded rate limits.
- **CORS Errors:** Browser blocked response due to missing CORS headers.

---

## 26. When to Choose Node.js, Python, or Another Backend Technology

- **Node.js (JavaScript/TypeScript):** Best for real-time apps (chat, streaming), API gateways, and full-stack JavaScript teams.
- **Python (Django / FastAPI / Flask):** Best for AI/ML integration, data science, rapid prototyping, and structured enterprise apps.
- **Go / Java / C#:** Best for high-performance microservices, enterprise-grade security, and heavy concurrent workloads.

---

## 27. Glossary

- **API:** Application Programming Interface.
- **CRUD:** Create, Read, Update, Delete.
- **Endpoint:** A specific URL where an API resource can be accessed.
- **JWT:** JSON Web Token.
- **Middleware:** Functions that execute during the lifecycle of an HTTP request in Express.
- **NoSQL:** Non-relational database.
- **Payload:** The data carried within an HTTP request or response body.
- **Rate Limiting:** Throttling client requests over time.
- **REST:** Representational State Transfer.
- **SQL:** Structured Query Language.
- **Stateless:** A server design where each request is processed independently without retaining session state across requests.
- **Webhook:** An automated HTTP callback triggered by specific server events.

---

## 28. Interview Questions & Answers

1. **Q: What is the difference between frontend and backend development?**  
   **A:** Frontend is what users see and interact with in their browser (HTML, CSS, JS). Backend handles server-side logic, databases, security, and APIs behind the scenes.
2. **Q: What is REST and what are its core principles?**  
   **A:** REST is an architectural style for APIs. Core principles include statelessness, client-server separation, uniform interface, and cacheability.
3. **Q: What does HTTP status code 401 mean compared to 403?**  
   **A:** 401 Unauthorized means the user is not authenticated (needs to log in). 403 Forbidden means the user is authenticated but lacks permission to access the resource.
4. **Q: Why should you never store plain-text passwords in a database?**  
   **A:** If the database is breached, attacker accounts are immediately compromised. Passwords must be hashed using strong algorithms like bcrypt or argon2 with salts.
5. **Q: What is CORS and why does it exist?**  
   **A:** Cross-Origin Resource Sharing is a browser security mechanism that restricts web pages from requesting resources from a different domain, preventing malicious sites from reading sensitive data.
6. **Q: Explain the difference between `PUT` and `PATCH`.**  
   **A:** `PUT` replaces an entire resource with new data, whereas `PATCH` applies partial updates to an existing resource.
7. **Q: What is middleware in Express.js?**  
   **A:** Functions that have access to the request object (`req`), response object (`res`), and `next` middleware function in the application's request-response cycle.
8. **Q: What is SQL Injection and how do you prevent it?**  
   **A:** SQL Injection occurs when malicious SQL statements are inserted into input fields. Prevent it by using parameterized queries, prepared statements, or ORMs.
9. **Q: What is the purpose of environment variables?**  
   **A:** To keep sensitive configuration data (database passwords, API keys) and environment-specific settings out of source code.
10. **Q: What is a JWT and how does it work?**  
    **A:** A JSON Web Token is a compact, URL-safe means of representing claims to be transferred between two parties. The server signs the token upon login, and the client sends it in the `Authorization` header for subsequent requests.
11. **Q: What is the difference between SQL and NoSQL databases?**  
    **A:** SQL databases are relational, structured in tables with predefined schemas. NoSQL databases are non-relational, storing flexible documents or key-value pairs.
12. **Q: What is rate limiting?**  
    **A:** A technique that restricts the number of requests a client can make to an API within a specified timeframe to prevent abuse.
13. **Q: What is connection pooling in database management?**  
    **A:** Maintaining a cache of database connections so that connections can be reused rather than opened and closed for every single request.
14. **Q: What is a webhook?**  
    **A:** An event-driven HTTP callback where a server sends an automated POST request to a client URL when a specific event occurs.
15. **Q: Why should error stack traces not be sent to clients in production?**  
    **A:** They reveal internal server paths, dependency versions, and database architectures that attackers can exploit.
16. **Q: What is database indexing and why is it important?**  
    **A:** Data structures (like B-trees) created on database columns to speed up data retrieval operations at the cost of slower writes.
17. **Q: What is authentication versus authorization?**  
    **A:** Authentication verifies who you are; authorization determines what you are allowed to do.
18. **Q: What is the Node.js event loop?**  
    **A:** A mechanism that allows Node.js to perform non-blocking I/O operations despite JavaScript being single-threaded, by offloading operations to the system kernel.
19. **Q: What is API versioning and why is it necessary?**  
    **A:** Managing changes to API endpoints (e.g., `/api/v1/`) to ensure existing client applications do not break when backend updates occur.
20. **Q: What is input sanitization?**  
    **A:** Cleaning and filtering incoming data to remove malicious characters or scripts (like HTML tags) before processing or storing it.
21. **Q: What is the purpose of pagination in APIs?**  
    **A:** To break large datasets into smaller chunks (pages), reducing memory consumption, bandwidth, and response times.
22. **Q: What does `HttpOnly` cookie flag do?**  
    **A:** It prevents client-side JavaScript from accessing the cookie via `document.cookie`, mitigating XSS credential theft.
23. **Q: What is an OpenAPI specification?**  
    **A:** A standard specification format for describing, producing, and consuming RESTful APIs.
24. **Q: When should you choose Node.js over Python for backend?**  
    **A:** When building real-time applications (WebSockets/chat), fast API gateways, or when the team wants to use JavaScript across the full stack.
25. **Q: What is a reverse proxy and what role does it play?**  
    **A:** A server (like Nginx or Caddy) that sits in front of backend web servers, handling incoming client requests, SSL termination, caching, and load balancing.

---

## 29. Multiple Choice Questions (MCQs)

1. **What does REST stand for?**  
   A) Remote Execution Standard Transfer  
   B) Representational State Transfer  
   C) Resource State Transmission  
   D) Rapid Express Server Technology  

2. **Which HTTP method is idempotent and used to retrieve resources?**  
   A) POST  
   B) PUT  
   C) GET  
   D) PATCH  

3. **What status code indicates successful creation of a resource?**  
   A) 200 OK  
   B) 201 Created  
   C) 204 No Content  
   D) 301 Moved Permanently  

4. **Which module in Node.js is commonly used to build web servers easily?**  
   A) http  
   B) express  
   C) path  
   D) fs  

5. **What vulnerability does parameterized queries prevent?**  
   A) XSS  
   B) CSRF  
   C) SQL Injection  
   D) Buffer Overflow  

6. **What is the primary difference between Authentication and Authorization?**  
   A) AuthN is passwords; AuthZ is usernames.  
   B) AuthN verifies identity; AuthZ verifies permissions.  
   C) AuthN is client-side; AuthZ is server-side.  
   D) There is no difference.  

7. **Which HTTP status code represents an Unauthorized error?**  
   A) 400  
   B) 401  
   C) 403  
   D) 404  

8. **What is the purpose of CORS?**  
   A) Speed up database queries  
   B) Encrypt HTTPS traffic  
   C) Restrict cross-origin browser requests for security  
   D) Compress JSON responses  

9. **Which hashing algorithm should be used for user passwords?**  
   A) MD5  
   B) SHA-1  
   C) Bcrypt or Argon2  
   D) Base64  

10. **What is a webhook?**  
    A) A database query optimizer  
    B) An event-driven HTTP POST callback to a client URL  
    C) A frontend testing library  
    D) An SSL certificate manager  

11. **Which database type is MongoDB?**  
    A) Relational SQL  
    B) NoSQL Document  
    C) Key-Value cache only  
    D) Graph database  

12. **What does the `HttpOnly` cookie flag protect against?**  
    A) SQL Injection  
    B) CSRF  
    C) XSS cookie theft via JavaScript  
    D) Man-in-the-middle sniffing  

13. **How should environment secrets be stored in Node.js?**  
    A) Hardcoded in `app.js`  
    B) Committed to Git in a config file  
    C) In environment variables via `.env`  
    D) In browser local storage  

14. **What does API pagination help with?**  
    A) Database connection pooling  
    B) Preventing server overload with large datasets  
    C) Encrypting request bodies  
    D) Setting CORS headers  

15. **Which HTTP method is intended to replace an entire resource?**  
    A) PATCH  
    B) GET  
    C) PUT  
    D) DELETE  

16. **What is the role of a reverse proxy like Nginx?**  
    A) Compile JavaScript code  
    B) Handle SSL termination and load balancing in front of backend servers  
    C) Store database records  
    D) Validate frontend forms  

17. **What is the function of middleware in Express?**  
    A) Connect to MongoDB  
    B) Intercept requests and responses to execute logic  
    C) Minify HTML files  
    D) Generate JWT secrets  

18. **Which error status code family represents server-side errors?**  
    A) 2xx  
    B) 3xx  
    C) 4xx  
    D) 5xx  

19. **What is input sanitization?**  
    A) Encrypting passwords with bcrypt  
    B) Cleaning incoming data to strip malicious markup or scripts  
    C) Converting JSON to XML  
    D) Checking user roles  

20. **What is rate limiting used for?**  
    A) Speeding up API responses  
    B) Preventing brute-force attacks and API abuse  
    C) Formatting JSON responses  
    D) Managing database migrations  

21. **Which tool is standard for testing Express API endpoints?**  
    A) React Router  
    B) Jest and Supertest  
    C) Webpack  
    D) Babel  

22. **What does JWT stand for?**  
    A) JavaScript Web Transfer  
    B) JSON Web Token  
    C) Java Web Terminal  
    D) Json Wireless Transmission  

23. **What is database indexing?**  
    A) Deleting old records automatically  
    B) Creating data structures to speed up queries  
    C) Backing up tables to the cloud  
    D) Joining multiple tables together  

24. **Why are database connection pools used?**  
    A) To avoid opening/closing new database connections for every request  
    B) To encrypt database credentials  
    C) To prevent SQL injection  
    D) To cache API responses  

25. **When should you choose Node.js for backend development?**  
    A) For heavy machine learning and matrix calculations  
    B) For real-time applications and full-stack JavaScript teams  
    C) Only when Python is unavailable  
    D) For legacy mainframe systems  

### MCQ Answer Key
1. B | 2. C | 3. B | 4. B | 5. C  
6. B | 7. B | 8. C | 9. C | 10. B  
11. B | 12. C | 13. C | 14. B | 15. C  
16. B | 17. B | 18. D | 19. B | 20. B  
21. B | 22. B | 23. B | 24. A | 25. B  

---

## 30. Backend & API Projects (Beginner to Advanced)

1. **Project 1: Personal Task Manager API (Beginner)**  
   - *Description:* Build a REST API with Node.js and Express to manage tasks (CRUD). Use in-memory storage or a simple JSON file. Implement basic validation and error handling.
   - *Skills Learned:* Express setup, routing, request methods, status codes, JSON responses.

2. **Project 2: Blog Platform with Relational Database (Intermediate)**  
   - *Description:* Create a backend for a blog where users can register, log in, create posts, and leave comments. Use PostgreSQL with parameterized queries or an ORM (Prisma/Sequelize).
   - *Skills Learned:* Relational database modeling, password hashing (bcrypt), JWT authentication, and authorization middleware.

3. **Project 3: Secure E-Commerce API with Stripe Webhooks (Advanced)**  
   - *Description:* Build a robust e-commerce product and order API featuring rate limiting, input sanitization, product filtering/pagination, and webhook integration for payment processing (Stripe).
   - *Skills Learned:* Webhooks, payment gateway integration, advanced security headers, rate limiting, and structured error logging.

4. **Project 4: Real-Time Chat Server with WebSockets (Advanced)**  
   - *Description:* Build a real-time messaging backend using Node.js, Express, and Socket.io. Authenticate connections via JWT and broadcast messages to chat rooms.
   - *Skills Learned:* WebSockets, persistent real-time connections, event-driven architecture, and state management.

5. **Project 5: Microservices API Gateway with Caching (Expert)**  
   - *Description:* Build an API gateway that routes traffic to multiple microservices, implements Redis caching for popular endpoints, handles centralized authentication, and uses containerization (Docker).
   - *Skills Learned:* Reverse proxying, Redis caching, microservices architecture, Dockerization, and production monitoring.
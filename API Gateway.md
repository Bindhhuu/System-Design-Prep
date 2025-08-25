# API Design for System Design Interviews

## What is an API?
- **API (Application Programming Interface)** is a set of rules and contracts that allow different software components to communicate.
- Acts as a bridge between client and server, or between services.
- Can be RESTful APIs, GraphQL APIs, gRPC APIs, WebSocket APIs, etc.

---

## How to Design an API
1. **Identify Use Cases**
   - Define what problems the API should solve.
   - Understand client needs (mobile app, web app, 3rd party).

2. **Define Resources & Endpoints**
   - For REST, map domain objects to resources (`/users`, `/orders`).
   - For GraphQL, define schemas and resolvers.

3. **Decide Data Format**
   - Common: JSON, XML, Protobuf.
   - Keep it consistent.

4. **Authentication & Authorization**
   - API keys, OAuth2, JWT, or custom tokens.
   - Role-based or scope-based access control.

5. **Error Handling**
   - Use standard HTTP status codes (e.g., 200 OK, 400 Bad Request, 404 Not Found, 500 Internal Server Error).
   - Provide clear error messages with error codes.

6. **Versioning**
   - Support backward compatibility.
   - Common styles: URI (`/v1/users`), headers (`Accept: application/vnd.company.v1+json`).

7. **Rate Limiting & Throttling**
   - Prevent abuse and ensure fairness.
   - Example: 100 requests/minute per API key.

8. **Documentation**
   - Use tools like Swagger/OpenAPI or Postman collections.
   - Include request/response examples.

9. **Monitoring & Logging**
   - Collect metrics like latency, error rates.
   - Enable debugging through correlation IDs.

---

## Characteristics of a Good API
✅ **Consistency**
- Naming conventions and structure are predictable.
- Example: always use plural nouns (`/users`, `/orders`).

✅ **Simplicity**
- Intuitive endpoints, easy to use without deep docs.

✅ **Scalability**
- Designed to handle growth (pagination, filtering, async operations).

✅ **Security**
- Uses HTTPS, authentication, authorization, input validation.

✅ **Extensibility**
- Versioning, allows future growth without breaking clients.

✅ **Idempotency**
- Safe methods like `GET`, and idempotent `PUT`/`DELETE`.

---

## Characteristics of a Bad API
❌ **Inconsistent Naming**
- `/getUser` in one place, `/users` in another.

❌ **Overloaded Endpoints**
- One endpoint doing too many things (`/doEverything`).

❌ **Poor Error Messages**
- Returning `500` for everything, no meaningful error body.

❌ **No Versioning**
- Breaking existing clients when changes are made.

❌ **Lack of Security**
- No HTTPS, no auth, or weak API keys.

❌ **Unscalable**
- Returning massive datasets without pagination.



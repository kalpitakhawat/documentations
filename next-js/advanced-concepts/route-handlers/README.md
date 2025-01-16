# Route Handlers in Next.js

## Overview

Route Handlers in Next.js, introduced with the App Router, provide a powerful way to create custom backend logic directly within your Next.js application. These handlers simplify building APIs and server-side logic without needing an external server. Each `route.js` file maps to an API endpoint and supports different HTTP methods like `GET`, `POST`, `PUT`, and `DELETE`.

---

## Defining Route Handlers

Route Handlers are defined in the `app/api` directory. Each file corresponds to a specific API endpoint and handles HTTP methods through exported functions.

### Example Directory Structure

```plaintext
app/
├── api/
│   ├── hello/
│   │   └── route.js       // Endpoint: /api/hello
│   ├── user/
│   │   ├── [id]/
│   │   │   └── route.js   // Endpoint: /api/user/:id
│   │   └── route.js       // Endpoint: /api/user
```

---

## Basic Route Handler Example

```javascript
// app/api/hello/route.js
export async function GET(request) {
  return new Response('Hello, World!', {
    status: 200,
    headers: {
      'Content-Type': 'text/plain',
    },
  });
}
```

- **Endpoint**: `/api/hello`
- **Method**: `GET`
- **Response**: `Hello, World!`

---

## Handling Multiple HTTP Methods

You can define different functions for each HTTP method within the same `route.js` file.

### Example

```javascript
// app/api/user/route.js
export async function GET(request) {
  return new Response(JSON.stringify({ message: 'Fetched user data' }), {
    status: 200,
    headers: { 'Content-Type': 'application/json' },
  });
}

export async function POST(request) {
  const body = await request.json();
  return new Response(JSON.stringify({ message: 'User created', data: body }), {
    status: 201,
    headers: { 'Content-Type': 'application/json' },
  });
}
```

- **GET `/api/user`**: Fetches user data.
- **POST `/api/user`**: Creates a new user.

---

## Dynamic Route Handlers

Dynamic routes allow creating endpoints with parameters by using square brackets (`[param]`) in the directory structure.

### Example: Dynamic Route

```plaintext
app/
├── api/
│   └── user/
│       └── [id]/
│           └── route.js  // Endpoint: /api/user/:id
```

```javascript
// app/api/user/[id]/route.js
export async function GET(request, { params }) {
  const { id } = params;
  return new Response(JSON.stringify({ message: `User ID: ${id}` }), {
    status: 200,
    headers: { 'Content-Type': 'application/json' },
  });
}
```

- **Endpoint**: `/api/user/:id`
- **Example Request**: `/api/user/123`
- **Response**: `{ "message": "User ID: 123" }`

---

## Streaming Responses

Route Handlers can send incremental data to the client using streaming responses. This is useful for real-time updates or handling large datasets.

### Example: Streaming Data

```javascript
// app/api/stream/route.js
export async function GET() {
  const stream = new ReadableStream({
    start(controller) {
      controller.enqueue('Part 1\n');
      controller.enqueue('Part 2\n');
      controller.close();
    },
  });

  return new Response(stream, {
    headers: {
      'Content-Type': 'text/plain',
    },
  });
}
```

- **Endpoint**: `/api/stream`
- **Response**:
  ```plaintext
  Part 1
  Part 2
  ```

---

## Best Practices

1. **Input Validation**:
   - Validate and sanitize user input to prevent security issues.
   ```javascript
   export async function POST(request) {
     try {
       const data = await request.json();
       if (!data.name) throw new Error('Name is required');
       return new Response(JSON.stringify({ message: 'User created', data }), {
         status: 201,
       });
     } catch (error) {
       return new Response(JSON.stringify({ error: error.message }), {
         status: 400,
       });
     }
   }
   ```

2. **Error Handling**:
   - Use `try-catch` blocks to handle exceptions gracefully.

3. **Efficient Data Fetching**:
   - Avoid fetching unnecessary data or performing expensive computations in handlers.

4. **Dynamic Routes**:
   - Use meaningful parameter names in dynamic routes for better readability.

5. **Testing**:
   - Test endpoints using tools like Postman or curl to ensure correctness.

6. **Set Proper Headers**:
   - Always specify appropriate headers like `Content-Type`.

---

## Conclusion

Route Handlers in Next.js provide a seamless way to integrate backend logic within your application. By leveraging features like dynamic routes, streaming responses, and multi-method support, you can build robust APIs tailored to your needs.

## Official Documentation

- [Route Handlers](https://nextjs.org/docs/app/building-your-application/routing/route-handlers)


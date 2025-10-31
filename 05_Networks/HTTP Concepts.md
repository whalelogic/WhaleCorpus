# `🌀 Understanding HTTP concepts`

`Think of an HTTP request like mailing a package.`


`URL Path (/users/123): The street address on the package.`
 `HTTP Method (GET, POST): The delivery instruction (e.g., "Standard Delivery" or "Signature Required").`

`Headers: The labels on the outside of the box (From, To, Contents: Books, Fragile: Yes).`

`Body: The actual items inside the box (like a JSON payload).`
```

### The Anatomy of an HTTP Request

- A raw request sent from a client looks something like this: HTTP

```
`GET /posts/42?comments=true HTTP/1.1`
`Host: whalerapi.com`
`User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64)`
`Accept: application/json`
`Authorization: Bearer my-secret-auth-token`

`{`
 `"key": "This is the optional request body, often used with POST or PUT"`
`}`
```

Let's break down how Go gives you access to this information.

How Go Parses the Request 📝

Whether you use Go's standard library or a framework like Fiber, the request is parsed into an object that you can easily query in your handler.

Using the Standard net/http Library

In a standard Go handler, you get a pointer to an http.Request object (conventionally named r). Go

func myHandler(w http.ResponseWriter, r *http.Request) { // 1. Get the Method and Path method := r.Method // "GET" path := r.URL.Path // "/posts/42"

```
`// 2. Get Query Parameters`
`showComments := r.URL.Query().Get("comments") // "true"`

`// 3. Get Headers`
`// Use .Get() to read a specific header's value`
`userAgent := r.Header.Get("User-Agent")      // "Mozilla/5.0..."`
`authToken := r.Header.Get("Authorization")   // "Bearer my-secret-auth-token"`

`// You can also iterate through all headers`
`for name, values := range r.Header {`
    `// values is a slice of strings`
    `fmt.Printf("Header '%s': %s\n", name, values[0])`
`}`

`// 4. Read the Body (important for POST, PUT, PATCH)`
`body, err := io.ReadAll(r.Body)`
`if err != nil {`
    `// Handle error`
`}`
`// Now 'body' is a byte slice containing the JSON`
```

}

Using the Fiber Framework

In Fiber, you get a context object (*fiber.Ctx, conventionally named c), which provides convenient helper methods. Go

func myFiberHandler(c *fiber.Ctx) error { // 1. Get the Method and Path method := c.Method() // "GET" path := c.Path() // "/posts/42"

```
`// 2. Get Query Parameters`
`showComments := c.Query("comments") // "true"`

`// 3. Get Headers`
`// Use .Get() which is a convenient wrapper`
`userAgent := c.Get("User-Agent")    // "Mozilla/5.0..."`
`authToken := c.Get("Authorization") // "Bearer my-secret-auth-token"`

`// 4. Read the Body`
`body := c.Body() // Returns the body as a byte slice`

`// Fiber also has helpers to parse the body directly into a struct`
`var requestData MyStruct`
`if err := c.BodyParser(&requestData); err != nil {`
    `// Handle error`
`}`

`return c.SendString("Request parsed!")`
```

}

How to Use Headers to Create Better Code

Accessing headers allows you to build more robust, secure, and flexible applications. Here are the most common use cases:

1. Content-Type - Handling Different Data Formats

A client uses the Content-Type header to tell you what format the request body is in (e.g., application/json, application/x-www-form-urlencoded). You can check this header to decide how to parse the incoming data. Go

func createUser(c *fiber.Ctx) error { var user User

```
`// Check what kind of data the client sent`
`if c.Is("json") {`
    `// If it's JSON, parse it from the body`
    `if err := c.BodyParser(&user); err != nil {`
        `return c.Status(fiber.StatusBadRequest).SendString("Invalid JSON")`
    `}`
`} else {`
    `return c.Status(fiber.StatusUnsupportedMediaType).SendString("Content-Type must be application/json")`
`}`

`// ... save the user to the database ...`
`return c.Status(fiber.StatusCreated).JSON(user)`
```

}

2. Authorization - Securing Your Endpoints

This is the most common header for API security. A client sends a token (like a JWT or an API key), and you can write middleware to verify it before allowing the request to proceed. Go

import "strings"

func AuthMiddleware(c *fiber.Ctx) error { // Get the Authorization header authHeader := c.Get("Authorization")

```
`// Check if it's missing or doesn't start with "Bearer "`
`if authHeader == "" || !strings.HasPrefix(authHeader, "Bearer ") {`
    `return c.Status(fiber.StatusUnauthorized).SendString("Missing or malformed JWT")`
`}`

`// Get the token itself (everything after "Bearer ")`
`tokenString := strings.TrimPrefix(authHeader, "Bearer ")`

`// Here, you would validate the token (e.g., jwt.Parse())`
`if !isValid(tokenString) {`
    `return c.Status(fiber.StatusUnauthorized).SendString("Invalid JWT")`
`}`

`// If valid, proceed to the next handler in the chain`
`return c.Next()`
```

}

// You would apply this in your main app setup: // app.Use(AuthMiddleware)

3. Accept - Content Negotiation

The Accept header is how a client tells you what data format it wants back. For example, it might request application/json or application/xml. Your server can check this header and format the response accordingly. Go

func getUser(c *fiber.Ctx) error { user := GetUserFromDB() // Get user data

```
`// Check what format the client wants`
`switch c.Accepts("json", "xml") {`
`case "json":`
    `return c.JSON(user)`
`case "xml":`
    `return c.XML(user)`
`default:`
    `// Default to JSON if the client doesn't specify`
    `return c.JSON(user)`
`}`
```

}

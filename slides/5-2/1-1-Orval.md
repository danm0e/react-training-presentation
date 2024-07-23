# Orval

### What Is Orval

- "Resftul client generator".
- Generates API clients from OpenAPI/Swagger definitions, with appropriate type-signatures (TypeScript).

---

### The Problem It Solves

- Manually writing an API client and keeping it in sync with the client is monotomous, time consuming but essential to avoid any inconsistencies or bugs.

Note: When creating a web application that interacts with an API, it is common to use a client library or write an API client manually that abstracts the API calls. This allows you to focus on the front end of your application without worrying about the details of the API like request headers, query parameters, and response handling. With that in mind, it is essential to keep the API client in sync with the API itself to avoid any inconsistencies or bugs.
---

### What Are The Benefits

- Get all the types, request parameters, response schemas, and API endpoints automatically.
- Generate the API client from the API definition itself.
- Integrate the API client in our unit tests. Orval provides first class support for mocking through the Mock Service Worker library, and it can automatically generate the MSW handlers for testing server.

Note: The more complex your API becomes, the more beneficial it is to generate the API client from the API definition to avoid bugs, while keeping type safety and consistency in your API client.
---
### Demo Time

```
npm i orval axios 
```

---
### Setup your local script
```
//package.json
...
scripts: {
    ...
    "api:gen": "orval"
}
```

### Find an example

https://github.com/APIs-guru/openapi-directory/tree/main/APIs

--- 
### Read YAML into typings

```
npm run api:gen -- --input ./src/example.yaml --output ./src/example.ts
```

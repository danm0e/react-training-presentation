# Orval
---
### What is it?
<div markdown="1">

### `Orval`<!-- .element: class="fragment" --> + `YAML`<!-- .element: class="fragment" -->  = `Client`<!-- .element: class="fragment" -->  + `Types`<!-- .element: class="fragment" -->

</div><!-- .element: class="fragment" -->

Note: When creating a web application that interacts with an API, it is common to use a client library or write an API client manually that abstracts the API calls. This allows you to focus on the front end of your application without worrying about the details of the API like request headers, query parameters, and response handling. With that in mind, it is essential to keep the API client in sync with the API itself to avoid any inconsistencies or bugs.
---

### What Are The Benefits

- Types
- Request Parameters<!-- .element: class="fragment" -->
- Response Schemas<!-- .element: class="fragment" -->
- API Client<!-- .element: class="fragment" -->
- Mocking service workers<!-- .element: class="fragment" -->

Note:
- Get all the types, request parameters, response schemas, and API endpoints automatically.
- Generate the API client from the API definition itself.
- Integrate the API client in our unit tests. Orval provides first class support for mocking through the Mock Service Worker library, and it can automatically generate the MSW handlers for testing server.
 The more complex your API becomes, the more beneficial it is to generate the API client from the API definition to avoid bugs, while keeping type safety and consistency in your API client.
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
---
### Find an example

https://github.com/APIs-guru/openapi-directory/tree/main/APIs

--- 
### Read YAML into typings

```
npm run api:gen -- --input ./src/example.yaml --output ./src/example.ts
```

# Standards for developing a Toto Microservice

These are the coding standards **that MUST be followed** whenever implementing a microservice in the Toto Ecosystem. 

**Always use when:**
- you are building in a codebase that uses the `totoms` package
- you are building in a codebase that uses Toto (e.g. `TotoControllerConfig`, `TotoMicroservice`, etc.)
- you are building in a codebase that exposes REST APIs 
- you are building in a codebase that consumes events from a Pub Sub infrastructure

**NEVER use:**
- if you are building a UI, UI components or in a codebase for an App, a Webapp or a PWA.

---

## REST Endpoints

- **Only** create REST endpoints **when the endpoint needs to be consumed by an external consumer**. Do not create endpoints that are only meant for internal usage within this microservice. Public endpoints will end up being used, so avoid making them if they're only made for internal usage: prefer an internal function or class, not exposed to external consumers.

**RED flags:**
- An endpoint is meant to be used internally by the microservice itself. Prefer a function or class that is not exposed to external consumers through a REST endpoint.

---

## API Documentation

Always follow these rules: 
- [ ] all REST endpoints have to be **documented**. Documentation for all the endpoints must be stored in `docs/interfaces/api-endpoints.md`
- [ ] all REST endpoints documentation **must be kept up-to-date**. Whenever a modification is made to the code base, you **must** check if that requires an update to the endpoints documentation, and if so, update the documentation to reflect the reality. 

**Template for API Endpoints document:**
The `api-endpoints.md` **must** follow this format: 

```markdown
# API Endpoints

[Table of Content]

## Resource 1
| Method | Endpoint | Description | 
| ------ | -------- | ----------- |

### Endpoint 
**Used for:** [describe why this endpoint was created, for which use cases, which scenarios]
**Request & Response:** [link to the classes that represents the expected input and response]

### Endpoint 

## Resource 2 
| Method | Endpoint | Description | 
| ------ | -------- | ----------- |

```

**Success criteria:**
- [ ] The endpoints documentation is up-to-date with the reality of the codebase.

### API Design
- Only use the following HTTP Methods: `POST`, `PUT`, `GET`, `DELETE`. No other methods.
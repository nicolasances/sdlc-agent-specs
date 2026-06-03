# Slicing Strategy for Microservices

*Note: by microservice, this document refers to any backend microservice that provides an API and business logic.*

## Guiding Principle

The guiding principles for slicing an idea into Features for a microservice follows the MVP philosophy: each Feature should deliver a complete, end-to-end user experience, even if it's minimal.

## Methodology

When working with backend Microservices, a feature will be a **vertical slice** that spans from the API endpoint, down to the delegate implementation and down to the DB integration. 
Each slice delivers working **end-to-end** functionality.

**A good task split (vertical slices) looks like this**: 
- Feature 1: 
    - Common functions to all tasks 
    - Empty Store class (remember: Store classes are classes, in my coding standard, dedicated to integrate to DBs) - *E.g. `CustomerStore`*
- Feature 2 - *E.g. Implement POST /customer* 
    - API Endpoint definition and registration 
    - Delegate implementation 
    - Business Logic (eventually using common functions built on Feature 1)
    - Database integration (Store method - *e.g. CustomerStore.saveCustomer()*)
- Feature 3 - *E.g. Implement GET /customers*
    - API Endpoint definition and registration 
    - Delegate implementation 
    - Business Logic (eventually using common functions built on Feature 1)
    - Database integration (Store method - *e.g. CustomerStore.listCustomers()*))

**A BAD task split (horizontal slices) looks like this:**
- Feature 1: 
    - All database integrations, queries, methods (Store calss + all methods)
- Feature 2: 
    - All Business Logic 
- Feature 3: 
    - All Delegate implementations
- Feature 4: 
    - All API Endpoints definition and their registration

### Important rules to follow
- [ ] Each feature must include an API endpoint that is **tied to a specific user story** or consumer need. Avoid creating endpoints that are not directly driven by a consumer story.
- [ ] **Minimize the number of total API endpoints**. Ask yourself these questions: 
    - Does this endpoint need to exist, or should its functionality be combined with another endpoint? 
    - Is this endpoint truly necessary to support a specific user story or consumer need, is it clearly something needed by the frontend or consumer, or is it an implementation detail that can be handled within the service without exposing a new endpoint?
- [ ] **Endpoints are meant to be consumed by the frontend or other services, not to be building blocks for other endpoints**. Each endpoint should have a clear purpose and be driven by a consumer story.

### Mistakes to avoid

- **Do not** split by technical layer (e.g. all DB integration in one feature, all API endpoints in another). Each feature should be a vertical slice that delivers end-to-end functionality.
- **Do not** create features that are too small to deliver a meaningful user experience. 
- **Do not** create endpoints that are not tied to a specific user story or consumer need. Each endpoint should have a clear purpose and be driven by a consumer story.
- **Do not** build API endpoints that are only meant to be used as building blocks for other endpoints. Each endpoint should be designed to be consumed by the frontend or other services, and should have a clear purpose on its own.

## Output Format
Each Feature for a backend microservice should be documented in a markdown file (.md) with the following format:

```markdown
# [Feature Name]

## 1. Purpose & Scope
[A description of the feature, why it's needed and what it does]

**Out of scope**: 
- [Thing deliberately excluded]
- [Thing deliberately excluded]

## 2. Key Endpoints
[Describe the API or Event endpoints this feature introduces or modifies. For each endpoint, include the HTTP method, URL path, a brief description of its purpose, and any relevant details about its behavior, such as expected request parameters, response format, and error handling.]

**Summary of Endpoints:**
| Endpoint Type (event or API) | Method (if API) | URL Path (if API) | Description |
|---------------------|-----------------|-------------------|-------------|

### Endpoint: [HTTP Method] [URL Path]
**Description:** 
[A brief description of the endpoint's purpose and behavior.] 

**Expected Use Case:** 
[Describe the typical use case for this endpoint, including any relevant details about how it fits into the overall user experience or system architecture. Refer to specific frontend user stories or other features if applicable (it is always applicable for an API - there is always a consumer of that API).]

## 4. Business Logic
[Describe the rules, flows, algorithms, and invariants that govern this feature's behavior. This includes any server-side logic that is necessary to support the API endpoints and events described above. Use one bullet per rule; be specific enough that a developer can implement it without guessing.]

## 5. Technical Decisions
[Surface any technical or architectural decision that you are making in the design of this feature, especially if it deviates from standard practices or if there are multiple viable approaches that are significantly different from each other.]

| # | Decision | Rationale |
|---|----------|-----------|

## 6. Success Criteria
[Define clear success criteria for this feature, which can be used to determine when the implementation is complete and meets the requirements. This could include specific API behaviors that must work, performance benchmarks, or any other measurable outcomes that indicate the feature is functioning as intended.]

| # | Criterion | Notes |
|---|-----------|-------|

## 7. Open Questions
[Surface any open questions that you have about the design of this feature, especially if they impact the user experience or the technical implementation. These could be questions about edge cases, error handling, performance considerations, or anything else that is not yet fully defined.]

| # | Question | Notes |
|---|----------|-------|

```

---
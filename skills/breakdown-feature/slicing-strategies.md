# Slicing Strategy for Feature Breakdown

When breaking down a feature into tasks (subfeatures), you **MUST** use the **Vertical Slices Strategy**. 

### Vertical Slices Strategy for Microservices (backend)

When working with backend Microservices, you will split the feature into **vertical slices** that span from the API endpoint, down to the delegate implementation and down to the DB integration. 
Each slice delivers working **end-to-end** functionality.

**A good task split (vertical slices) looks like this**: 
- Tasl 1: 
    - Common functions to all tasks 
    - Empty Store class (remember: Store classes are classes, in my coding standard, dedicated to integrate to DBs) - *E.g. `CustomerStore`*
- Task 2 - *E.g. Implement POST /customer* 
    - API Endpoint definition and registration 
    - Delegate implementation 
    - Business Logic (eventually using common functions built on Task 1)
    - Database integration (Store method - *e.g. CustomerStore.saveCustomer()*)
- Task 3 - *E.g. Implement GET /customers*
    - API Endpoint definition and registration 
    - Delegate implementation 
    - Business Logic (eventually using common functions built on Task 1)
    - Database integration (Store method - *e.g. CustomerStore.listCustomers()*))

**A BAD task split (horizontal slices) looks like this:**
- Task 1: 
    - All database integrations, queries, methods (Store calss + all methods)
- Task 2: 
    - All Business Logic 
- Task 3: 
    - All Delegate implementations
- Task 4: 
    - All API Endpoints definition and their registration


### Vertical Slices Strategy for Frontend

For frontends, the logic is the same. 
A good slice (task) will include: 
- UI
- Presentation logic
- API integration

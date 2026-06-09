# Node Coding Standards

When coding in Typescript in NodeJS you **MUST** follow these coding standards. 

---

## Formatting & Style

### Inline Whenever Possible 

- [ ] **Do not** break a line of code in multiple lines. 

Example: 
```typescript
// DO NOT DO: 
async findByLanguageWithStats({ language, userId, page, pageSize }: {
    language: string;
    userId: string;
    page: number;
    pageSize: number;
}): Promise<VocabularyWithStatsResult> { ... }

// INSTEAD DO: 
async findByLanguageWithStats({ language, userId, page, pageSize }: { language: string; userId: string; page: number; pageSize: number; }): Promise<VocabularyWithStatsResult> { ... }
```

**Exeptions**: 
- **Arrays** can be broken into multiple lines. 
- Complex objects and structures can be broken into multiple lines if the number of fields or the nesting complexity are too high.


### Use Interfaces and Classes rather than inline objects

- [ ] Always use Interfaces and Classes rather than inline objects. 

Example:
```typescript
// DO NOT DO: 
someFunction({ language, userId, page, pageSize }: { language: string; userId: string; page: number; pageSize: number; }): {...}

// INSTEAD DO: 
someFunction(input: SomeFunctionInput): {...}

interface SomeFunctionInput {
    language: string
    userId: string
    page: number
    pageSize: number
}
```

### Space things out

This is a personal preference. I like to read code **well spaced out**.
This is what I typically like: 
- Always put a empty line **before return statements**. 
- Cluster together input validation, but separate it visually from input extraction.
- There should be an empty line after the function header (declaration) and before the first line of code.
- Async invocations should be clearly visible in the code. They should be isolated with an empty line before and after. 
- Single lines within a block statement (or if .. else statement) should not have empty lines around. 
- If statements should be separated from the rest of the code with empty lines before and after.

Example: 
```typescript 
// I DON'T LIKE WHEN ALL CODE IS COMPACTED TOGETHER: 
parseRequest(req: Request): AddSentenceAlternativeRequest {
    const language = req.params.language;
    if (!SUPPORTED_LANGUAGES.includes(language)) throw new ValidationError(400, `Unsupported language: ${language}`);
    const translation = req.body?.translation;
    if (!translation) throw new ValidationError(400, "translation is required");
    return { language, sentenceId: req.params.sentenceId, translation };
}

// I PREFER THIS INSTEAD: 
parseRequest(req: Request): AddSentenceAlternativeRequest {
    
    const language = req.params.language;
    const translation = req.body?.translation;
    
    if (!SUPPORTED_LANGUAGES.includes(language)) throw new ValidationError(400, `Unsupported language: ${language}`);
    if (!translation) throw new ValidationError(400, "translation is required");
    
    return { language, sentenceId: req.params.sentenceId, translation };
}
```

---

## Code Documentation & Comments

### Comment all methods (functions)

- [ ] All methods (functions) must be commented wiht **JSDoc**. Always.

Example of comments
```typescript
    /**
     * [Description of what the function does]
     * 
     * [Any special rules worth documenting (business logic)]:
     * - [Rule 1]
     * - [Rule 2]
     * 
     * @param {type} paramName - [Describe the param and what it's for]
     * 
     * @returns {type} [returned data]
     */
    async saveChallenge(challenge: TomeChallenge): Promise<void> {
        // ...
    }
```

### Comment interface and class fields

- [ ] All class or interface fields (attributes) **must** be commented inline. This is **important**: no documentation of classes and interfaces means poor readability and code that cannot be understood by the user.

Example:
```typescript
interface UserInput {
    id: string;             // The id of the user. Hex string representation of the MongoDB ObjectId. Generated automatically by the Database.
    email: string;          // The email of the user.
    createdAt: string;      // The time at which the user was created. 
}
```

---

## Coding Standards

### Database integration 

- Database integration **must** always happen in a **backend microservice**. 
- Database integration **must** always happen in a "Store" class. E.g. `SentenceStore` will contain all the methods to read and write objects in the `sentence` collection.
- When using MongoDB, no need to wrap `ObjectId` in a try-catch statement. It is ok that a runtime exception is thrown, if the rest of the service is well built (e.g. validation) this should never happen. So **do not do this**: `try { oid = new ObjectId(sentenceId); } catch { ... }`. Just do `new ObjectId(sentenceId)` instead and use it.

---

## Tests

- [ ] When writing unit tests **ALWAYS** use Mocha. 
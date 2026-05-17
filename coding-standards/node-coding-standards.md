# Node Coding Standards

When coding in Typescript in NodeJS you **MUST** follow these coding standards. 

## Style

### Inline Whenever Possible 

**Do not** break a line of code in multiple lines. Example: 

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
- Always put a empty line **before return statements**, unless the return statement is the only statement in an if, else clause. 
- Cluster together input validation, but separate it visually from input extraction.
- There should be an empty line after the function header (declaration) and before the first line of code.

An example: 

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

## Tests

- When writing unit tests **ALWAYS** use Mocha. 
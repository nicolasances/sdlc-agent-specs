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
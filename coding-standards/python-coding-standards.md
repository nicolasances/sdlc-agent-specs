# Python Coding Standards

When coding in Python you **MUST** follow these coding standards. 

## Style

### Inline Whenever Possible 

**Do not** break a line of code in multiple lines. Example: 
```python
# DO NOT DO: 
client = MongoClient(
    host=config.mongo_host,
    username=config.mongo_user,
    password=config.mongo_pwd,
    authSource=config.get_db_name(),
)

## INSTEAD DO:
client = MongoClient( host=config.mongo_host, username=config.mongo_user, password=config.mongo_pwd, authSource=config.get_db_name() )
```

**Exeptions**: 
- **Arrays** can be broken into multiple lines. 
- Complex list comprehension can be broken into multiple lines.
- **Dicts** can be broken into multiple lines.
- `asyncio.gather(...)` statements. 

### Space things 

You should always have an empty line: 
1. Before `return` statements, unless the statement is the only statement of a conditional statement. 
2. Before and after `await` statements. I like async invocations to be clearly visible in the code. 

Example of 1): 
```python
# DO NOT DO: 
accepted_texts = {s.sentence for s in result.sentences}
return accepted_texts

# INSTEAD DO: 
accepted_texts = {s.sentence for s in result.sentences}

return accepted_texts
```

Example of 2): 
```python
# DO NOT DO: 
as_generated = [GeneratedSentence(sentence=s.sentence, translation=s.translation) for s in sentences]
result = await self._run_verification(as_generated)
print(result.text)

# INSTEAD DO DO: 
as_generated = [GeneratedSentence(sentence=s.sentence, translation=s.translation) for s in sentences]

result = await self._run_verification(as_generated)

print(result.text)

```
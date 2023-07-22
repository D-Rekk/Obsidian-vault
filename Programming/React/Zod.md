> **Title**: Zod
> **Date**: 2023/ 21st Jul
> **Tags**:  #Typescript #React #schema #Zod
---

Although TypeScript looks great in all aspects, it only does static *type checking at compile time* and **doesn’t have any runtime checks** at all.
This is where Zod does, *runtime verification* and *schema validation*.

### Schema validation
---
**Schema validation** is the process of checking whether data adheres to a predefined structure or a set of rules, namely *schema*. A schema defines the expected format, constraints, and rules that data must follow to be considered valid. 

# What is Zod
---
Runtime checks help with getting correctly validated data on the server side. In a case where the user is filling out some kind of form, TypeScript doesn’t know if the user inputs are as good as you expect them to be on the server at runtime.
**Zod** helps with *data integrity* and prevents sending out garbage values to the database. 

## Zod benefits

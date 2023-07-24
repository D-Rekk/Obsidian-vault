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

## How to use Zod
---
```TypeScript
import { z } from "zod"
const dataInputFromUser = z.string().min(8).max(16)
dataInputFromUser.parse("A long text")
```

Primitive values are not just limited to `string`, but provide other methods such as `number`, `bigint`, `boolean`, and `date`. There are a couple of empty types as well, like `undefined`, `null`, and `void`.

---
Most of the user-facing form require more than a single entries. This is where to use **Zod object**: it creates a schema that can set properties you want to check at runtime.
```TS
const formData = z.object({
	firstName = z.string().min(2).max(32),
	lastName = z.string().min(2).max(16),
	phone = z.string().min(10).max(14).optional(),
	email = z.string().email(),
	url = z.string().url().optional(),
})

type FormData = z.infer<typeof FormData>;

const validateFormData = (inputs: FormData) => {
  try {
	  const isValidData = FormData.parse(inputs);
	  console.log('Validated Form Data:', isValidData);
	  return isValidData;
  } catch (error) {
  console.error('Validation Error:', error.message);
  throw error; // Rethrow the validation error to be handled elsewhere if needed. }
};
```

>With `z.infer` we don't have to rewrite a type with every single key-entry of the defined object; we can simply infer it's type with `z.infer<typeof zObject>`

If you want to defined custom intervals or messages you can use **Zod refinements**.
**refine** is a method that let's you customize validation on your schema. It also allows you to defined additional checks on the data
```TS
const userBio = z.string().refine((i) => i.length <= 255, {
	message: `You Bio can't surpass 255 characters`
})
```
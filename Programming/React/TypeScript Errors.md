Created: October 29, 2022 11:01 PM
Status: Open
Updated: October 29, 2022 11:27 PM

### (2339) Property 'name' does not exist on type 'object[]’

Content

```tsx
myObject.someProperty //ts(2339)
myObject.someProperty as any
```

---

### (7015) Element implicitly has an 'any' type because index expression is not of type 'number’

Happens because you’re trying to access an object not using the **dot-notation** but using the **index-notation**

```tsx
myObject['results'] //ts(7015)
myObject['results' as keyof typeof myObject] //or just keyof object
```

---
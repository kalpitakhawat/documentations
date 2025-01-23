# Generics in TypeScript

## Overview

Generics in TypeScript provide a way to create reusable, flexible, and type-safe components, functions, and classes. They allow developers to define the type of values a function, class, or interface can work with, improving code reusability and type safety.

---

## Why Use Generics?

1. **Code Reusability:**
   - Write flexible code that can work with multiple data types.

2. **Type Safety:**
   - Ensures consistency and correctness without sacrificing flexibility.

3. **Improved Maintainability:**
   - Makes it easier to scale and refactor code without type-related errors.

---

## Generic Functions

Generics allow us to create functions that work with a variety of types.

### Example:

```typescript
function identity<T>(value: T): T {
    return value;
}

let result1 = identity<string>("Hello");  // Type is string
let result2 = identity<number>(42);        // Type is number
```

### Explanation:
- `<T>` represents a type parameter.
- The function can take a value of any type `T` and return the same type.

---

## Generic Interfaces

Generic interfaces define contracts that work with a variety of types.

### Example:

```typescript
interface Box<T> {
    value: T;
}

let stringBox: Box<string> = { value: "TypeScript" };
let numberBox: Box<number> = { value: 100 };
```

### Explanation:
- The interface `Box<T>` accepts a generic type `T`.
- `stringBox` holds a string value, and `numberBox` holds a number value.

---

## Generic Classes

Generic classes provide flexibility while maintaining strong type checks.

### Example:

```typescript
class Storage<T> {
    private items: T[] = [];

    addItem(item: T): void {
        this.items.push(item);
    }

    getItems(): T[] {
        return this.items;
    }
}

let numberStorage = new Storage<number>();
numberStorage.addItem(10);
numberStorage.addItem(20);
console.log(numberStorage.getItems());
```

### Explanation:
- The `Storage<T>` class stores an array of any type `T`.
- The `addItem` method adds elements of the specified type.

---

## Generic Constraints

Constraints restrict the types that can be used with generics.

### Example:

```typescript
interface Lengthwise {
    length: number;
}

function logLength<T extends Lengthwise>(item: T): void {
    console.log(item.length);
}

logLength({ length: 10, value: "test" });  // Works
logLength("Hello");  // Works because strings have length
// logLength(42);    // Error: number doesn't have length property
```

### Explanation:
- The `T extends Lengthwise` constraint ensures that the type has a `length` property.

---

## Generic Type Aliases

Generics can also be used in type aliases to create flexible and reusable types.

### Example:

```typescript
type Pair<T, U> = {
    first: T;
    second: U;
};

const pair: Pair<string, number> = { first: "Age", second: 30 };
```

---

## Utility Types with Generics

TypeScript provides several built-in utility types that use generics to transform types.

### Common Utility Types:

1. **Partial<T>** – Makes all properties of a type optional.
   ```typescript
   interface Person {
       name: string;
       age: number;
   }

   let partialPerson: Partial<Person> = { name: "John" };
   ```

2. **Readonly<T>** – Makes all properties of a type immutable.
   ```typescript
   const readonlyPerson: Readonly<Person> = { name: "John", age: 30 };
   // readonlyPerson.age = 31; // Error
   ```

3. **Record<K, T>** – Creates an object type with keys of type `K` and values of type `T`.
   ```typescript
   let userRoles: Record<string, string> = { admin: "John", editor: "Jane" };
   ```

4. **Pick<T, K>** – Constructs a type by picking a set of properties from another type.
   ```typescript
   interface User {
       id: number;
       name: string;
       age: number;
   }

   type UserPreview = Pick<User, 'id' | 'name'>;
   const user: UserPreview = { id: 1, name: "Alice" };
   ```

5. **Omit<T, K>** – Constructs a type by excluding a set of properties from another type.
   ```typescript
   type UserWithoutAge = Omit<User, 'age'>;
   const user: UserWithoutAge = { id: 1, name: "Alice" };
   ```

6. **Required<T>** – Makes all optional properties required.
   ```typescript
   interface Profile {
       name?: string;
       age?: number;
   }

   type CompleteProfile = Required<Profile>;
   ```

7. **Exclude<T, U>** – Excludes types from a union.
   ```typescript
   type Primitive = string | number | boolean;
   type StringOrNumber = Exclude<Primitive, boolean>;
   ```

8. **Extract<T, U>** – Extracts types that are assignable to another type.
   ```typescript
   type Primitive = string | number | boolean;
   type StringsOnly = Extract<Primitive, string>;
   ```

---

## Best Practices

1. **Use Descriptive Type Parameters:**
   - Instead of using single letters like `T`, use meaningful names like `ItemType`.

2. **Avoid Overusing Generics:**
   - Only use generics when truly necessary to maintain simplicity.

3. **Combine Generics with Constraints:**
   - Use constraints to ensure the flexibility of generics while maintaining type safety.

---

## Conclusion

Generics in TypeScript provide powerful tools to create flexible and reusable components while ensuring type safety. They help to write DRY (Don't Repeat Yourself) code and improve overall code maintainability.

---

## Official Documentation

- [TypeScript Generics](https://www.typescriptlang.org/docs/handbook/generics.html)

---

Happy coding with TypeScript!


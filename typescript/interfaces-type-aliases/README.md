# Interfaces and Type Aliases in TypeScript

## Overview

In TypeScript, both **interfaces** and **type aliases** provide ways to define the shape of objects and enforce structure within code. Understanding their differences and use cases is crucial for writing maintainable and scalable applications.

---

## What is an Interface?

An interface is a blueprint for an object that defines the structure it should follow. Interfaces are useful for defining contracts in object-oriented programming.

### Example:

```typescript
interface Person {
    name: string;
    age: number;
    greet(): string;
}

const person: Person = {
    name: "Alice",
    age: 30,
    greet() {
        return `Hello, my name is ${this.name}`;
    }
};
```

---

## What is a Type Alias?

A type alias is a way to create a new name for a type. It can represent primitive types, union types, or object shapes.

### Example:

```typescript
type PersonType = {
    name: string;
    age: number;
    greet(): string;
};

const person: PersonType = {
    name: "Bob",
    age: 25,
    greet() {
        return `Hello, I am ${this.name}`;
    }
};
```

---

## Differences Between Interfaces and Type Aliases

| Feature                | Interface               | Type Alias                |
|----------------------- |-------------------------|---------------------------|
| Extensibility          | Can be extended          | Cannot be extended         |
| Merging                | Supports declaration merging | Does not support merging   |
| Use Cases              | Best for defining objects | Great for complex types    |

---

## Extending Interfaces and Types

### Extending Interfaces

Interfaces can be extended using the `extends` keyword to add new properties.

```typescript
interface Employee extends Person {
    jobTitle: string;
}

const employee: Employee = {
    name: "Charlie",
    age: 40,
    jobTitle: "Engineer",
    greet() {
        return `Hello, I am ${this.name}`;
    }
};
```

### Extending Type Aliases

Type aliases can be combined using intersections (`&`).

```typescript
type EmployeeType = PersonType & {
    jobTitle: string;
};

const employee: EmployeeType = {
    name: "Dave",
    age: 28,
    jobTitle: "Designer",
    greet() {
        return `Hi, I am ${this.name}`;
    }
};
```

---

## When to Use Interfaces vs Type Aliases

### Use Interfaces When:
- You need to define object shapes.
- You want to extend or merge structures.
- You are using an OOP-oriented approach.

### Use Type Aliases When:
- You need to define complex types (e.g. unions and intersections).
- You want to create reusable utility types.
- You prefer flexibility with type composition.

---

## Best Practices

1. **Use interfaces when defining object shapes and extending behavior.**
2. **Use type aliases for complex unions, intersections, and primitive aliases.**
3. **Prefer interfaces when working with public libraries to enable declaration merging.**
4. **Choose consistency across your codebase; do not mix interfaces and types arbitrarily.**

---

## Conclusion

Both interfaces and type aliases are powerful features in TypeScript that help maintain code clarity and enforce type safety. Choosing between them depends on your project's specific needs and preferences.

---

## Official Documentation

- [TypeScript Interfaces](https://www.typescriptlang.org/docs/handbook/interfaces.html)
- [TypeScript Type Aliases](https://www.typescriptlang.org/docs/handbook/advanced-types.html#type-aliases)

---

Happy coding with TypeScript!


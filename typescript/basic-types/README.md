# Basic Types in TypeScript

## Overview

TypeScript provides a set of basic types that allow developers to specify the shape and behavior of values in their code. Using these types enhances code quality by catching potential errors at compile time and improving readability.

---

## Primitive Types

### 1. **`string`**
   Represents textual data.

   ```typescript
   let firstName: string = "John";
   let message: string = `Hello, ${firstName}!`;
   ```

### 2. **`number`**
   Represents numeric values, including integers and floating-point numbers.

   ```typescript
   let age: number = 30;
   let price: number = 99.99;
   ```

### 3. **`boolean`**
   Represents true or false values.

   ```typescript
   let isCompleted: boolean = true;
   ```

### 4. **`null` and `undefined`**
   - `null` represents an explicitly empty value.
   - `undefined` represents an uninitialized variable.

   ```typescript
   let emptyValue: null = null;
   let notAssigned: undefined = undefined;
   ```

### 5. **`bigint`**
   Represents large integers that exceed the safe limit of `number`.

   ```typescript
   let largeNumber: bigint = 9007199254740991n;
   ```

### 6. **`symbol`**
   Represents unique values useful for object property keys.

   ```typescript
   const uniqueKey: symbol = Symbol('key');
   ```

---

## Special Types

### 1. **`any`**
   Disables type checking and allows any value. Use with caution as it defeats TypeScript's type-safety features.

   ```typescript
   let randomValue: any = "Hello";
   randomValue = 42;
   ```

### 2. **`unknown`**
   Represents values of any type but requires type checking before usage.

   ```typescript
   let unknownValue: unknown = "Hello";
   if (typeof unknownValue === 'string') {
       console.log(unknownValue.toUpperCase());
   }
   ```

### 3. **`void`**
   Used for functions that do not return a value.

   ```typescript
   function logMessage(message: string): void {
       console.log(message);
   }
   ```

### 4. **`never`**
   Represents values that will never occur, often used for functions that throw errors.

   ```typescript
   function throwError(message: string): never {
       throw new Error(message);
   }
   ```

---

## Type Inference

TypeScript can infer types based on assigned values, reducing the need for explicit type annotations.

```typescript
let inferredString = "Hello"; // inferred as string
let inferredNumber = 100;     // inferred as number
```

---

## Type Assertions

Used to tell TypeScript that a value is of a specific type when its actual type is unknown.

```typescript
let someValue: any = "This is a string";
let strLength: number = (someValue as string).length;
```

---

## Union and Intersection Types

### Union Types
Allows a variable to hold multiple types.

```typescript
let value: string | number;
value = "Hello";
value = 42;
```

### Intersection Types
Combines multiple types into one.

```typescript
type Employee = { name: string } & { age: number };
let employee: Employee = { name: "Alice", age: 25 };
```

---

## Best Practices

1. Prefer specific types over `any` to maintain type safety.
2. Use type inference where possible to reduce redundancy.
3. Leverage `unknown` over `any` when handling uncertain values.
4. Always initialize variables to avoid `undefined` issues.

---

## Conclusion

Understanding and utilizing TypeScript's basic types is fundamental to writing robust and error-free code. They provide the foundation for more advanced TypeScript features.

---

## Official Documentation

- [TypeScript Basic Types](https://www.typescriptlang.org/docs/handbook/basic-types.html)

---

Happy coding with TypeScript!


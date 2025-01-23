# Decorators and Modules in TypeScript

## Overview

TypeScript provides **decorators** and **modules** as powerful features to enhance code organization and reusability. Decorators allow developers to add metadata and behavior to classes and their members, while modules enable the organization of code into reusable, maintainable units.

---

# Decorators in TypeScript

## What are Decorators?

Decorators in TypeScript are special functions that allow you to modify classes, methods, properties, and parameters at design time. They provide a declarative way to add behavior and metadata.

Decorators are commonly used in frameworks such as Angular for dependency injection and metadata handling.

### Enabling Decorators

To use decorators in TypeScript, you must enable them in your `tsconfig.json` file:

```json
{
  "compilerOptions": {
    "experimentalDecorators": true,
    "emitDecoratorMetadata": true
  }
}
```

---

## Types of Decorators

### 1. Class Decorators

Class decorators are applied to classes to enhance or modify their behavior.

#### Example:

```typescript
function Logger(constructor: Function) {
    console.log("Logging class:", constructor);
}

@Logger
class Person {
    constructor(public name: string) {}
}

const p = new Person("John");
// Output: Logging class: [class Person]
```

### 2. Method Decorators

Method decorators are used to modify the behavior of class methods.

#### Example:

```typescript
function LogMethod(target: any, propertyKey: string, descriptor: PropertyDescriptor) {
    console.log(`Method called: ${propertyKey}`);
}

class Calculator {
    @LogMethod
    add(a: number, b: number): number {
        return a + b;
    }
}

const calc = new Calculator();
calc.add(2, 3);
// Output: Method called: add
```

### 3. Property Decorators

Property decorators are used to add metadata or validation logic to class properties.

#### Example:

```typescript
function ReadOnly(target: any, propertyKey: string) {
    Object.defineProperty(target, propertyKey, {
        writable: false
    });
}

class User {
    @ReadOnly
    role: string = "admin";
}

const user = new User();
user.role = "guest"; // Error: Cannot assign to 'role' because it is a read-only property.
```

### 4. Parameter Decorators

Parameter decorators allow modifying the behavior of function parameters.

#### Example:

```typescript
function LogParameter(target: any, propertyKey: string, parameterIndex: number) {
    console.log(`Parameter index: ${parameterIndex} in method ${propertyKey}`);
}

class Product {
    setPrice(@LogParameter price: number) {
        console.log(`Price set to: ${price}`);
    }
}

const product = new Product();
product.setPrice(100);
// Output: Parameter index: 0 in method setPrice
```

---

# Modules in TypeScript

## What are Modules?

Modules in TypeScript allow developers to break the code into smaller, reusable files. Modules help in maintaining code structure and reusability across different parts of an application.

TypeScript follows the **ES6 module system**, using `import` and `export` keywords to facilitate code reuse.

---

## Exporting and Importing Modules

### 1. Exporting from a Module

You can export values, functions, classes, and interfaces from a module.

#### Example:

```typescript
// utils.ts
export function greet(name: string): string {
    return `Hello, ${name}!`;
}

export const PI = 3.14;
```

### 2. Importing a Module

You can import an exported member from another module using `import`.

#### Example:

```typescript
// main.ts
import { greet, PI } from './utils';

console.log(greet("Alice")); // Outputs: Hello, Alice!
console.log(PI);              // Outputs: 3.14
```

### 3. Default Exports

You can have a default export when a module has a single entity to export.

#### Example:

```typescript
// math.ts
export default class MathHelper {
    static square(x: number): number {
        return x * x;
    }
}
```

```typescript
// app.ts
import MathHelper from './math';
console.log(MathHelper.square(5)); // Outputs: 25
```

### 4. Importing Everything

You can import all exports from a module using `*`.

#### Example:

```typescript
import * as Utils from './utils';

console.log(Utils.greet("Bob"));
console.log(Utils.PI);
```

---

## Module Resolution

TypeScript supports various module resolution strategies, including:

- **Node Module Resolution:** Compatible with Node.js module resolution system.
- **Classic Module Resolution:** Used for legacy projects.

You can configure module resolution in `tsconfig.json`:

```json
{
  "compilerOptions": {
    "module": "ES6",
    "moduleResolution": "Node"
  }
}
```

---

## Namespaces vs Modules

In older TypeScript versions, **namespaces** were used for organizing code, but modern TypeScript recommends using **modules** instead. Modules offer better compatibility with modern JavaScript and provide better tooling support.

---

## Best Practices

1. **Use Decorators Judiciously:**
   - Avoid overusing decorators; use them where metadata or behavior enhancement is needed.

2. **Organize Modules Logically:**
   - Break down large applications into smaller modules for better maintainability.

3. **Avoid Circular Dependencies:**
   - Ensure that modules do not depend on each other in a cyclic way to avoid runtime issues.

4. **Use Default Exports Sparingly:**
   - Named exports are preferred to make imports clearer and less ambiguous.

---

## Conclusion

Decorators and modules in TypeScript are powerful tools to enhance code structure and maintainability. Decorators provide a way to add behavior declaratively, while modules allow for better organization and reuse of code across projects.

---

## Official Documentation

- [TypeScript Decorators](https://www.typescriptlang.org/docs/handbook/decorators.html)
- [TypeScript Modules](https://www.typescriptlang.org/docs/handbook/modules.html)

---

Happy coding with TypeScript!


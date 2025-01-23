# Type Guards in TypeScript

## Overview

Type Guards in TypeScript are mechanisms used to ensure type safety at runtime. They allow developers to narrow down types within conditional blocks, enabling more precise type checks and safer operations when dealing with union types or values of uncertain types.

TypeScript provides several built-in ways to create type guards, including `typeof`, `instanceof`, user-defined type guards, and discriminated unions.

---

## Why Use Type Guards?

1. **Type Safety:**
   - Ensures that operations are performed on the correct types, preventing runtime errors.

2. **Improved Code Readability:**
   - Makes the code easier to understand by providing explicit type checks.

3. **Enhanced IntelliSense:**
   - Helps IDEs provide better code completion suggestions based on narrowed types.

4. **Refactoring Support:**
   - Simplifies debugging and maintenance of complex applications.

---

## Built-in Type Guards

### 1. **`typeof` Type Guard**

The `typeof` operator is used to check primitive types like `string`, `number`, `boolean`, etc.

#### Example:
```typescript
function logValue(value: string | number) {
    if (typeof value === "string") {
        console.log("It's a string: ", value.toUpperCase());
    } else {
        console.log("It's a number: ", value.toFixed(2));
    }
}

logValue("Hello");  // Outputs: It's a string: HELLO
logValue(42);        // Outputs: It's a number: 42.00
```

### 2. **`instanceof` Type Guard**

The `instanceof` operator checks whether an object is an instance of a specific class.

#### Example:
```typescript
class Car {
    drive() {
        console.log("Driving a car...");
    }
}

class Bike {
    ride() {
        console.log("Riding a bike...");
    }
}

function useVehicle(vehicle: Car | Bike) {
    if (vehicle instanceof Car) {
        vehicle.drive();
    } else {
        vehicle.ride();
    }
}

useVehicle(new Car());  // Outputs: Driving a car...
useVehicle(new Bike()); // Outputs: Riding a bike...
```

---

## User-Defined Type Guards

Custom functions can be created to determine an object's type by returning a type predicate.

#### Example:
```typescript
interface Dog {
    bark: () => void;
}

interface Cat {
    meow: () => void;
}

function isDog(animal: Dog | Cat): animal is Dog {
    return (animal as Dog).bark !== undefined;
}

function makeNoise(animal: Dog | Cat) {
    if (isDog(animal)) {
        animal.bark();
    } else {
        animal.meow();
    }
}

const pet1: Dog = { bark: () => console.log("Woof!") };
const pet2: Cat = { meow: () => console.log("Meow!") };

makeNoise(pet1); // Outputs: Woof!
makeNoise(pet2); // Outputs: Meow!
```

---

## Discriminated Unions

TypeScript allows using discriminated unions, which have a common property to distinguish between different types.

#### Example:
```typescript
interface Square {
    kind: "square";
    size: number;
}

interface Circle {
    kind: "circle";
    radius: number;
}

type Shape = Square | Circle;

function getArea(shape: Shape): number {
    switch (shape.kind) {
        case "square":
            return shape.size * shape.size;
        case "circle":
            return Math.PI * shape.radius * shape.radius;
    }
}

console.log(getArea({ kind: "square", size: 10 })); // Outputs: 100
console.log(getArea({ kind: "circle", radius: 5 })); // Outputs: 78.54
```

---

## Type Assertions vs Type Guards

While type guards dynamically check types at runtime, type assertions allow developers to override TypeScript's type inference when they are confident about a value's type.

#### Example:
```typescript
let value: any = "Hello";
let strLength: number = (value as string).length;
console.log(strLength);  // Outputs: 5
```

**Best Practice:** Prefer type guards over assertions to ensure runtime safety.

---

## Best Practices

1. **Prefer Built-in Type Guards:**
   - Use `typeof` and `instanceof` where applicable for reliable type checks.

2. **Encapsulate Type Logic in Functions:**
   - Create user-defined type guard functions for complex checks.

3. **Use Discriminated Unions:**
   - Leverage a common field to simplify type narrowing.

4. **Avoid Excessive Type Assertions:**
   - Overuse of assertions can lead to runtime errors.

---

## Conclusion

Type guards in TypeScript are an essential tool to ensure type safety at runtime, allowing developers to write more reliable and predictable code. By utilizing built-in type checks and custom guards, you can enhance code quality and avoid potential runtime errors.

---

## Official Documentation

- [TypeScript Type Guards](https://www.typescriptlang.org/docs/handbook/advanced-types.html#typeof-type-guards)
- [TypeScript Discriminated Unions](https://www.typescriptlang.org/docs/handbook/unions-and-intersections.html)

---

Happy coding with TypeScript!


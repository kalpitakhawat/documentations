# Introduction to TypeScript

## Overview

TypeScript is a statically typed superset of JavaScript that compiles to plain JavaScript. Developed and maintained by Microsoft, TypeScript enhances JavaScript with optional static typing, interfaces, generics, and modern features, making it ideal for large-scale application development.

This guide introduces TypeScript's core concepts, its advantages, and how to set it up for your projects.

---

## Why Use TypeScript?

1. **Static Typing**  
   - TypeScript enables early error detection and improves code reliability by catching type-related bugs at compile time.

2. **Improved Developer Experience**  
   - Features such as IntelliSense, autocompletion, and better refactoring support enhance productivity.

3. **Modern JavaScript Features**  
   - Includes ES6+ features and additional capabilities such as interfaces, decorators, and namespaces.

4. **Scalability**  
   - Well-suited for large applications, improving maintainability and collaboration among developers.

5. **Seamless JavaScript Integration**  
   - TypeScript code compiles to standard JavaScript, allowing it to run in any JavaScript environment.

---

## Installing TypeScript

You can install TypeScript globally using npm:

```bash
npm install -g typescript
```

To verify the installation:

```bash
tsc --version
```

---

## Setting Up a TypeScript Project

Follow these steps to set up a basic TypeScript project:

1. **Initialize a project with TypeScript configuration:**
   ```bash
   tsc --init
   ```

2. **This creates a `tsconfig.json` file where you can define configurations like:**
   ```json
   {
     "compilerOptions": {
       "target": "ES6",
       "module": "CommonJS",
       "strict": true,
       "outDir": "dist",
       "rootDir": "src"
     }
   }
   ```

3. **Create a TypeScript file (`src/index.ts`):**
   ```typescript
   function greet(name: string): string {
       return `Hello, ${name}!`;
   }
   console.log(greet("World"));
   ```

4. **Compile the TypeScript file:**
   ```bash
   tsc
   ```

5. **Run the generated JavaScript file:**
   ```bash
   node dist/index.js
   ```

---

## TypeScript vs JavaScript

| Feature              | TypeScript                         | JavaScript                     |
|--------------------- |---------------------------------- |------------------------------- |
| Typing               | Static (Optional)                 | Dynamic                        |
| Compilation          | Required (to JS)                  | Not required                   |
| Error Detection      | Compile-time errors               | Runtime errors                 |
| Tooling Support      | Strong (VS Code, WebStorm)        | Basic                          |
| Ecosystem            | Integrates well with JS libraries | Natively supported everywhere  |

---

## Core TypeScript Concepts

1. **Basic Types**  
   - `string`, `number`, `boolean`, `null`, `undefined`, `any`, `void`

2. **Advanced Types**  
   - Union types, intersection types, and literal types.

3. **Interfaces and Type Aliases**  
   - Enforce type structures and improve code reusability.

4. **Generics**  
   - Reusable components with dynamic types.

5. **Modules and Namespaces**  
   - Code organization and dependency management.

---

## Next Steps

Continue exploring TypeScript with the following guides:

- **[Basic Types](../basic-types/README.md)**
- **[Interfaces and Generics](../interfaces-type-aliases/README.md)**
- **[Decorators and Modules](../decorators-modules/README.md)**

---

## Official Documentation

For more information, visit the official TypeScript documentation:

- [TypeScript Documentation](https://www.typescriptlang.org/docs/)
- [TypeScript Playground](https://www.typescriptlang.org/play)
- [GitHub Repository](https://github.com/microsoft/TypeScript)

---

Happy coding with TypeScript!


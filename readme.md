# TypeScript Types and Enums: A Quick Guide

This repository contains explanations and examples of key TypeScript concepts: the differences between `any`, `unknown`, and `never` types, and the use of enums with examples.

## 📌 TypeScript Types: `any`, `unknown`, and `never`

Understanding these three types is crucial for writing type-safe TypeScript code:

### 1. `any`
The `any` type is the most flexible type in TypeScript. It essentially turns off type checking for a variable, allowing it to be assigned any value and permitting any operations on it.

```typescript
let flexible: any = "I can be anything";
flexible = 42;               // OK
flexible = true;             // OK
flexible.nonExistentMethod(); // Also OK (no compile error, but runtime error)
```

⚠️ **Warning**: Overuse of `any` defeats the purpose of TypeScript's type system. Use it sparingly!

### 2. `unknown`
The `unknown` type is TypeScript's type-safe counterpart to `any`. While it can hold any value like `any`, you can't perform arbitrary operations on an `unknown` variable without first narrowing its type.

```typescript
let uncertain: unknown = "Could be anything";

// The following would cause compile errors:
// uncertain.toUpperCase(); 
// let sure: string = uncertain;

// Proper usage with type narrowing:
if (typeof uncertain === "string") {
    console.log(uncertain.toUpperCase()); // Now OK
}
```

✅ **Best Practice**: Prefer `unknown` over `any` when you need flexibility but want to maintain type safety.

### 3. `never`
The `never` type represents values that should never occur. It's used for functions that always throw exceptions or never return, and for impossible type intersections.

```typescript
// Function that always throws
function error(message: string): never {
    throw new Error(message);
}

// Function with infinite loop
function infiniteLoop(): never {
    while (true) {}
}

// Also used in exhaustive type checking
type Shape = 'circle' | 'square';

function getArea(shape: Shape): number {
    switch (shape) {
        case 'circle': return Math.PI * 2;
        case 'square': return 4;
        default: 
            const exhaustiveCheck: never = shape;
            return exhaustiveCheck;
    }
}
```

🔍 **Key Difference**: While `any` allows everything, `unknown` requires type checking before operations, and `never` represents unreachable code or impossible states.

## 🌟 Enums in TypeScript

Enums (enumerations) allow you to define a set of named constants, making your code more readable and maintainable.

### Numeric Enum Example
By default, enums are numeric, starting from 0:

```typescript
enum Direction {
    North,    // 0
    East,     // 1
    South,    // 2
    West      // 3
}

let heading: Direction = Direction.North;
console.log(heading); // Output: 0
```

You can also set specific numeric values:

```typescript
enum StatusCodes {
    OK = 200,
    BadRequest = 400,
    Unauthorized = 401,
    NotFound = 404,
    ServerError = 500
}

let responseCode: StatusCodes = StatusCodes.OK;
```

### String Enum Example
String enums are more readable and meaningful when serialized:

```typescript
enum LogLevel {
    ERROR = "ERROR",
    WARN = "WARNING",
    INFO = "INFORMATION",
    DEBUG = "DEBUG"
}

let currentLogLevel: LogLevel = LogLevel.INFO;
console.log(`Current log level: ${currentLogLevel}`); 
// Output: "Current log level: INFORMATION"
```

### Why Use Enums?
1. **Self-documenting code**: Makes it clear what values are acceptable
2. **Type safety**: Prevents invalid values from being assigned
3. **Autocomplete**: IDEs can suggest possible enum values
4. **Consistency**: Ensures the same value is used throughout the codebase

## 🚀 Getting Started

To experiment with these examples:

1. Clone this repository
2. Install TypeScript: `npm install -g typescript`
3. Compile and run the examples

## 📚 Additional Resources

- [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/intro.html)
- [TypeScript Deep Dive](https://basarat.gitbook.io/typescript/)
- [TypeScript Playground](https://www.typescriptlang.org/play)

Happy coding! 💻✨
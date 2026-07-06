# TypeScript Interview Notes (React + TypeScript)

> Focused for Senior Frontend / React Interviews (e.g., SonicWall)

---

# Table of Contents

1. What is TypeScript?
2. Why TypeScript?
3. Basic Types
4. Arrays
5. Objects
6. Optional Properties
7. Readonly Properties
8. Function Types
9. Void
10. Never
11. Any
12. Unknown
13. Type Inference
14. Type Alias
15. Interface
16. Type vs Interface
17. Union Types
18. Literal Types
19. Intersection Types
20. Enum
21. Tuple
22. Generics
23. Generic Interfaces
24. keyof
25. typeof
26. Utility Types
27. Type Narrowing
28. Optional Chaining
29. Nullish Coalescing
30. Type Assertion
31. Type Guards
32. Optional Parameters
33. Default Parameters
34. Rest Parameters
35. Generic Constraints
36. Frequently Asked Interview Questions

---

# 1. What is TypeScript?

TypeScript is a **statically typed superset of JavaScript** developed by Microsoft. It adds type checking during development, making applications more reliable and easier to maintain.

### Benefits

- Detects errors at compile time
- Better IntelliSense
- Easier refactoring
- Improves code readability
- Great for large applications

---

# 2. Why TypeScript?

### JavaScript

```javascript
function add(a, b) {
    return a + b;
}

add(10, "20"); // "1020"
```

No compile-time error.

### TypeScript

```typescript
function add(a: number, b: number): number {
    return a + b;
}

add(10, "20");
```

Compile-time error.

---

# 3. Basic Types

```typescript
let age: number = 28;
let name: string = "John";
let isAdmin: boolean = false;
let data: null = null;
let value: undefined = undefined;
```

---

# 4. Arrays

```typescript
let numbers: number[] = [1,2,3];

let names: Array<string> = ["John", "Bob"];
```

---

# 5. Objects

```typescript
let user: {
    id: number;
    name: string;
} = {
    id: 1,
    name: "John"
};
```

---

# 6. Optional Properties

```typescript
interface User {
    id: number;
    name: string;
    age?: number;
}
```

`age` is optional.

---

# 7. Readonly Properties

```typescript
interface User {
    readonly id: number;
    name: string;
}

const user: User = {
    id: 1,
    name: "John"
};

// user.id = 5 ❌ Error
```

---

# 8. Function Types

```typescript
function greet(name: string): string {
    return `Hello ${name}`;
}
```

Arrow function

```typescript
const add = (a: number, b: number): number => {
    return a + b;
};
```

---

# 9. Void

```typescript
function print(): void {
    console.log("Hello");
}
```

Used when nothing is returned.

---

# 10. Never

Used when a function never completes normally.

```typescript
function error(message: string): never {
    throw new Error(message);
}
```

Another example

```typescript
while(true) {

}
```

### Difference

| void | never |
|------|--------|
| Returns nothing | Never returns |
| Function completes | Function never completes |

---

# 11. Any

```typescript
let value: any = "Hello";

value = 10;
value = true;
```

Avoid using `any` whenever possible.

---

# 12. Unknown

Safer than `any`.

```typescript
let value: unknown = "Hello";

// value.length ❌
```

Need narrowing.

```typescript
if (typeof value === "string") {
    console.log(value.length);
}
```

### any vs unknown

| any | unknown |
|------|----------|
| Unsafe | Safe |
| No type checking | Requires narrowing |
| Can access properties | Cannot until checked |

---

# 13. Type Inference

```typescript
let age = 30;
```

TypeScript automatically infers

```typescript
number
```

---

# 14. Type Alias

```typescript
type User = {
    id: number;
    name: string;
};
```

---

# 15. Interface

```typescript
interface User {
    id: number;
    name: string;
}
```

---

# 16. Type vs Interface ⭐⭐⭐⭐⭐

## Interface

```typescript
interface User {
    id: number;
}

interface Employee extends User {
    salary: number;
}
```

## Type

```typescript
type User = {
    id: number;
};

type Status = "Pending" | "Completed";
```

### Differences

| Interface | Type |
|------------|------|
| Object shapes | Any type |
| Extendable | Uses intersections |
| Declaration merging | No declaration merging |
| Preferred for APIs | Preferred for unions & utility types |

---

# 17. Union Types

```typescript
let id: number | string;

id = 10;
id = "EMP001";
```

---

# 18. Literal Types

```typescript
type Direction = "left" | "right" | "top" | "bottom";
```

---

# 19. Intersection Types

```typescript
type Person = {
    name: string;
};

type Employee = {
    salary: number;
};

type Staff = Person & Employee;
```

---

# 20. Enum

Numeric Enum

```typescript
enum Role {
    Admin,
    User,
    Guest
}
```

String Enum

```typescript
enum Role {
    Admin = "ADMIN",
    User = "USER"
}
```

---

# 21. Tuple

```typescript
let employee: [number, string];

employee = [101, "John"];
```

Fixed length and order.

---

# 22. Generics ⭐⭐⭐⭐⭐

Without Generics

```typescript
function identity(value: any) {
    return value;
}
```

With Generics

```typescript
function identity<T>(value: T): T {
    return value;
}
```

Usage

```typescript
identity<number>(10);

identity<string>("Hello");
```

Multiple Generics

```typescript
function pair<T, U>(first: T, second: U) {
    return { first, second };
}
```

---

# 23. Generic Interfaces

```typescript
interface ApiResponse<T> {
    data: T;
    success: boolean;
}
```

Usage

```typescript
const response: ApiResponse<User>;
```

---

# 24. keyof

```typescript
type User = {
    id: number;
    name: string;
};

type Keys = keyof User;
```

Result

```typescript
"id" | "name"
```

---

# 25. typeof

```typescript
const person = {
    name: "John",
    age: 25
};

type Person = typeof person;
```

---

# 26. Utility Types ⭐⭐⭐⭐⭐

## Partial

```typescript
interface User {
    id: number;
    name: string;
}

type UpdateUser = Partial<User>;
```

---

## Required

```typescript
type CompleteUser = Required<User>;
```

---

## Readonly

```typescript
type ReadonlyUser = Readonly<User>;
```

---

## Pick

```typescript
type BasicUser = Pick<User, "id" | "name">;
```

---

## Omit

```typescript
type UserWithoutId = Omit<User, "id">;
```

---

## Record

```typescript
type Permissions = Record<string, boolean>;

const roles: Permissions = {
    admin: true,
    editor: false
};
```

---

## Exclude

```typescript
type Result = Exclude<"A" | "B" | "C", "B">;
```

Result

```typescript
"A" | "C"
```

---

## Extract

```typescript
type Result = Extract<"A" | "B", "B" | "C">;
```

Result

```typescript
"B"
```

---

# 27. Type Narrowing

```typescript
function print(value: string | number) {

    if (typeof value === "string") {
        console.log(value.toUpperCase());
    } else {
        console.log(value.toFixed(2));
    }

}
```

---

# 28. Optional Chaining

```typescript
user?.address?.city;
```

---

# 29. Nullish Coalescing

```typescript
const username = user.name ?? "Guest";
```

Only falls back when value is `null` or `undefined`.

---

# 30. Type Assertion

```typescript
const input = document.getElementById("name") as HTMLInputElement;

input.value = "John";
```

---

# 31. Type Guards

```typescript
function print(value: string | number) {

    if (typeof value === "string") {
        console.log(value.toUpperCase());
    }

}
```

---

# 32. Optional Parameters

```typescript
function greet(name: string, age?: number) {

}
```

---

# 33. Default Parameters

```typescript
function greet(name: string = "Guest") {

}
```

---

# 34. Rest Parameters

```typescript
function sum(...numbers: number[]) {

    return numbers.reduce((a, b) => a + b, 0);

}
```

---

# 35. Generic Constraints

```typescript
function getLength<T extends { length: number }>(item: T): number {
    return item.length;
}

getLength("Hello");
getLength([1,2,3]);

// getLength(100); ❌ Error
```

---

# 36. Frequently Asked Interview Questions

## Basics

- What is TypeScript?
- Why TypeScript over JavaScript?
- What are the advantages?

---

## Types

- any vs unknown
- never vs void
- type vs interface
- Union vs Intersection
- Enum vs Literal Types

---

## Generics

- What are Generics?
- Why use Generics?
- Generic Constraints
- Generic Interfaces

---

## Utility Types

- Partial
- Required
- Readonly
- Pick
- Omit
- Record
- Exclude
- Extract

---

## Advanced

- keyof
- typeof
- Type Guards
- Type Narrowing
- Type Assertions
- Optional Chaining
- Nullish Coalescing

---

# ⭐ Most Important Topics (Senior React Interviews)

★★★★★

- Type vs Interface
- any vs unknown
- Generics
- Utility Types
- Union & Intersection Types
- Type Guards
- Type Narrowing

★★★★☆

- keyof
- typeof
- Generic Constraints
- Readonly
- Record
- Pick
- Omit

★★★☆☆

- Tuples
- Enums
- Type Inference
- Optional Chaining
- Nullish Coalescing
- Type Assertions

---

# Quick Revision (1 Minute)

- TypeScript = Statically Typed JavaScript
- `interface` → Object Shapes
- `type` → Unions, Intersections, Utility Types
- `any` → Avoid
- `unknown` → Safe alternative
- `never` → Function never returns
- `void` → Returns nothing
- `Partial` → All optional
- `Required` → All required
- `Readonly` → Immutable
- `Pick` → Select properties
- `Omit` → Remove properties
- `Record` → Key-value object
- `keyof` → Object keys
- `typeof` → Infer type from value
- `Generic` → Reusable type-safe code
- `extends` → Generic constraint
- `Union (|)` → One of many types
- `Intersection (&)` → Combine multiple types

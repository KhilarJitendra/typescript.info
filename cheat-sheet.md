---

# 🧠 TypeScript + React Cheat Sheet (Developer Edition)

# Also Why TS - Follow - https://github.com/KhilarJitendra/typescript.info/blob/main/basics/E01.md

---

# 1️⃣ Basic Types

```ts
let name: string = "Jitendra"
let age: number = 28
let isActive: boolean = true
let value: null = null
let data: undefined = undefined
```

### Arrays

```ts
let numbers: number[] = [1,2,3]

let names: Array<string> = ["A","B"]
```

---

# 2️⃣ Type Inference

TypeScript automatically detects types.

```ts
let name = "Jitendra"
```

TS understands this as:

```ts
string
```

---

# 3️⃣ Union Types

When variable can have **multiple types**

```ts
let id: string | number

id = 10
id = "abc"
```

---

# 4️⃣ Type Alias

```ts
type ID = string | number

let userId: ID
```

---

# 5️⃣ Interface

Used for **object structure**

```ts
interface User {
  id: number
  name: string
  email?: string
}
```

Optional property

```
email?
```

Usage

```ts
const user: User = {
  id: 1,
  name: "Jitendra"
}
```

---

# 6️⃣ Interface Extension

```ts
interface User {
  name: string
}

interface Admin extends User {
  role: string
}
```

---

# 7️⃣ Type vs Interface

| Feature | Type | Interface |
| ------- | ---- | --------- |
| Union   | ✅    | ❌         |
| Extend  | ⚠️   | ✅         |
| Objects | ✅    | ✅         |

Example:

```ts
type Status = "success" | "error"
```

---

# 8️⃣ Functions

### Basic

```ts
function add(a: number, b: number): number {
  return a + b
}
```

### Arrow Function

```ts
const multiply = (a:number,b:number):number => a*b
```

### Optional Parameter

```ts
function greet(name: string, age?: number) {}
```

### Default Parameter

```ts
function greet(name: string = "Guest") {}
```

---

# 9️⃣ Generics (Very Important)

Reusable types.

```ts
function identity<T>(value: T): T {
  return value
}
```

Usage

```ts
identity<string>("hello")
identity<number>(10)
```

---

# 🔟 Generic with Arrays

```ts
function getFirst<T>(arr: T[]): T {
  return arr[0]
}
```

---

# 1️⃣1️⃣ Generic Constraints

```ts
function printLength<T extends { length:number }>(arg:T){
  console.log(arg.length)
}
```

---

# 1️⃣2️⃣ Enums

```ts
enum Role {
 Admin,
 User,
 Guest
}
```

Usage

```ts
let role: Role = Role.Admin
```

Modern projects prefer:

```ts
type Role = "admin" | "user"
```

---

# 1️⃣3️⃣ keyof

Extract keys from object.

```ts
type User = {
 name:string
 age:number
}

type Keys = keyof User
```

Result

```
"name" | "age"
```

---

# 1️⃣4️⃣ Utility Types (Important)

### Partial

Makes properties optional

```ts
type UpdateUser = Partial<User>
```

---

### Pick

```ts
type UserName = Pick<User,"name">
```

---

### Omit

```ts
type UserWithoutAge = Omit<User,"age">
```

---

### Record

```ts
type Roles = Record<string,string>
```

---

# 1️⃣5️⃣ Type Assertion

```ts
let value: unknown = "Hello"

let length = (value as string).length
```

---

# 1️⃣6️⃣ Type Narrowing

```ts
function printId(id: string | number) {

 if(typeof id === "string"){
  console.log(id.toUpperCase())
 } else {
  console.log(id)
 }

}
```

---

# ⚛️ React + TypeScript Cheat Sheet

---

# 1️⃣ Component Props

```tsx
interface ButtonProps {
 title:string
 onClick:()=>void
}

const Button:React.FC<ButtonProps> = ({title,onClick})=>{
 return <button onClick={onClick}>{title}</button>
}
```

---

# 2️⃣ useState

```tsx
const [count,setCount] = useState<number>(0)
```

---

# 3️⃣ useRef

```tsx
const inputRef = useRef<HTMLInputElement>(null)
```

---

# 4️⃣ API Response Typing

```ts
interface Product {
 id:number
 name:string
 price:number
}
```

---

# 5️⃣ useReducer

```ts
type Action =
 | {type:"increment"}
 | {type:"decrement"}
```

---

# ⚡ React Event Types (Important)

React events use **SyntheticEvent**.

---

# 1️⃣ Mouse Events

```tsx
const handleClick = (e: React.MouseEvent<HTMLButtonElement>) => {
 console.log(e.currentTarget)
}
```

Events

| Event         | Type             |
| ------------- | ---------------- |
| onClick       | React.MouseEvent |
| onDoubleClick | React.MouseEvent |
| onMouseEnter  | React.MouseEvent |
| onMouseLeave  | React.MouseEvent |

---

# 2️⃣ Input Change Event

```tsx
const handleChange = (e:React.ChangeEvent<HTMLInputElement>)=>{
 console.log(e.target.value)
}
```

Used for

```
input
textarea
select
```

---

# 3️⃣ Form Submit

```tsx
const handleSubmit = (e:React.FormEvent<HTMLFormElement>)=>{
 e.preventDefault()
}
```

---

# 4️⃣ Keyboard Events

```tsx
const handleKey = (e:React.KeyboardEvent<HTMLInputElement>)=>{
 if(e.key === "Enter"){
  console.log("Enter pressed")
 }
}
```

Events

```
onKeyDown
onKeyUp
```

---

# 5️⃣ Focus Events

```tsx
const handleFocus = (e:React.FocusEvent<HTMLInputElement>)=>{
 console.log("focused")
}
```

Events

```
onFocus
onBlur
```

---

# 6️⃣ Clipboard Events

```tsx
const handlePaste = (e:React.ClipboardEvent<HTMLInputElement>)=>{
 console.log("pasted")
}
```

---

# 7️⃣ Drag Events

```tsx
const handleDrag = (e:React.DragEvent<HTMLDivElement>)=>{
 console.log("dragging")
}
```

---

# 8️⃣ Pointer Events

```tsx
const handlePointer = (e:React.PointerEvent<HTMLDivElement>)=>{
 console.log(e.pointerType)
}
```

---

# 🎯 Things Senior Frontend Engineers MUST Know

Focus on these **for interviews**:

### TypeScript

✔ Interfaces
✔ Type vs Interface
✔ Generics
✔ Utility Types
✔ Union Types
✔ keyof
✔ Type Narrowing

### React + TS

✔ Props typing
✔ useState typing
✔ API response typing
✔ Event types
✔ Custom hooks typing

---

# 🚀 Ultimate 10 Things That Impress Interviewers

1️⃣ Generics
2️⃣ Utility Types
3️⃣ keyof
4️⃣ Mapped Types
5️⃣ API typing
6️⃣ Component props typing
7️⃣ Custom hook typing
8️⃣ Event typing
9️⃣ Type guards
🔟 Advanced generics

---

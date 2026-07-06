# React + TypeScript Interview Notes

---

# 1. Typing Functional Components

```tsx
interface ButtonProps {
  title: string;
}

function Button({ title }: ButtonProps) {
  return <button>{title}</button>;
}
```

> Prefer typing the props instead of using `React.FC`.

---

# 2. React.FC vs Normal Function ⭐⭐⭐⭐

## React.FC

```tsx
const Button: React.FC<ButtonProps> = ({ title }) => {
  return <button>{title}</button>;
};
```

## Recommended

```tsx
function Button({ title }: ButtonProps) {
  return <button>{title}</button>;
}
```

### Why?

- Simpler
- Doesn't automatically include `children`
- Better generic support

---

# 3. Props Interface

```tsx
interface CardProps {
  title: string;
  description: string;
  isActive: boolean;
}

function Card(props: CardProps) {}
```

---

# 4. Optional Props

```tsx
interface ButtonProps {
  title: string;
  disabled?: boolean;
}
```

Usage

```tsx
<Button title="Save" />

<Button title="Save" disabled />
```

---

# 5. Default Props

```tsx
interface ButtonProps {
  title: string;
  variant?: "primary" | "secondary";
}

function Button({
    title,
    variant = "primary"
}: ButtonProps) {

}
```

---

# 6. Children Props

```tsx
interface LayoutProps {
    children: React.ReactNode;
}

function Layout({ children }: LayoutProps) {
    return <div>{children}</div>;
}
```

---

# 7. Event Types ⭐⭐⭐⭐⭐

Button Click

```tsx
const handleClick = (
    e: React.MouseEvent<HTMLButtonElement>
) => {

};
```

Input

```tsx
const handleChange = (
    e: React.ChangeEvent<HTMLInputElement>
) => {

    console.log(e.target.value);

};
```

Form

```tsx
const handleSubmit = (
    e: React.FormEvent<HTMLFormElement>
) => {

    e.preventDefault();

};
```

Keyboard

```tsx
const handleKeyDown = (
    e: React.KeyboardEvent<HTMLInputElement>
) => {

};
```

---

# 8. useState ⭐⭐⭐⭐⭐

Number

```tsx
const [count, setCount] =
useState<number>(0);
```

String

```tsx
const [name, setName] =
useState<string>("");
```

Object

```tsx
interface User{
    id:number;
    name:string;
}

const [user,setUser] =
useState<User>();
```

Array

```tsx
const [users,setUsers] =
useState<User[]>([]);
```

Nullable

```tsx
const [user,setUser] =
useState<User | null>(null);
```

---

# 9. useRef ⭐⭐⭐⭐⭐

Input

```tsx
const inputRef =
useRef<HTMLInputElement>(null);

inputRef.current?.focus();
```

Div

```tsx
const divRef =
useRef<HTMLDivElement>(null);
```

Timer

```tsx
const timer =
useRef<number | null>(null);
```

---

# 10. useEffect

```tsx
useEffect(() => {

    fetchUsers();

}, []);
```

No special typing required.

---

# 11. useReducer ⭐⭐⭐⭐⭐

State

```tsx
interface State{
    count:number;
}
```

Action

```tsx
type Action =
| { type:"increment" }
| { type:"decrement" };
```

Reducer

```tsx
function reducer(
    state:State,
    action:Action
){

    switch(action.type){

        case "increment":
            return {
                count:state.count+1
            };

        case "decrement":
            return {
                count:state.count-1
            };

        default:
            return state;
    }

}
```

---

# 12. Context API

```tsx
interface AuthContextType{
    user:string;
    login:()=>void;
}
```

```tsx
const AuthContext =
createContext<AuthContextType | null>(null);
```

---

# 13. API Response Types ⭐⭐⭐⭐⭐

```tsx
interface User{
    id:number;
    name:string;
}
```

```tsx
const response =
await fetch("/users");

const users:User[] =
await response.json();
```

---

# 14. Generic API Response

```tsx
interface ApiResponse<T>{

    data:T;

    success:boolean;

}
```

Usage

```tsx
const response:
ApiResponse<User[]>;
```

---

# 15. Custom Hooks ⭐⭐⭐⭐⭐

```tsx
function useFetch<T>(url:string){

}
```

Usage

```tsx
const users =
useFetch<User[]>("/users");
```

---

# 16. Forward Ref

```tsx
interface InputProps{
    placeholder:string;
}

const Input =
forwardRef<
HTMLInputElement,
InputProps
>((props,ref)=>{

    return (
        <input
            ref={ref}
            {...props}
        />
    );

});
```

---

# 17. React.memo

```tsx
interface UserProps{
    name:string;
}

const User =
React.memo(
function User({
    name
}:UserProps){

});
```

---

# 18. useCallback

```tsx
const handleClick =
useCallback(()=>{

},[]);
```

---

# 19. useMemo

```tsx
const total =
useMemo(()=>{

    return calculate();

},[]);
```

---

# 20. Typing Async Functions

```tsx
async function getUsers():
Promise<User[]>{

}
```

---

# 21. Type Assertion

```tsx
const input =
document.getElementById(
"search"
) as HTMLInputElement;
```

---

# 22. Generic Components ⭐⭐⭐⭐⭐

```tsx
interface TableProps<T>{

    data:T[];

}
```

```tsx
function Table<T>({
    data
}:TableProps<T>){

}
```

Usage

```tsx
<Table<User>
data={users}
/>
```

---

# 23. Discriminated Unions

```tsx
type Loading={
    status:"loading";
};

type Success={
    status:"success";
    data:User[];
};

type Error={
    status:"error";
    message:string;
};

type State=
Loading
| Success
| Error;
```

---

# 24. Common Interview Questions

### React.FC vs normal function?

Prefer normal function.

---

### interface vs type?

Interface for object shapes.

Type for unions and utility types.

---

### How do you type props?

Using interfaces.

---

### How do you type useState?

```tsx
const [user,setUser]=
useState<User | null>(null);
```

---

### How do you type API response?

```tsx
interface ApiResponse<T>{

    data:T;

}
```

---

### How do you type refs?

```tsx
useRef<HTMLInputElement>(null);
```

---

### How do you type events?

```tsx
React.ChangeEvent<HTMLInputElement>

React.MouseEvent<HTMLButtonElement>

React.FormEvent<HTMLFormElement>

React.KeyboardEvent<HTMLInputElement>
```

---

### How do you build reusable components?

Using Generics.

Example

```tsx
function Table<T>(){

}
```

---

# ⭐ Most Important

★★★★★

- Props
- Interfaces
- Event Types
- useState
- useRef
- API Types
- Generics
- Generic Components
- Custom Hooks
- useReducer
- Context API

★★★★☆

- ForwardRef
- React.memo
- useCallback
- useMemo
- Discriminated Unions

★★★☆☆

- React.FC
- Type Assertions
- Async Functions

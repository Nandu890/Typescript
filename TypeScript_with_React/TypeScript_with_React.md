# **🚀 TypeScript with React: A Complete Guide**

TypeScript makes React development **safer, more scalable, and easier to maintain** by adding  **static type checking** . Let’s explore how to use TypeScript effectively in a React project.

---

## **✅ 4.1 Setting Up a TypeScript React Project**

To create a React app with TypeScript:

```sh
npx create-react-app my-app --template typescript
cd my-app
npm start
```

If you're using Vite (faster alternative):

```sh
npm create vite@latest my-app --template react-ts
cd my-app
npm install
npm run dev
```

🔹 This sets up a React project with TypeScript pre-configured.

---

## **✅ 4.2 TypeScript in Functional Components**

### **1️⃣ Typing Props in a Component**

```tsx
type ButtonProps = {
    text: string;
    onClick: () => void;
};

const Button: React.FC<ButtonProps> = ({ text, onClick }) => {
    return <button onClick={onClick}>{text}</button>;
};

export default Button;
```

✅ `text` is a **string** and `onClick` is a  **function** .

---

### **2️⃣ Typing `useState`**

```tsx
import { useState } from "react";

const Counter = () => {
    const [count, setCount] = useState<number>(0);

    return (
        <div>
            <p>Count: {count}</p>
            <button onClick={() => setCount(count + 1)}>Increment</button>
        </div>
    );
};

export default Counter;
```

✅ We explicitly define the type of `count` as `number`.

---

### **3️⃣ Typing `useEffect`**

```tsx
import { useEffect, useState } from "react";

const Timer = () => {
    const [time, setTime] = useState<number>(0);

    useEffect(() => {
        const interval = setInterval(() => {
            setTime((prev) => prev + 1);
        }, 1000);

        return () => clearInterval(interval);
    }, []);

    return <p>Time: {time}s</p>;
};

export default Timer;
```

✅ TypeScript ensures `setTime` always updates with a `number`.

---

## **✅ 4.3 Handling Events with TypeScript**

### **1️⃣ Typing onClick Events**

```tsx
const handleClick = (event: React.MouseEvent<HTMLButtonElement>) => {
    console.log("Button clicked!", event);
};

<button onClick={handleClick}>Click Me</button>;
```

✅ The `event` is strictly typed as `MouseEvent`.

---

### **2️⃣ Typing Input Change Events**

```tsx
const handleChange = (event: React.ChangeEvent<HTMLInputElement>) => {
    console.log(event.target.value);
};

<input type="text" onChange={handleChange} />;
```

✅ Ensures `event.target.value` is always a `string`.

---

## **✅ 4.4 Typing Components with Children**

### **1️⃣ Passing React Nodes as Children**

```tsx
type CardProps = {
    children: React.ReactNode;
};

const Card: React.FC<CardProps> = ({ children }) => {
    return <div className="card">{children}</div>;
};

export default Card;
```

✅ `React.ReactNode` ensures any valid JSX can be passed as children.

---

## **✅ 4.5 Typing Props with `interface` vs `type`**

Both `interface` and `type` can be used for defining props.

### **1️⃣ Using `interface`**

```tsx
interface UserProps {
    name: string;
    age: number;
}

const User: React.FC<UserProps> = ({ name, age }) => {
    return <p>{name} is {age} years old.</p>;
};
```

### **2️⃣ Using `type` (Recommended for Complex Types)**

```tsx
type UserProps = {
    name: string;
    age: number;
};

const User: React.FC<UserProps> = ({ name, age }) => {
    return <p>{name} is {age} years old.</p>;
};
```

✅ **Use `interface` for object structures** and  **`type` for unions and complex types** .

---

## **✅ 4.6 Typing `useReducer`**

`useReducer` is great for managing complex state in React.

```tsx
type State = { count: number };
type Action = { type: "increment" | "decrement" };

const reducer = (state: State, action: Action): State => {
    switch (action.type) {
        case "increment":
            return { count: state.count + 1 };
        case "decrement":
            return { count: state.count - 1 };
        default:
            return state;
    }
};

const Counter = () => {
    const [state, dispatch] = useReducer(reducer, { count: 0 });

    return (
        <div>
            <p>Count: {state.count}</p>
            <button onClick={() => dispatch({ type: "increment" })}>+</button>
            <button onClick={() => dispatch({ type: "decrement" })}>-</button>
        </div>
    );
};

export default Counter;
```

✅ Ensures `state` and `dispatch` always have expected types.

---

## **✅ 4.7 Typing API Calls (`fetch`)**

```tsx
type Post = { id: number; title: string; body: string };

const [posts, setPosts] = useState<Post[]>([]);

useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/posts")
        .then((res) => res.json())
        .then((data: Post[]) => setPosts(data));
}, []);
```

✅ TypeScript ensures the API response matches the `Post` type.

---

## **✅ 4.8 Typing Context API**

```tsx
type Theme = "light" | "dark";

const ThemeContext = createContext<Theme>("light");

const ThemeProvider: React.FC<{ children: React.ReactNode }> = ({ children }) => {
    const [theme, setTheme] = useState<Theme>("light");

    return (
        <ThemeContext.Provider value={theme}>
            {children}
        </ThemeContext.Provider>
    );
};
```

✅ The context is strongly typed as `"light" | "dark"`.

---

## **✅ 4.9 Typing Higher-Order Components (HOCs)**

HOCs wrap components for  **code reuse** .

```tsx
function withBorder<T extends {}>(Component: React.ComponentType<T>) {
    return (props: T) => (
        <div style={{ border: "1px solid black", padding: "10px" }}>
            <Component {...props} />
        </div>
    );
}

const Hello = ({ name }: { name: string }) => <h1>Hello, {name}!</h1>;

const HelloWithBorder = withBorder(Hello);
```

✅ Ensures `Component` retains its original props.

---

## **🚀 What’s Next?**

Now that you know  **TypeScript with React** , you can:

1. **Build scalable React apps with TypeScript.**
2. **Use TypeScript in Redux, React Query, and Next.js.**
3. **Explore Design Patterns in TypeScript.**

Would you like to dive into  **Redux with TypeScript** ,  **Next.js** , or **real-world project ideas** next? 😊

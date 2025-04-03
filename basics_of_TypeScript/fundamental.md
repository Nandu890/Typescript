## **🚀 TypeScript Basics**

### **🔹 1.1 What is TypeScript?**

TypeScript is a **superset of JavaScript** that adds  **static typing** . It helps catch errors  **at compile time** , making your code **safer** and  **easier to maintain** .

✅ **Why Use TypeScript?**

* **Type Safety:** Catches errors before runtime.
* **Better Code Completion & IntelliSense.**
* **Object-Oriented Programming (OOP) Support.**
* **Easier Refactoring & Scalability.**

---

## **✅ 1.2 Setting Up TypeScript**

### **1️⃣ Install TypeScript Globally**

```sh
npm install -g typescript
```

🔹 Check if it's installed:

```sh
tsc --version
```

### **2️⃣ Initialize a TypeScript Project**

Inside your project folder, run:

```sh
tsc --init
```

This creates a `tsconfig.json` file, where you can configure TypeScript settings.

### **3️⃣ Compile TypeScript to JavaScript**

Write TypeScript in a `.ts` file and compile it using:

```sh
tsc filename.ts
```

This generates a `.js` file that can run in browsers or Node.js.

---

## **✅ 1.3 Basic Types in TypeScript**

TypeScript provides **strict typing** for better safety.

### **1️⃣ Primitive Types**

```ts
let username: string = "Alice";
let age: number = 25;
let isDeveloper: boolean = true;
```

### **2️⃣ Arrays & Tuples**

```ts
let numbers: number[] = [1, 2, 3, 4]; // Array of numbers
let user: [string, number] = ["Alice", 25]; // Tuple (fixed length)
```

### **3️⃣ Union Types (Multiple Allowed Types)**

```ts
let id: string | number;
id = 123; // ✅
id = "ABC"; // ✅
```

### **4️⃣ Any & Unknown Types**

```ts
let data: any = 10; // Avoid using `any`, as it removes type safety
let value: unknown = "Hello"; // `unknown` is safer than `any`
```

---

## **✅ 1.4 Functions & Type Annotations**

TypeScript allows defining the  **types of parameters and return values** .

### **1️⃣ Function with Parameters & Return Type**

```ts
function add(a: number, b: number): number {
    return a + b;
}
console.log(add(5, 3)); // Output: 8
```

### **2️⃣ Optional & Default Parameters**

```ts
function greet(name: string, age?: number): string {
    return `Hello, ${name}, Age: ${age ?? "Unknown"}`;
}
console.log(greet("Alice")); // Output: Hello, Alice, Age: Unknown
```

### **3️⃣ Arrow Functions**

```ts
const multiply = (x: number, y: number): number => x * y;
console.log(multiply(4, 5)); // Output: 20
```

---

## **✅ 1.5 Objects & Interfaces**

Interfaces define the **structure** of an object.

```ts
interface User {
    name: string;
    age: number;
    isAdmin?: boolean; // Optional property
}

const user1: User = { name: "Alice", age: 25 };
console.log(user1.name); // Output: Alice
```

---

## **✅ 1.6 Type Aliases & Enums**

### **1️⃣ Type Aliases**

```ts
type ID = string | number; // Can be string or number
let userID: ID = "abc123";
```

### **2️⃣ Enums**

Enums are used for defining a set of  **named constants** .

```ts
enum Role {
    Admin,
    User,
    Guest
}

let userRole: Role = Role.Admin;
console.log(userRole); // Output: 0 (Enums start from index 0 by default)
```

---

## **✅ 1.7 TypeScript Compiler Options (`tsconfig.json`)**

Some important options in `tsconfig.json`:

```json
{
  "compilerOptions": {
    "target": "ES6",   // JavaScript version to compile to
    "strict": true,    // Enable strict type checking
    "noImplicitAny": true, // Prevents use of `any`
    "outDir": "./dist" // Output folder for compiled JS
  }
}
```

---

## **🚀 What’s Next?**


1. **Practice by converting JavaScript projects into TypeScript.**
2. **Move to Advanced TypeScript topics:**
   * **Interfaces & Generics**
   * **OOP in TypeScript**
   * **Type Guards & Utility Types**

# **🚀 Advanced TypeScript Concepts**

  **TypeScript basics** , let's explore more advanced concepts to make your code  **scalable, reusable, and maintainable** .

---

## **✅ 2.1 Interfaces & Type Aliases**

Both **interfaces** and **type aliases** define the shape of objects, but they have some differences.

### **1️⃣ Interfaces (Recommended for Object Structures)**

```ts
interface User {
    name: string;
    age: number;
    isAdmin?: boolean; // Optional property
}

const user1: User = { name: "Alice", age: 25 };
```

✅ Interfaces can be  **extended** :

```ts
interface Employee extends User {
    salary: number;
}

const emp: Employee = { name: "Bob", age: 30, salary: 50000 };
```

---

### **2️⃣ Type Aliases (Recommended for Unions & Tuples)**

```ts
type ID = string | number; // Can be string or number
let userID: ID = "abc123";
```

✅ Type aliases can also be **used for objects** (like interfaces):

```ts
type Product = { name: string; price: number };
const item: Product = { name: "Laptop", price: 1000 };
```

🔹 **Interfaces are preferred** for objects, while **type aliases are better for unions & complex types.**

---

## **✅ 2.2 Generics (Reusable Code with Types)**

Generics allow you to create **functions, interfaces, and classes** that work with any type.

### **1️⃣ Generic Function**

```ts
function identity<T>(value: T): T {
    return value;
}

console.log(identity<string>("Hello")); // Output: Hello
console.log(identity<number>(10));      // Output: 10
```

🔹 The `<T>` syntax defines a  **generic type parameter** .

---

### **2️⃣ Generic Interfaces**

```ts
interface Box<T> {
    content: T;
}

const stringBox: Box<string> = { content: "Books" };
const numberBox: Box<number> = { content: 123 };
```

---

### **3️⃣ Generic Constraints**

You can restrict generics using `extends`.

```ts
function getLength<T extends { length: number }>(item: T): number {
    return item.length;
}

console.log(getLength("Hello")); // ✅ Works (string has length)
console.log(getLength([1, 2, 3])); // ✅ Works (array has length)
// console.log(getLength(10)); // ❌ Error: number does not have length
```

---

## **✅ 2.3 Utility Types (Built-in Type Helpers)**

TypeScript provides **utility types** to modify and reuse existing types.

### **1️⃣ `Partial<T>` (Make Properties Optional)**

```ts
interface User {
    name: string;
    age: number;
}

const updateUser: Partial<User> = { age: 26 }; // Only updating age
```

### **2️⃣ `Readonly<T>` (Prevent Modifications)**

```ts
const user: Readonly<User> = { name: "Alice", age: 25 };
// user.age = 26; // ❌ Error: Cannot modify readonly property
```

### **3️⃣ `Pick<T, K>` (Select Specific Properties)**

```ts
type UserName = Pick<User, "name">; // Only keeps `name`
```

### **4️⃣ `Omit<T, K>` (Remove Specific Properties)**

```ts
type UserWithoutAge = Omit<User, "age">; // Removes `age`
```

### **5️⃣ `Record<K, T>` (Create an Object Type with Fixed Keys)**

```ts
type Roles = "admin" | "user" | "guest";
type RolePermissions = Record<Roles, boolean>;

const permissions: RolePermissions = { admin: true, user: false, guest: false };
```

---

## **✅ 2.4 Type Guards (Check Types at Runtime)**

Since TypeScript types  **don’t exist at runtime** , **type guards** help  **determine types dynamically** .

### **1️⃣ `typeof` for Primitives**

```ts
function logValue(value: string | number) {
    if (typeof value === "string") {
        console.log("String:", value.toUpperCase());
    } else {
        console.log("Number:", value.toFixed(2));
    }
}
```

### **2️⃣ `instanceof` for Objects**

```ts
class Car {
    drive() { console.log("Driving a car"); }
}
class Bike {
    ride() { console.log("Riding a bike"); }
}

function useVehicle(vehicle: Car | Bike) {
    if (vehicle instanceof Car) {
        vehicle.drive();
    } else {
        vehicle.ride();
    }
}
```

### **3️⃣ Custom Type Predicates (`is`)**

```ts
interface Dog { bark: () => void; }
interface Cat { meow: () => void; }

function isDog(animal: Dog | Cat): animal is Dog {
    return (animal as Dog).bark !== undefined;
}

function makeSound(animal: Dog | Cat) {
    if (isDog(animal)) {
        animal.bark();
    } else {
        animal.meow();
    }
}
```

---

## **✅ 2.5 Advanced Object-Oriented Programming (OOP)**

### **1️⃣ Classes & Inheritance**

```ts
class Person {
    constructor(public name: string, protected age: number) {}

    greet() {
        console.log(`Hello, my name is ${this.name}`);
    }
}

class Employee extends Person {
    constructor(name: string, age: number, private salary: number) {
        super(name, age);
    }

    getSalary() {
        return this.salary;
    }
}
```

* `public`: Accessible everywhere.
* `private`: Only accessible inside the class.
* `protected`: Accessible inside the class and subclasses.

---

### **2️⃣ Abstract Classes (Blueprints for Classes)**

```ts
abstract class Animal {
    abstract makeSound(): void; // Must be implemented in subclasses
}

class Dog extends Animal {
    makeSound() { console.log("Bark!"); }
}
```

---

## **✅ 2.6 Advanced Asynchronous Programming**

TypeScript fully supports **async/await** and  **Promises** .

### **1️⃣ Promise with Type Safety**

```ts
function fetchData(): Promise<string> {
    return new Promise((resolve) => {
        setTimeout(() => resolve("Data loaded"), 2000);
    });
}

fetchData().then(data => console.log(data));
```

### **2️⃣ Async/Await**

```ts
async function fetchDataAsync(): Promise<void> {
    const data = await fetchData();
    console.log(data);
}
fetchDataAsync();
```

---

## **✅ 2.7 TypeScript with React**

### **1️⃣ Props & State in Functional Components**

```tsx
type ButtonProps = { text: string };

const Button: React.FC<ButtonProps> = ({ text }) => {
    return <button>{text}</button>;
};
```

### **2️⃣ Using TypeScript with `useState`**

```tsx
const [count, setCount] = useState<number>(0);
```

---

## **🚀 What’s Next?**

1. **Apply these concepts in real-world projects.**
2. **Move to TypeScript with React, Node.js, and API Development.**
3. **Build a TypeScript-based full-stack app.**

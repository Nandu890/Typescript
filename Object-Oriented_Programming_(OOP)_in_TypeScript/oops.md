# **🚀 Object-Oriented Programming (OOP) in TypeScript**

Object-Oriented Programming (OOP) in TypeScript helps organize code using  **classes, objects, inheritance, and encapsulation** . TypeScript extends JavaScript’s class system with **strong typing** and additional features.

---

## **✅ 3.1 Classes & Objects**

A **class** is a blueprint for creating objects.

### **1️⃣ Defining a Basic Class**

```ts
class Person {
    name: string;
    age: number;

    constructor(name: string, age: number) {
        this.name = name;
        this.age = age;
    }

    greet() {
        console.log(`Hello, my name is ${this.name}`);
    }
}

const person1 = new Person("Alice", 25);
person1.greet(); // Output: Hello, my name is Alice
```

---

## **✅ 3.2 Access Modifiers**

TypeScript provides **modifiers** to control access to class properties and methods.

| Modifier      | Description                             |
| ------------- | --------------------------------------- |
| `public`    | Accessible from anywhere (default).     |
| `private`   | Accessible only inside the class.       |
| `protected` | Accessible in the class and subclasses. |

### **1️⃣ Example: Using Modifiers**

```ts
class Employee {
    public name: string; 
    private salary: number;
    protected department: string;

    constructor(name: string, salary: number, department: string) {
        this.name = name;
        this.salary = salary;
        this.department = department;
    }

    public showSalary() {
        console.log(`Salary: ${this.salary}`); // ✅ Allowed inside class
    }
}

const emp = new Employee("Bob", 5000, "IT");
console.log(emp.name);  // ✅ Public, accessible
// console.log(emp.salary); ❌ Error: Private property
// console.log(emp.department); ❌ Error: Protected property
```

---

## **✅ 3.3 Readonly Properties**

A `readonly` property **cannot be modified** after initialization.

```ts
class Car {
    readonly brand: string;
    constructor(brand: string) {
        this.brand = brand;
    }
}

const myCar = new Car("Toyota");
// myCar.brand = "Honda"; ❌ Error: Cannot modify readonly property
```

---

## **✅ 3.4 Getters & Setters**

`get` and `set` methods allow controlled access to class properties.

```ts
class User {
    private _password: string = "";

    get password(): string {
        return "****"; // Always return masked value
    }

    set password(newPassword: string) {
        if (newPassword.length >= 6) {
            this._password = newPassword;
        } else {
            console.log("Password too short!");
        }
    }
}

const user = new User();
user.password = "12345"; // Output: Password too short!
user.password = "strongpassword";
console.log(user.password); // Output: ****
```

---

## **✅ 3.5 Inheritance (Extending a Class)**

`extends` allows a class to inherit properties and methods from another class.

```ts
class Animal {
    constructor(public name: string) {}

    makeSound() {
        console.log("Some sound...");
    }
}

class Dog extends Animal {
    constructor(name: string, public breed: string) {
        super(name); // Call parent constructor
    }

    makeSound() {
        console.log("Bark! Bark!");
    }
}

const dog = new Dog("Buddy", "Labrador");
dog.makeSound(); // Output: Bark! Bark!
```

---

## **✅ 3.6 Abstract Classes (Blueprints for Classes)**

An **abstract class** cannot be instantiated and is meant to be  **extended** .

```ts
abstract class Shape {
    abstract getArea(): number; // Abstract method (must be implemented in subclasses)

    showType() {
        console.log("This is a shape.");
    }
}

class Circle extends Shape {
    constructor(public radius: number) {
        super();
    }

    getArea(): number {
        return Math.PI * this.radius * this.radius;
    }
}

const circle = new Circle(5);
console.log(circle.getArea()); // Output: 78.54
```

🔹 **Abstract classes allow defining structure without implementation.**

🔹 **All subclasses must implement the abstract methods.**

---

## **✅ 3.7 Interfaces vs. Abstract Classes**

| Feature                | Interface                                    | Abstract Class                                |
| ---------------------- | -------------------------------------------- | --------------------------------------------- |
| Can have properties?   | ✅ Yes                                       | ✅ Yes                                        |
| Can have methods?      | ✅ Only method signatures                    | ✅ Both implemented and abstract methods      |
| Supports constructors? | ❌ No                                        | ✅ Yes                                        |
| Multiple inheritance?  | ✅ A class can implement multiple interfaces | ❌ A class can extend only one abstract class |

Example using an  **interface** :

```ts
interface Vehicle {
    speed: number;
    move(): void;
}

class Bike implements Vehicle {
    speed = 60;
    move() {
        console.log(`Moving at speed ${this.speed}`);
    }
}
```

---

## **✅ 3.8 Static Properties & Methods**

`static` members belong to the class itself, not instances.

```ts
class MathUtils {
    static PI = 3.14;

    static add(a: number, b: number): number {
        return a + b;
    }
}

console.log(MathUtils.PI); // Output: 3.14
console.log(MathUtils.add(5, 3)); // Output: 8
```

---

## **✅ 3.9 Polymorphism (Method Overriding)**

A **subclass** can override methods from a  **parent class** .

```ts
class Animal {
    makeSound() {
        console.log("Some generic sound");
    }
}

class Cat extends Animal {
    makeSound() {
        console.log("Meow!");
    }
}

const cat = new Cat();
cat.makeSound(); // Output: Meow!
```

---

## **✅ 3.10 Dependency Injection (Using OOP in Large Applications)**

Large applications use **Dependency Injection (DI)** to make classes  **loosely coupled** .

```ts
interface Logger {
    log(message: string): void;
}

class ConsoleLogger implements Logger {
    log(message: string) {
        console.log(message);
    }
}

class App {
    constructor(private logger: Logger) {}

    run() {
        this.logger.log("App is running...");
    }
}

const logger = new ConsoleLogger();
const app = new App(logger);
app.run(); // Output: App is running...
```

🔹  **Advantage** : The `App` class doesn’t depend on a specific logging implementation.

---

## **🚀 What’s Next?**

Now that you’ve mastered  **OOP in TypeScript** , you can:

1. **Apply OOP concepts in real-world projects.**
2. **Use TypeScript with frameworks like React, Angular, or Node.js.**
3. **Learn Design Patterns in TypeScript.**

Would you like to explore **real-world OOP projects** or dive into **TypeScript with React/Node.js** next? 😊


---

**TypeScript Deep Dive: Key Concepts Explained**

TypeScript has become a key tool in modern web development, enhancing JavaScript with strong typing and better tooling. Below are four important TypeScript concepts every developer should understand.

---

**1. Interfaces vs. Types in TypeScript: What’s the Difference?**

Both `interface` and `type` are used to define the shape of data, especially objects, but they have key differences:

**Interfaces**

* Primarily used for object shapes
* Can be extended using `extends`
* Can be implemented in classes using `implements`
* Support declaration merging (multiple interfaces with the same name are combined)

Example:

```typescript
interface User {
  name: string;
  age: number;
}

interface Admin extends User {
  role: string;
}
```

**Types**

* More flexible: can define unions, intersections, primitives, tuples, etc.
* Use `&` for intersections
* Do not support declaration merging like interfaces

Example:

```typescript
type ID = string | number;

type Employee = {
  id: ID;
  department: string;
} & User;
```

**When to use which?**

* Use `interface` when working with object-oriented designs or classes
* Use `type` for advanced compositions like unions and intersections

---

**2. The `keyof` Keyword: Accessing Object Keys Dynamically**

`keyof` creates a union of an object’s keys. It helps enforce type-safe dynamic property access.

Example:

```typescript
interface Person {
  name: string;
  age: number;
  location: string;
}

type PersonKeys = keyof Person; // "name" | "age" | "location"

function getProperty(obj: Person, key: PersonKeys) {
  return obj[key];
}

const person = { name: "Alice", age: 30, location: "NY" };
console.log(getProperty(person, "name")); // Works
// console.log(getProperty(person, "email")); // Error
```

**Use cases:**

* Safe access to object properties
* Utility types like `Pick`, `Record`, etc.

---

**3. `any`, `unknown`, and `never`: Special Types in TypeScript**

**`any`**

* Turns off type checking
* Can hold any value, but is unsafe

Example:

```typescript
let data: any = "Hello";
data = 42;
data.someMethod(); // No error, even if it doesn’t exist
```

**`unknown`**

* Safer version of `any`
* Requires type checking before use

Example:

```typescript
let input: unknown = getValue();

if (typeof input === "string") {
  console.log(input.toUpperCase());
}
```

**`never`**

* Used for functions that never return
* Often seen in error throwing or infinite loops

Example:

```typescript
function throwError(msg: string): never {
  throw new Error(msg);
}
```

**Key points:**

* Use `unknown` instead of `any` for safety
* Use `never` for unreachable code

---

**4. Enums in TypeScript: Numeric vs. String**

Enums define a set of named constants.

**Numeric Enums**

* Automatically assigned numbers starting from 0

Example:

```typescript
enum Direction {
  Up,    // 0
  Down,  // 1
  Left,  // 2
  Right  // 3
}

console.log(Direction.Up); // 0
```

**String Enums**

* You provide explicit string values

Example:

```typescript
enum LogLevel {
  Error = "ERROR",
  Warn = "WARN",
  Info = "INFO"
}

console.log(LogLevel.Error); // "ERROR"
```

**When to use enums:**

* When a variable should only have a few predefined values
* String enums are easier to debug and read

---

**Conclusion**

By mastering these TypeScript concepts—interfaces vs. types, the `keyof` operator, special types (`any`, `unknown`, `never`), and enums—you'll be able to write safer, cleaner, and more powerful TypeScript code.


# TypeScript Mülakat Soruları ve Cevapları

## Temel Sorular

### 1. TypeScript nedir ve JavaScript'ten farkları nelerdir?

**Cevap:** TypeScript, JavaScript'in üzerine inşa edilmiş, statik tip desteği sunan bir programlama dilidir. Temel farkları:

- Static typing
- OOP özellikleri (interface, enum, generics)
- Compile-time type checking
- IDE desteği ve intellisense
- ECMAScript features

### 2. Type vs Interface farkı nedir?

**Cevap:**

```typescript
// Type
type User = {
  id: number;
  name: string;
};

type Admin = User & {
  role: string;
};

// Interface
interface User {
  id: number;
  name: string;
}

interface Admin extends User {
  role: string;
}
```

### 3. TypeScript'te type assertion nasıl yapılır?

**Cevap:**

```typescript
// Angle bracket syntax
let someValue: any = "this is a string";
let strLength: number = (<string>someValue).length;

// as syntax
let someValue: any = "this is a string";
let strLength: number = (someValue as string).length;
```

### 4. Union ve Intersection Types nedir?

**Cevap:**

```typescript
// Union Types
type StringOrNumber = string | number;
let value: StringOrNumber = "hello"; // veya 42

// Intersection Types
type Employee = Person & {
  employeeId: number;
  department: string;
};
```

## Orta Seviye Sorular

### 5. Generics nasıl kullanılır?

**Cevap:**

```typescript
// Generic function
function identity<T>(arg: T): T {
  return arg;
}

// Generic interface
interface Collection<T> {
  add(item: T): void;
  remove(item: T): void;
  items(): T[];
}

// Generic class
class Queue<T> {
  private data: T[] = [];
  push(item: T) {
    this.data.push(item);
  }
  pop(): T | undefined {
    return this.data.shift();
  }
}
```

### 6. Utility Types nelerdir?

**Cevap:**

```typescript
interface User {
  id: number;
  name: string;
  email: string;
}

// Partial
type PartialUser = Partial<User>;

// Pick
type UserBasics = Pick<User, "id" | "name">;

// Omit
type UserWithoutEmail = Omit<User, "email">;

// Record
type UserRoles = Record<string, User>;

// Required
type RequiredUser = Required<PartialUser>;
```

### 7. Decorators nasıl kullanılır?

**Cevap:**

```typescript
// Class decorator
function logger(target: any) {
  console.log(`Class ${target.name} was created`);
}

@logger
class Example {
  constructor() {}
}

// Property decorator
function required(target: any, propertyKey: string) {
  let value = target[propertyKey];

  const getter = () => value;
  const setter = (newVal: any) => {
    if (!newVal) {
      throw new Error(`${propertyKey} is required`);
    }
    value = newVal;
  };

  Object.defineProperty(target, propertyKey, {
    get: getter,
    set: setter,
    enumerable: true,
    configurable: true,
  });
}
```

## İleri Seviye Sorular

### 8. Type Guards nasıl kullanılır?

**Cevap:**

```typescript
// Type predicate
function isString(value: any): value is string {
  return typeof value === "string";
}

// instanceof
function processValue(value: string | Date) {
  if (value instanceof Date) {
    return value.toISOString();
  }
  return value.toUpperCase();
}

// in operator
interface Dog {
  bark(): void;
}
interface Cat {
  meow(): void;
}

function makeSound(animal: Dog | Cat) {
  if ("bark" in animal) {
    animal.bark();
  } else {
    animal.meow();
  }
}
```

### 9. Conditional Types nasıl kullanılır?

**Cevap:**

```typescript
type IsString<T> = T extends string ? true : false;

type A = IsString<string>; // true
type B = IsString<number>; // false

// Infer keyword
type ReturnType<T> = T extends (...args: any[]) => infer R ? R : any;

function foo(): number {
  return 42;
}

type FooReturn = ReturnType<typeof foo>; // number
```

### 10. Mapped Types nasıl kullanılır?

**Cevap:**

```typescript
type Readonly<T> = {
  readonly [P in keyof T]: T[P];
};

type Optional<T> = {
  [P in keyof T]?: T[P];
};

type Nullable<T> = {
  [P in keyof T]: T[P] | null;
};

interface User {
  id: number;
  name: string;
}

type ReadonlyUser = Readonly<User>;
type OptionalUser = Optional<User>;
type NullableUser = Nullable<User>;
```

### 11. Module Augmentation nasıl yapılır?

**Cevap:**

```typescript
// Existing module
declare module "express" {
  interface Request {
    user?: {
      id: number;
      name: string;
    };
  }
}

// Usage
app.get("/", (req: Request) => {
  console.log(req.user?.name);
});
```

### 12. Project Configuration

**Cevap:**

```json
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "commonjs",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "outDir": "./dist",
    "rootDir": "./src",
    "declaration": true,
    "experimentalDecorators": true
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules", "**/*.spec.ts"]
}
```

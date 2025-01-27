# Testing Mülakat Soruları ve Cevapları

## Temel Sorular

### 1. Test türleri nelerdir?

**Cevap:**

- Unit Testing: En küçük kod birimlerinin testi
- Integration Testing: Birimlerin birlikte çalışmasının testi
- E2E Testing: Kullanıcı perspektifinden tüm uygulamanın testi
- Functional Testing: Fonksiyonların beklenen davranışlarının testi
- Performance Testing: Performans metriklerinin testi

### 2. Jest nedir ve temel özellikleri nelerdir?

**Cevap:**

```javascript
// Test Suite
describe("Calculator", () => {
  // Test Case
  test("adds 1 + 2 to equal 3", () => {
    expect(add(1, 2)).toBe(3);
  });

  // Matchers
  test("object assignment", () => {
    const data = { one: 1 };
    expect(data).toEqual({ one: 1 });
  });
});

// Setup ve Teardown
beforeEach(() => {
  // Her testten önce çalışır
});

afterEach(() => {
  // Her testten sonra çalışır
});
```

### 3. React Testing Library nasıl kullanılır?

**Cevap:**

```javascript
import { render, screen, fireEvent } from "@testing-library/react";

test("shows the children when the checkbox is checked", () => {
  const testMessage = "Test Message";
  render(<Toggle>{testMessage}</Toggle>);

  // Element bulma
  const checkbox = screen.getByRole("checkbox");
  const content = screen.getByText(testMessage);

  // Event tetikleme
  fireEvent.click(checkbox);

  // Assertion
  expect(content).toBeVisible();
});
```

### 4. Mock functions nasıl kullanılır?

**Cevap:**

```javascript
// Jest mock function
const mockCallback = jest.fn((x) => 42 + x);
forEach([0, 1], mockCallback);

expect(mockCallback.mock.calls.length).toBe(2);
expect(mockCallback.mock.results[0].value).toBe(42);

// API mock
jest.mock("axios");
test("fetches data", async () => {
  const data = { id: 1, name: "John" };
  axios.get.mockResolvedValue({ data });

  const result = await fetchData();
  expect(result).toEqual(data);
});
```

## Orta Seviye Sorular

### 5. Cypress ile E2E testing nasıl yapılır?

**Cevap:**

```javascript
describe("Login Flow", () => {
  beforeEach(() => {
    cy.visit("/login");
  });

  it("should login successfully", () => {
    cy.get("[data-testid=email]").type("user@example.com");
    cy.get("[data-testid=password]").type("password123");
    cy.get("[data-testid=submit]").click();

    cy.url().should("include", "/dashboard");
    cy.get("[data-testid=welcome]").should("contain", "Welcome");
  });

  it("should show error for invalid credentials", () => {
    cy.get("[data-testid=email]").type("invalid@example.com");
    cy.get("[data-testid=password]").type("wrong");
    cy.get("[data-testid=submit]").click();

    cy.get("[data-testid=error]").should("be.visible");
  });
});
```

### 6. Test Coverage nasıl ölçülür ve artırılır?

**Cevap:**

```javascript
// Jest configuration
module.exports = {
  collectCoverage: true,
  coverageThreshold: {
    global: {
      branches: 80,
      functions: 80,
      lines: 80,
      statements: 80,
    },
  },
  collectCoverageFrom: [
    "src/**/*.{js,jsx}",
    "!src/index.js",
    "!src/serviceWorker.js",
  ],
};

// Test örneği
describe("User service", () => {
  it("should cover all branches", () => {
    expect(validateUser({ name: "John" })).toBe(false);
    expect(validateUser({ name: "John", age: 20 })).toBe(true);
    expect(validateUser({ name: "John", age: 15 })).toBe(false);
  });
});
```

### 7. Integration Tests nasıl yazılır?

**Cevap:**

```javascript
describe("TodoList Integration", () => {
  it("should add and complete todo", async () => {
    const { getByText, getByTestId } = render(<TodoApp />);

    // Add todo
    fireEvent.change(getByTestId("todo-input"), {
      target: { value: "New Todo" },
    });
    fireEvent.click(getByText("Add"));

    // Verify todo is added
    expect(getByText("New Todo")).toBeInTheDocument();

    // Complete todo
    fireEvent.click(getByTestId("todo-checkbox"));

    // Verify todo is completed
    expect(getByText("New Todo")).toHaveStyle({
      textDecoration: "line-through",
    });
  });
});
```

## İleri Seviye Sorular

### 8. Test Driven Development (TDD) nedir?

**Cevap:**

```javascript
// 1. Önce test yaz (Red)
test("should calculate total with discount", () => {
  const cart = new ShoppingCart();
  cart.addItem({ price: 100 });
  cart.applyDiscount(10);

  expect(cart.getTotal()).toBe(90);
});

// 2. Minimum kod yaz (Green)
class ShoppingCart {
  constructor() {
    this.items = [];
    this.discount = 0;
  }

  addItem(item) {
    this.items.push(item);
  }

  applyDiscount(percentage) {
    this.discount = percentage;
  }

  getTotal() {
    const subtotal = this.items.reduce((sum, item) => sum + item.price, 0);
    return subtotal * (1 - this.discount / 100);
  }
}

// 3. Refactor
```

### 9. Performance Testing nasıl yapılır?

**Cevap:**

```javascript
// Jest Timer Mocks
jest.useFakeTimers();

test("debounce function", () => {
  const func = jest.fn();
  const debouncedFunc = debounce(func, 1000);

  debouncedFunc();
  debouncedFunc();
  debouncedFunc();

  expect(func).not.toBeCalled();

  jest.runAllTimers();

  expect(func).toBeCalledTimes(1);
});

// Load Testing with k6
import http from "k6/http";
import { check, sleep } from "k6";

export default function () {
  const res = http.get("http://test.k6.io");
  check(res, {
    "status is 200": (r) => r.status === 200,
    "response time < 200ms": (r) => r.timings.duration < 200,
  });
  sleep(1);
}
```

### 10. Snapshot Testing nasıl yapılır?

**Cevap:**

```javascript
import renderer from "react-test-renderer";

it("renders correctly", () => {
  const tree = renderer.create(<Button text="Test" />).toJSON();
  expect(tree).toMatchSnapshot();
});

// Update snapshots
// jest --updateSnapshot

// Interactive mode
// jest --watch
```

### 11. Custom Test Matchers nasıl yazılır?

**Cevap:**

```javascript
expect.extend({
  toBeWithinRange(received, floor, ceiling) {
    const pass = received >= floor && received <= ceiling;
    if (pass) {
      return {
        message: () =>
          `expected ${received} not to be within range ${floor} - ${ceiling}`,
        pass: true,
      };
    } else {
      return {
        message: () =>
          `expected ${received} to be within range ${floor} - ${ceiling}`,
        pass: false,
      };
    }
  },
});

test("numeric ranges", () => {
  expect(100).toBeWithinRange(90, 110);
  expect(101).not.toBeWithinRange(0, 100);
});
```

### 12. Test Doubles (Stubs, Spies, Mocks) nasıl kullanılır?

**Cevap:**

```javascript
// Spy
const spy = jest.spyOn(console, "log");
expect(spy).toHaveBeenCalledWith("test");
spy.mockRestore();

// Stub
const stub = jest.fn().mockImplementation(() => 42);
expect(stub()).toBe(42);

// Mock
jest.mock("./database", () => ({
  query: jest.fn().mockResolvedValue([{ id: 1 }]),
}));

test("database query", async () => {
  const results = await database.query("SELECT * FROM users");
  expect(results).toEqual([{ id: 1 }]);
});
```

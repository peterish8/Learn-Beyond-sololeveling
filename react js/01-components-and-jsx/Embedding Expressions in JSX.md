## 📌 Embedding Expressions in JSX

> [!SUCCESS] **Definition**: Use curly braces `{}` to embed JavaScript in JSX.
> **Recall**: Anything inside `{}` is evaluated as JavaScript! 🎯

---

## 🎯 **The Curly Braces `{}`**

> **Goal**: Display dynamic data in JSX using curly braces

```jsx
const name = "Alice";
const element = <h1>Hello, {name}!</h1>;

// USAGE EXAMPLE
// Expected Output: <h1>Hello, Alice!</h1>
```

---

## 📐 **What Can You Embed?**

### 1. Variables

> **Goal**: Display username and age from variables

```jsx
const username = "john_doe";
const age = 25;

function UserInfo() {
  return (
    <div>
      <p>Username: {username}</p>
      <p>Age: {age}</p>
    </div>
  );
}

// USAGE EXAMPLE
// <UserInfo />
// Expected: Username: john_doe, Age: 25
```

---

### 2. Math Operations

> **Goal**: Calculate total price with tax

```jsx
const price = 100;
const tax = 0.1;

function PriceTag() {
  return <p>Total: ${price + (price * tax)}</p>;
}

// USAGE EXAMPLE
// <PriceTag />
// Expected: Total: $110
```

---

### 3. Function Calls

> **Goal**: Format a user's full name using a function

```jsx
function formatName(user) {
  return user.firstName + ' ' + user.lastName;
}

const user = { firstName: 'John', lastName: 'Doe' };

function Greeting() {
  return <h1>Hello, {formatName(user)}!</h1>;
}

// USAGE EXAMPLE
// <Greeting />
// Expected: Hello, John Doe!
```

---

### 4. Ternary Expressions

> **Goal**: Show different messages based on login status

```jsx
const isLoggedIn = true;

function WelcomeMessage() {
  return (
    <p>{isLoggedIn ? 'Welcome back!' : 'Please log in'}</p>
  );
}

// USAGE EXAMPLE
// <WelcomeMessage />
// Expected: Welcome back!
```

---

### 5. Array Methods

> **Goal**: Display a list of fruits using map()

```jsx
const fruits = ['Apple', 'Banana', 'Cherry'];

function FruitList() {
  return (
    <ul>
      {fruits.map(fruit => <li key={fruit}>{fruit}</li>)}
    </ul>
  );
}

// USAGE EXAMPLE
// <FruitList />
// Expected: Unordered list with 3 fruit items
```

---

### 6. Object Properties

> **Goal**: Display product name and price from an object

```jsx
const product = {
  name: 'Laptop',
  price: 999
};

function ProductCard() {
  return <p>{product.name}: ${product.price}</p>;
}

// USAGE EXAMPLE
// <ProductCard />
// Expected: Laptop: $999
```

---

## 📊 What You CAN vs CANNOT Embed

| Can Embed ✅ | Cannot Embed ❌ | Why? |
|-------------|----------------|------|
| Variables | Objects directly | Objects aren't valid React children |
| Math operations | `if` statements | `if` is a statement, not expression |
| Function calls | `for` loops | `for` is a statement, not expression |
| Ternary operators | `while` loops | `while` is a statement, not expression |
| Array methods | `switch` statements | `switch` is a statement, not expression |
| Object properties | - | - |

---

## 🧠 Memory Tricks

> [!NOTE] **Remember This!** 🧠
> - **Curly braces** = JavaScript zone! `{variable}`, `{expression}` 🎯
> - **Can embed**: variables, math, functions, ternaries, `.map()` ✅
> - **Cannot embed**: objects, `if/for/while` statements ❌
> - **Statements vs Expressions**: Use ternary `? :` instead of `if`.
> - **Objects**: Access properties `{user.name}`, not `{user}`.

---

## ❓ Questions to Test Yourself

> [!QUESTION] **Q1**: What's wrong with this code?
> > ```jsx
> > const user = { name: 'Alice', age: 25 };
> > return <p>{user}</p>;
> > ```
> > [!SUCCESS]- Answer
> > You **can't render objects directly**!
> > 
> > **Fix:**
> > ```jsx
> > return <p>{user.name} - {user.age}</p>;
> > ```

> [!QUESTION] **Q2**: How do you use if-else in JSX?
> > [!SUCCESS]- Answer
> > You **can't** use `if-else` directly in JSX. Use ternary instead:
> > ```jsx
> > // ✅ Ternary operator
> > <p>{isLoggedIn ? 'Welcome' : 'Please log in'}</p>
> > 
> > // ✅ Or if-else before return
> > if (isLoggedIn) {
> >   return <p>Welcome</p>;
> > }
> > return <p>Please log in</p>;
> > ```

> [!QUESTION] **Q3**: Can you embed a function definition in JSX?
> > [!SUCCESS]- Answer
> > **No!** You can only **call** functions, not define them:
> > ```jsx
> > // ❌ Wrong
> > <p>{function() { return 'Hello' }}</p>
> > 
> > // ✅ Correct - call a function
> > <p>{getMessage()}</p>
> > ```

> [!QUESTION] **Q4**: What renders for `{0 && <Component />}`?
> > [!SUCCESS]- Answer
> > It renders **"0"** on the screen!
> > 
> > Why? Because `0` is falsy but React still renders it.
> > 
> > **Fix:** Use explicit boolean check:
> > ```jsx
> > {count > 0 && <Component />}  // Safe ✅
> > ```

> [!QUESTION] **Q5**: How do you display an array in JSX?
> > [!SUCCESS]- Answer
> > Use `.map()` to transform array into JSX elements:
> > ```jsx
> > {items.map(item => <li key={item.id}>{item.name}</li>)}
> > ```
> > Don't forget the `key` prop!

---

> [!WARNING] **Watch Out!**
> Empty strings `''`, `null`, `undefined`, `true`, and `false` don't render.
> But the number `0` DOES render!

> [!TIP] **Pro Tip**
> Template literals can make JSX cleaner:
> ```jsx
> <p>{`Hello, ${name}! You are ${age} years old.`}</p>
> ```

---

Back to: [[index|Module 1 Hub]] | [[../React JS Hub|React Hub]]

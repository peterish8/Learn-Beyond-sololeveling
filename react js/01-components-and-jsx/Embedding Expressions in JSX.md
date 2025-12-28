# Embedding Expressions in JSX

## 🎯 The Curly Braces `{}`
Use **curly braces** to embed any JavaScript expression inside JSX.

```jsx
const name = "Alice";
const element = <h1>Hello, {name}!</h1>;
// Output: Hello, Alice!
```

---

## 📦 What Can You Embed?

### 1. Variables
```jsx
const username = "john_doe";
const age = 25;

return (
  <div>
    <p>Username: {username}</p>
    <p>Age: {age}</p>
  </div>
);
```

### 2. Math Operations
```jsx
const price = 100;
const tax = 0.1;

return <p>Total: ${price + (price * tax)}</p>;
// Output: Total: $110
```

### 3. Function Calls
```jsx
function formatName(user) {
  return user.firstName + ' ' + user.lastName;
}

const user = { firstName: 'John', lastName: 'Doe' };

return <h1>Hello, {formatName(user)}!</h1>;
// Output: Hello, John Doe!
```

### 4. Ternary Expressions
```jsx
const isLoggedIn = true;

return <p>{isLoggedIn ? 'Welcome back!' : 'Please log in'}</p>;
```

### 5. Array Methods
```jsx
const fruits = ['Apple', 'Banana', 'Cherry'];

return (
  <ul>
    {fruits.map(fruit => <li key={fruit}>{fruit}</li>)}
  </ul>
);
```

### 6. Object Properties
```jsx
const product = {
  name: 'Laptop',
  price: 999
};

return <p>{product.name}: ${product.price}</p>;
```

---

## ⚠️ What You CANNOT Embed

### ❌ Objects Directly
```jsx
const user = { name: 'John' };

// ❌ WRONG - Objects are not valid as React child
return <p>{user}</p>;

// ✅ CORRECT - Access the property
return <p>{user.name}</p>;
```

### ❌ Statements (if, for, while)
```jsx
// ❌ WRONG - Statements don't work
return <p>{if (true) { 'Hello' }}</p>;

// ✅ CORRECT - Use ternary instead
return <p>{true ? 'Hello' : 'Goodbye'}</p>;
```

---

## 💡 Practical Examples

```jsx
function ProductCard({ product }) {
  const discountedPrice = product.price * 0.9;
  
  return (
    <div className="card">
      <h2>{product.name}</h2>
      <p>Original: ${product.price}</p>
      <p>Sale: ${discountedPrice.toFixed(2)}</p>
      <p>In Stock: {product.inStock ? '✅ Yes' : '❌ No'}</p>
      <p>Rating: {'⭐'.repeat(product.rating)}</p>
    </div>
  );
}
```

---

## 🎓 Key Takeaways

- [ ] Use `{}` to embed JavaScript in JSX
- [ ] Can embed: variables, math, functions, ternaries
- [ ] Cannot embed: objects directly, if/for statements
- [ ] Always access object properties, not the whole object

[[index|← Back to Module]]

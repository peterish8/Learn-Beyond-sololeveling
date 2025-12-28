# Props Destructuring

## 🎯 What is Destructuring?
A JavaScript feature to **extract values** from objects/arrays into separate variables.

---

## 📦 Without vs With Destructuring

### Without (Repetitive 😴)
```jsx
function UserCard(props) {
  return (
    <div>
      <h2>{props.name}</h2>
      <p>{props.email}</p>
      <p>{props.age}</p>
      <p>{props.location}</p>
    </div>
  );
}
```

### With Destructuring (Clean ✅)
```jsx
function UserCard({ name, email, age, location }) {
  return (
    <div>
      <h2>{name}</h2>
      <p>{email}</p>
      <p>{age}</p>
      <p>{location}</p>
    </div>
  );
}
```

---

## 🔧 Destructuring Patterns

### 1. In Function Parameters (Most Common)
```jsx
function Greeting({ name, time }) {
  return <h1>Good {time}, {name}!</h1>;
}
```

### 2. Inside Function Body
```jsx
function Greeting(props) {
  const { name, time } = props;
  return <h1>Good {time}, {name}!</h1>;
}
```

### 3. With Default Values
```jsx
function Greeting({ name = 'Guest', time = 'day' }) {
  return <h1>Good {time}, {name}!</h1>;
}

// Usage
<Greeting />  // Good day, Guest!
<Greeting name="John" />  // Good day, John!
```

### 4. Renaming Props
```jsx
function UserCard({ name: userName, age: userAge }) {
  return (
    <div>
      <p>{userName}</p>  {/* Renamed variable */}
      <p>{userAge}</p>
    </div>
  );
}
```

### 5. Rest Operator (Collect Remaining Props)
```jsx
function Button({ variant, size, ...rest }) {
  // rest contains all other props (onClick, disabled, etc.)
  return (
    <button 
      className={`btn-${variant} btn-${size}`} 
      {...rest}
    >
      Click
    </button>
  );
}

// Usage
<Button variant="primary" size="lg" onClick={handleClick} disabled={false} />
```

---

## 🎯 Nested Object Destructuring

```jsx
// If prop is an object
const user = {
  name: 'John',
  address: {
    city: 'NYC',
    zip: '10001'
  }
};

// Nested destructuring
function UserCard({ name, address: { city, zip } }) {
  return (
    <div>
      <h2>{name}</h2>
      <p>{city}, {zip}</p>
    </div>
  );
}

<UserCard {...user} />
```

---

## ⚡ Array Destructuring in Props

```jsx
function Podium({ winners }) {
  const [first, second, third] = winners;
  
  return (
    <div>
      <p>🥇 {first}</p>
      <p>🥈 {second}</p>
      <p>🥉 {third}</p>
    </div>
  );
}

// Usage
<Podium winners={['Alice', 'Bob', 'Charlie']} />
```

---

## 💡 Best Practices

```jsx
// ✅ Destructure in parameters
function Card({ title, content, footer }) {
  return (/* ... */);
}

// ✅ Use default values
function Modal({ isOpen = false, title = 'Modal' }) {
  return (/* ... */);
}

// ✅ Use rest for forwarding props
function Input({ label, ...inputProps }) {
  return (
    <label>
      {label}
      <input {...inputProps} />
    </label>
  );
}
```

---

## 🎓 Key Takeaways

- [ ] Destructure in function parameters for cleanest code
- [ ] Set default values: `{ name = 'Guest' }`
- [ ] Rename with colon: `{ name: userName }`
- [ ] Collect extras with rest: `{ ...rest }`
- [ ] Avoid `props.` everywhere – destructure!

[[index|← Back to Module]]

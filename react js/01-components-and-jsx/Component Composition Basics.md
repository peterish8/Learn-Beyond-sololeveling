# Component Composition Basics

## 🎯 What is Composition?
Building complex UIs by **combining smaller, simpler components** together.

> Think of it like building with LEGO blocks!

---

## 🏗️ Basic Composition

```jsx
// Small components
function Header() {
  return <header><h1>My App</h1></header>;
}

function Sidebar() {
  return <aside>Navigation here</aside>;
}

function Content() {
  return <main>Main content here</main>;
}

function Footer() {
  return <footer>© 2024</footer>;
}

// Compose them together
function App() {
  return (
    <div className="app">
      <Header />
      <div className="layout">
        <Sidebar />
        <Content />
      </div>
      <Footer />
    </div>
  );
}
```

---

## 🎁 Nesting Components

Components can contain other components:

```jsx
function Avatar({ src, name }) {
  return <img src={src} alt={name} className="avatar" />;
}

function UserInfo({ user }) {
  return (
    <div className="user-info">
      <Avatar src={user.avatar} name={user.name} />
      <span>{user.name}</span>
    </div>
  );
}

function Comment({ comment }) {
  return (
    <div className="comment">
      <UserInfo user={comment.author} />
      <p>{comment.text}</p>
      <span>{comment.date}</span>
    </div>
  );
}
```

---

## 📦 Component Tree

```
App
├── Header
├── Layout
│   ├── Sidebar
│   │   └── NavItem (multiple)
│   └── Content
│       └── ArticleCard (multiple)
└── Footer
```

---

## 🧩 Specialization Pattern

Create specialized versions of a component:

```jsx
// Generic Button
function Button({ color, children, onClick }) {
  return (
    <button 
      style={{ backgroundColor: color }}
      onClick={onClick}
    >
      {children}
    </button>
  );
}

// Specialized versions
function PrimaryButton({ children, onClick }) {
  return <Button color="blue" onClick={onClick}>{children}</Button>;
}

function DangerButton({ children, onClick }) {
  return <Button color="red" onClick={onClick}>{children}</Button>;
}

function SuccessButton({ children, onClick }) {
  return <Button color="green" onClick={onClick}>{children}</Button>;
}

// Usage
function App() {
  return (
    <>
      <PrimaryButton onClick={() => {}}>Save</PrimaryButton>
      <DangerButton onClick={() => {}}>Delete</DangerButton>
      <SuccessButton onClick={() => {}}>Confirm</SuccessButton>
    </>
  );
}
```

---

## ✅ Composition Benefits

| Benefit | Description |
|---------|-------------|
| **Reusability** | Use same component in multiple places |
| **Maintainability** | Change once, updates everywhere |
| **Readability** | Small components are easier to understand |
| **Testability** | Test components in isolation |
| **Separation** | Each component has one job |

---

## 💡 Practical Example: Card Layout

```jsx
function Card({ children }) {
  return <div className="card">{children}</div>;
}

function CardHeader({ title }) {
  return <div className="card-header"><h2>{title}</h2></div>;
}

function CardBody({ children }) {
  return <div className="card-body">{children}</div>;
}

function CardFooter({ children }) {
  return <div className="card-footer">{children}</div>;
}

// Compose flexibly
function ProductCard({ product }) {
  return (
    <Card>
      <CardHeader title={product.name} />
      <CardBody>
        <p>{product.description}</p>
        <span>${product.price}</span>
      </CardBody>
      <CardFooter>
        <button>Add to Cart</button>
      </CardFooter>
    </Card>
  );
}
```

---

## 🎓 Key Takeaways

- [ ] Build complex UIs from small components
- [ ] Components can contain other components
- [ ] Create specialized versions of generic components
- [ ] Each component should do ONE thing well
- [ ] Use composition over inheritance

[[index|← Back to Module]]

# Early Returns

## 🎯 What are Early Returns?
Returning from a function **before** the main JSX, usually for guard clauses or special cases.

```jsx
function UserProfile({ user }) {
  if (!user) return <div>Please log in</div>;  // Early return
  
  // Main JSX
  return (
    <div>
      <h1>{user.name}</h1>
    </div>
  );
}
```

---

## ✅ Benefits

| Benefit | Description |
|---------|-------------|
| **Cleaner code** | Avoid deep nesting |
| **Guard clauses** | Handle edge cases first |
| **Readability** | Easier to follow logic |
| **Less indentation** | Flatter code structure |

---

## 📝 Common Patterns

### Loading State
```jsx
function DataDisplay({ data, isLoading }) {
  if (isLoading) {
    return <div>Loading...</div>;
  }
  
  return (
    <ul>
      {data.map(item => <li key={item.id}>{item.name}</li>)}
    </ul>
  );
}
```

### Error State
```jsx
function UserProfile({ user, error }) {
  if (error) {
    return <div className="error">Error: {error.message}</div>;
  }
  
  if (!user) {
    return <div>No user found</div>;
  }
  
  return (
    <div>
      <h1>{user.name}</h1>
      <p>{user.email}</p>
    </div>
  );
}
```

### Permission Check
```jsx
function AdminPanel({ user }) {
  if (!user) return <Login />;
  if (!user.isAdmin) return <div>Access denied</div>;
  
  return (
    <div className="admin-panel">
      <h1>Admin Dashboard</h1>
      <AdminControls />
    </div>
  );
}
```

---

## 🆚 Early Return vs Nested Conditionals

### Without Early Returns (Nested)
```jsx
function Component({ data, loading, error }) {
  return (
    <div>
      {loading ? (
        <p>Loading...</p>
      ) : error ? (
        <p>Error: {error}</p>
      ) : data ? (
        <div>
          <h1>{data.title}</h1>
          <p>{data.content}</p>
        </div>
      ) : (
        <p>No data</p>
      )}
    </div>
  );
}
```

### With Early Returns (Cleaner ✅)
```jsx
function Component({ data, loading, error }) {
  if (loading) return <p>Loading...</p>;
  if (error) return <p>Error: {error}</p>;
  if (!data) return <p>No data</p>;
  
  return (
    <div>
      <h1>{data.title}</h1>
      <p>{data.content}</p>
    </div>
  );
}
```

---

## 📋 Multiple Guard Clauses

```jsx
function EditProfile({ user, canEdit, isPremium }) {
  // Guard clauses first
  if (!user) {
    return <Redirect to="/login" />;
  }
  
  if (!canEdit) {
    return <div>You cannot edit this profile</div>;
  }
  
  if (!isPremium) {
    return (
      <div>
        <p>Upgrade to premium to edit profile</p>
        <UpgradeButton />
      </div>
    );
  }
  
  // Main happy path
  return (
    <form>
      <input name="name" defaultValue={user.name} />
      <input name="bio" defaultValue={user.bio} />
      <button type="submit">Save</button>
    </form>
  );
}
```

---

## 💡 Practical Example

```jsx
function ProductPage({ productId }) {
  const [product, setProduct] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    fetch(`/api/products/${productId}`)
      .then(res => res.json())
      .then(data => {
        setProduct(data);
        setLoading(false);
      })
      .catch(err => {
        setError(err.message);
        setLoading(false);
      });
  }, [productId]);

  // Early returns for different states
  if (loading) {
    return <div className="spinner">Loading product...</div>;
  }

  if (error) {
    return (
      <div className="error">
        <h2>Failed to load product</h2>
        <p>{error}</p>
      </div>
    );
  }

  if (!product) {
    return <div>Product not found</div>;
  }

  // Main render
  return (
    <div className="product">
      <h1>{product.name}</h1>
      <p>{product.description}</p>
      <p>${product.price}</p>
      <button>Add to Cart</button>
    </div>
  );
}
```

---

## 🎓 Key Takeaways

- [ ] Return early for special cases
- [ ] Handle errors/loading at the top
- [ ] Reduces nesting and complexity
- [ ] Main code is at the bottom (happy path)
- [ ] Makes code easier to read and maintain

[[index|← Back to Module]]

# Controlled Components

## 🎯 What are Controlled Components?
Form inputs whose values are **controlled by React state**.

```jsx
const [value, setValue] = useState('');

<input 
  value={value}                         // State controls value
  onChange={(e) => setValue(e.target.value)}  // State updates on change
/>
```

---

## 🔄 How They Work

```
User types → onChange fires → State updates → Component re-renders → Input shows new value
```

React state is the **single source of truth** for the input value.

---

## 📝 Basic Example

```jsx
function NameInput() {
  const [name, setName] = useState('');

  return (
    <div>
      <input 
        type="text"
        value={name}
        onChange={(e) => setName(e.target.value)}
        placeholder="Enter your name"
      />
      <p>Hello, {name}!</p>
    </div>
  );
}
```

---

## 💡 Different Input Types

### Text Input
```jsx
const [text, setText] = useState('');

<input 
  type="text"
  value={text}
  onChange={(e) => setText(e.target.value)}
/>
```

### Textarea
```jsx
const [message, setMessage] = useState('');

<textarea 
  value={message}
  onChange={(e) => setMessage(e.target.value)}
/>
```

### Checkbox
```jsx
const [isChecked, setIsChecked] = useState(false);

<input 
  type="checkbox"
  checked={isChecked}        // Use 'checked', not 'value'
  onChange={(e) => setIsChecked(e.target.checked)}
/>
```

### Radio Buttons
```jsx
const [selected, setSelected] = useState('option1');

<label>
  <input 
    type="radio"
    value="option1"
    checked={selected === 'option1'}
    onChange={(e) => setSelected(e.target.value)}
  />
  Option 1
</label>

<label>
  <input 
    type="radio"
    value="option2"
    checked={selected === 'option2'}
    onChange={(e) => setSelected(e.target.value)}
  />
  Option 2
</label>
```

### Select Dropdown
```jsx
const [country, setCountry] = useState('us');

<select 
  value={country}
  onChange={(e) => setCountry(e.target.value)}
>
  <option value="us">United States</option>
  <option value="uk">United Kingdom</option>
  <option value="ca">Canada</option>
</select>
```

---

## 📋 Complete Form Example

```jsx
function ContactForm() {
  const [form, setForm] = useState({
    name: '',
    email: '',
    message: '',
    subscribe: false,
    country: 'us'
  });

  const handleChange = (e) => {
    const { name, value, type, checked } = e.target;
    setForm(prev => ({
      ...prev,
      [name]: type === 'checkbox' ? checked : value
    }));
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    console.log('Form submitted:', form);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input
        name="name"
        type="text"
        value={form.name}
        onChange={handleChange}
        placeholder="Name"
      />
      
      <input
        name="email"
        type="email"
        value={form.email}
        onChange={handleChange}
        placeholder="Email"
      />
      
      <textarea
        name="message"
        value={form.message}
        onChange={handleChange}
        placeholder="Message"
      />
      
      <label>
        <input
          name="subscribe"
          type="checkbox"
          checked={form.subscribe}
          onChange={handleChange}
        />
        Subscribe to newsletter
      </label>
      
      <select name="country" value={form.country} onChange={handleChange}>
        <option value="us">United States</option>
        <option value="uk">United Kingdom</option>
      </select>
      
      <button type="submit">Submit</button>
    </form>
  );
}
```

---

## ✅ Benefits

| Benefit | Description |
|---------|-------------|
| **Single source of truth** | State controls the value |
| **Validation** | Easy to validate before updating state |
| **Transformations** | Can transform input (e.g., uppercase) |
| **Conditional logic** | Enable/disable based on other inputs |

---

## 🎓 Key Takeaways

- [ ] Controlled = React state controls the input
- [ ] Use `value` and `onChange` together
- [ ] Checkbox uses `checked` not `value`
- [ ] State is the single source of truth
- [ ] Enables validation and transformations

[[index|← Back to Module]]

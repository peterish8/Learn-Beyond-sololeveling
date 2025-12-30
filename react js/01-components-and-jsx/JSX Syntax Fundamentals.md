## 📌 JSX Syntax Fundamentals

> [!SUCCESS] **Definition**: JSX = JavaScript XML. Write HTML-like code in JavaScript!
> **Recall**: JSX compiles to `React.createElement()` behind the scenes.

---

## 🎯 **What is JSX?**

> **Goal**: Understand how to write JSX syntax

```jsx
// This is JSX - looks like HTML!
const element = <h1>Hello, World!</h1>;

// Behind the scenes, it becomes:
const element = React.createElement('h1', null, 'Hello, World!');

// USAGE EXAMPLE
// ReactDOM.render(element, document.getElementById('root'));
// Expected: Renders "Hello, World!" in an h1 tag
```

---

## 📐 **JSX Rules**

### Rule 1: Must Have One Parent Element

```jsx
// ❌ WRONG - Multiple root elements
return (
  <h1>Title</h1>
  <p>Paragraph</p>
);

// ✅ CORRECT - Wrapped in one parent
return (
  <div>
    <h1>Title</h1>
    <p>Paragraph</p>
  </div>
);

// ✅ ALSO CORRECT - Using Fragment
return (
  <>
    <h1>Title</h1>
    <p>Paragraph</p>
  </>
);
```

---

### Rule 2: All Tags Must Be Closed

```jsx
// ❌ WRONG - Unclosed tags
<img src="photo.jpg">
<input type="text">
<br>

// ✅ CORRECT - Self-closing tags
<img src="photo.jpg" />
<input type="text" />
<br />
```

---

### Rule 3: Use `className` Instead of `class`

```jsx
// ❌ WRONG - 'class' is reserved in JS
<div class="container">

// ✅ CORRECT
<div className="container">
```

---

### Rule 4: Use `htmlFor` Instead of `for`

```jsx
// ❌ WRONG
<label for="email">Email</label>

// ✅ CORRECT
<label htmlFor="email">Email</label>
```

---

### Rule 5: CamelCase for Attributes

```jsx
// HTML → JSX conversion
onclick      → onClick
onchange     → onChange
tabindex     → tabIndex
maxlength    → maxLength
```

---

## 📊 JSX vs HTML Quick Reference

| HTML | JSX | Why? |
|------|-----|------|
| `class` | `className` | `class` is reserved in JavaScript |
| `for` | `htmlFor` | `for` is reserved in JavaScript |
| `onclick` | `onClick` | camelCase convention |
| `tabindex` | `tabIndex` | camelCase convention |
| `<br>` | `<br />` | Must be self-closed |
| `style="color: red"` | `style={{ color: 'red' }}` | Style is an object |

---

## 📌 Complete Example

> **Goal**: Create a card component with proper JSX syntax

```jsx
function Card() {
  return (
    <div className="card">
      <img src="avatar.jpg" alt="User" />
      <h2>John Doe</h2>
      <p>Frontend Developer</p>
      <button onClick={() => alert('Hi!')}>
        Say Hello
      </button>
    </div>
  );
}

// USAGE EXAMPLE
// <Card />
// Expected: Renders a card with image, name, title, and button
```

---

## 🧠 Memory Tricks

> [!NOTE] **Remember This!** 🧠
> - **JSX** = HTML in JavaScript. Not a string! 📝
> - **One root** = Wrap in `<div>` or Fragment `<>`. 🎁
> - **Close everything** = `<br />`, `<img />` need slashes.
> - **className** not class. **htmlFor** not for. 🔤
> - **camelCase** events = `onClick`, `onChange`. 🐫

---

## ❓ Questions to Test Yourself

> [!QUESTION] **Q1**: Why can't you use `class` in JSX?
> > [!SUCCESS]- Answer
> > `class` is a **reserved keyword** in JavaScript (used for ES6 classes).
> > React uses `className` to avoid conflicts.

> [!QUESTION] **Q2**: What's wrong with this JSX?
> > ```jsx
> > return (
> >   <h1>Hello</h1>
> >   <p>World</p>
> > );
> > ```
> > [!SUCCESS]- Answer
> > **Missing parent wrapper!** JSX can only return ONE root element.
> > 
> > **Fix:**
> > ```jsx
> > return (
> >   <>
> >     <h1>Hello</h1>
> >     <p>World</p>
> >   </>
> > );
> > ```

> [!QUESTION] **Q3**: How do you write inline styles in JSX?
> > [!SUCCESS]- Answer
> > Use a JavaScript object with camelCase properties:
> > ```jsx
> > <div style={{ backgroundColor: 'blue', fontSize: '16px' }}>
> >   Content
> > </div>
> > ```
> > Note the **double curly braces**: outer for JSX expression, inner for object.

> [!QUESTION] **Q4**: What happens if you forget to close a self-closing tag?
> > [!SUCCESS]- Answer
> > **Syntax error!** JSX won't compile.
> > ```jsx
> > <img src="photo.jpg">  // ❌ Error
> > <img src="photo.jpg" /> // ✅ Correct
> > ```

> [!QUESTION] **Q5**: Is JSX required to use React?
> > [!SUCCESS]- Answer
> > **No**, but it makes code much cleaner! Without JSX:
> > ```jsx
> > // Without JSX (ugly!)
> > React.createElement('h1', null, 'Hello');
> > 
> > // With JSX (clean!)
> > <h1>Hello</h1>
> > ```

---

> [!WARNING] **Common Mistakes**
> - Forgetting to close self-closing tags: `<img>` → `<img />`
> - Using `class` instead of `className`
> - Trying to return multiple root elements without wrapper

> [!TIP] **Pro Tip**
> Use React DevTools browser extension to inspect JSX elements!

---

Back to: [[index|Module 1 Hub]] | [[../React JS Hub|React Hub]]

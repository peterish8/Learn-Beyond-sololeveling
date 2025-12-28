# 📝 Forms & Inputs

## Module Progress
- [ ] [[Controlled Components]] 🎮 React controls the input value
- [ ] [[Input Textarea Select Elements]] 📋 Different form element types
- [ ] [[Handling Form Submission]] 📤 onSubmit and form data
- [ ] [[Multiple Inputs]] 📑 Managing many fields
- [ ] [[Form Validation Basics]] ✅ Checking user input
- [ ] [[Uncontrolled Components]] 🔓 Using refs for form values

---

## 🎯 Learning Objectives
- Create controlled components with `value` and `onChange`
- Handle different input types (text, textarea, select)
- Process form submissions
- Manage forms with multiple inputs efficiently
- Implement basic client-side validation
- Understand when to use uncontrolled components

## 📌 Key Concepts
> **Controlled**: `<input value={state} onChange={(e) => setState(e.target.value)} />`

> State is the "single source of truth" for the input value.

> For multiple inputs, use a single state object and dynamic keys:
> ```jsx
> const [form, setForm] = useState({ name: '', email: '' });
> onChange={(e) => setForm({...form, [e.target.name]: e.target.value})}
> ```

[[React JS Hub|← Back to Hub]]

# ⚛️ React JS Learning Hub

> [!INFO] **React Progress Tracker**
> Track your React learning journey across all core modules!
> 
> ```dataviewjs
> const module01 = dv.page("react js/01-components-and-jsx/index.md");
> const module02 = dv.page("react js/02-props-and-state/index.md");
> const module03 = dv.page("react js/03-essential-hooks/index.md");
> const module04 = dv.page("react js/04-event-handling/index.md");
> const module05 = dv.page("react js/05-conditional-rendering/index.md");
> const module06 = dv.page("react js/06-lists-and-keys/index.md");
> const module07 = dv.page("react js/07-forms-and-inputs/index.md");
> const module08 = dv.page("react js/08-styling-react/index.md");
> const module09 = dv.page("react js/09-project-setup/index.md");
> const module10 = dv.page("react js/10-common-patterns/index.md");
> 
> const allTasks = [
>   ...(module01?.file?.tasks || []),
>   ...(module02?.file?.tasks || []),
>   ...(module03?.file?.tasks || []),
>   ...(module04?.file?.tasks || []),
>   ...(module05?.file?.tasks || []),
>   ...(module06?.file?.tasks || []),
>   ...(module07?.file?.tasks || []),
>   ...(module08?.file?.tasks || []),
>   ...(module09?.file?.tasks || []),
>   ...(module10?.file?.tasks || [])
> ];
> 
> const completed = allTasks.filter(t => t.completed).length;
> const total = allTasks.length;
> const percent = total === 0 ? 0 : Math.round((completed / total) * 100);
> 
> dv.paragraph(`**Overall Status:** ${completed}/${total} Topics Completed (**${percent}%**)`);
> dv.paragraph(`<div style="width: 100%; background-color: #e0e0e0; border-radius: 10px; height: 20px; box-shadow: inset 0 1px 3px rgba(0,0,0,0.2);"><div style="width: ${percent}%; background-color: #4caf50; height: 100%; border-radius: 10px; transition: width 0.5s ease;"></div></div>`);
> ```

---

## 🧱 **Module 01: Components & JSX**

![[01-components-and-jsx/index#Module Progress]]

---

## 📦 **Module 02: Props & State**

![[02-props-and-state/index#Module Progress]]

---

## 🪝 **Module 03: Essential Hooks**

![[03-essential-hooks/index#Module Progress]]

---

## 🖱️ **Module 04: Event Handling**

![[04-event-handling/index#Module Progress]]

---

## 🔀 **Module 05: Conditional Rendering**

![[05-conditional-rendering/index#Module Progress]]

---

## 📋 **Module 06: Lists & Keys**

![[06-lists-and-keys/index#Module Progress]]

---

## 📝 **Module 07: Forms & Inputs**

![[07-forms-and-inputs/index#Module Progress]]

---

## 🎨 **Module 08: Styling React**

![[08-styling-react/index#Module Progress]]

---

## ⚙️ **Module 09: Project Setup**

![[09-project-setup/index#Module Progress]]

---

## 🔧 **Module 10: Common Patterns**

![[10-common-patterns/index#Module Progress]]

---

## 🚀 Next Steps (Intermediate Concepts)
After completing the fundamentals, explore:
- [ ] [[Context API]] - Global state management
- [ ] [[React Router]] - Client-side routing
- [ ] [[useReducer]] - Complex state logic
- [ ] [[useMemo & useCallback]] - Performance optimization
- [ ] [[React Query]] - Server state management
- [ ] [[Zustand or Redux]] - State management libraries

---

> Keep going! "The secret to getting ahead is getting started." 💪

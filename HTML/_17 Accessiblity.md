# 🟠 HTML — Accessibility Basics (A11y) (`alt`, `label`, `aria-*`, Keyboard, `tabindex`) — Methods, Pitfalls, Fixes

> `HTML Accessibility (A11y)` defines **how content is perceived, navigated, and operated** by assistive technologies; it encodes **meaning, relationships, and interaction**, not visual appearance.

---

---

## 1️⃣ `alt` — Alternative Text for Images

### **Purpose (Mandatory — do not skip)**

- Provides a **textual alternative** for non-text content
    
- Required for meaningful images
    
- Read by screen readers, shown when image fails
    
- **Semantic**, **eager**
    

---

### **Method**

```html
<img src="..." alt="description">
```

---

### **Correct usage**

```html
<img src="chart.png" alt="Sales increased from 2023 to 2024">
```

---

### **Observed output**

```text
Screen reader announces image description
```

---

### **Common pitfalls**

- ❌ Empty or missing `alt` on informative images
    
- ❌ Repeating filename or “image”
    
- ❌ Over-describing decorative images
    

---

### **Failure example**

```html
<img src="chart.png">
```

**Failure:**  
Image announced as “unlabeled graphic”

---

### **Correct alternative**

```html
<img src="chart.png" alt="Sales trend chart">
```

---

### **Observed output**

```text
Meaning conveyed non-visually
```

---

## 2️⃣ `<label>` — Accessible Control Name

### **Purpose (Mandatory — do not skip)**

- Defines the **accessible name** for form controls
    
- Required for screen readers and voice input
    
- Expands clickable focus area
    
- **Inline**, **finite**, **eager**
    

---

### **Method**

```html
<label for="id">Text</label>
```

---

### **Correct usage**

```html
<label for="email">Email</label>
<input id="email" name="email">
```

---

### **Observed output**

```text
Label announced with input
```

---

### **Common pitfalls**

- ❌ Using `placeholder` instead of label
    
- ❌ Missing `for` / `id` association
    

---

### **Failure example**

```html
<input placeholder="Email">
```

**Failure:**  
No accessible name

---

### **Correct alternative**

```html
<label>
  Email
  <input name="email">
</label>
```

---

### **Observed output**

```text
Input correctly identified
```

---

## 3️⃣ `aria-*` — ARIA Attributes

### **Purpose (Mandatory — do not skip)**

- Adds **accessibility semantics** where HTML cannot
    
- Communicates roles, states, and properties
    
- Supplements—not replaces—native HTML
    
- **Declarative**, **eager**
    

---

### **Method**

```html
aria-label
aria-hidden
aria-expanded
aria-live
```

---

### **Correct usage**

```html
<button aria-expanded="false">Menu</button>
```

---

### **Observed output**

```text
Screen reader announces collapsed state
```

---

### **Common pitfalls**

- ❌ Using ARIA instead of native elements
    
- ❌ Incorrect or stale ARIA states
    
- ❌ Overusing `aria-label`
    

---

### **Failure example**

```html
<div role="button">Click</div>
```

**Failure:**  
Keyboard and semantics missing

---

### **Correct alternative**

```html
<button>Click</button>
```

---

### **Observed output**

```text
Native semantics and keyboard support
```

---

## 4️⃣ Keyboard Navigation — Focus Order & Operability

### **Purpose (Mandatory — do not skip)**

- Ensures **all functionality is keyboard-accessible**
    
- Defines predictable focus order
    
- Required for WCAG compliance
    
- **Behavioral**, **runtime-dependent**
    

---

### **Method**

```html
<!-- Native focus via tab order -->
```

---

### **Correct usage**

```html
<button>Save</button>
<a href="#">Link</a>
```

---

### **Observed output**

```text
Tab key moves focus sequentially
```

---

### **Common pitfalls**

- ❌ Click-only interactions
    
- ❌ Removing focus outlines
    
- ❌ Non-focusable custom controls
    

---

### **Failure example**

```html
<div onclick="do()">Click</div>
```

**Failure:**  
Not keyboard operable

---

### **Correct alternative**

```html
<button onclick="do()">Click</button>
```

---

### **Observed output**

```text
Keyboard + mouse supported
```

---

## 5️⃣ `tabindex` — Focus Control

### **Purpose (Mandatory — do not skip)**

- Controls **keyboard focus order**
    
- Enables focus on non-interactive elements
    
- Can remove elements from tab order
    
- **Declarative**, **eager**
    

---

### **Method**

```html
tabindex="0 | -1 | positive"
```

---

### **Correct usage**

```html
<div tabindex="0">Focusable</div>
```

---

### **Observed output**

```text
Element receives keyboard focus
```

---

### **Common pitfalls**

- ❌ Using positive tabindex values
    
- ❌ Managing focus manually without reason
    
- ❌ Breaking natural tab order
    

---

### **Failure example**

```html
<div tabindex="5">Out of order</div>
```

**Failure:**  
Confusing navigation order

---

### **Correct alternative**

```html
<div tabindex="0">In natural order</div>
```

---

### **Observed output**

```text
Predictable focus flow
```

---

## 🚨 Conceptual Pitfalls (Very Important)

❌ **ARIA fixes bad HTML**

```html
<div role="button">X</div>
```

```text
Still broken
```

✅ Use native elements first

---

❌ **Placeholder = label**

```html
<input placeholder="Name">
```

```text
Not announced reliably
```

✅ Always provide `<label>`

---

❌ **Mouse-only interaction**

```html
<div onclick="open()">Open</div>
```

```text
Keyboard blocked
```

✅ All actions must be keyboard-accessible

---

## 🧠 Mental Model (Exam + Design)

- Accessibility is **structural**, not cosmetic
    
- Native HTML gives free accessibility
    
- ARIA fills gaps, never replaces HTML
    
- Keyboard access is mandatory
    
- Focus order defines usability
    
- Screen readers rely on semantics, not CSS
    

---

## 📌 Summary Table

|Feature|Purpose|Common Pitfall|
|---|---|---|
|`alt`|Image alternative|Missing / useless text|
|`<label>`|Control name|Placeholder misuse|
|`aria-*`|Extra semantics|Overuse|
|Keyboard nav|Operability|Click-only UI|
|`tabindex`|Focus control|Positive values|

---

## ✅ Golden Rule

If you must add ARIA, **ask why native HTML wasn’t enough**.  
If a feature can’t be used with a keyboard, it is **not accessible**.
# 🟠 HTML — Global & Common Attributes (`id`, `class`, `title`, `hidden`, `data-*`, `contenteditable`, `draggable`) — Methods, Pitfalls, Fixes

> `HTML Global & Common Attributes` are **element-level modifiers** that attach **identity, metadata, behavior, or state** to elements; they are **orthogonal to tag semantics** and apply across most HTML elements.

---

---

## 1️⃣ `id` — Unique Element Identifier

### **Purpose (Mandatory — do not skip)**

- Assigns a **document-unique identifier**
    
- Enables DOM lookup, fragment navigation, CSS targeting
    
- Must be **unique within the entire document**
    
- **Static**, **eager**
    

---

### **Method**

```html
id="identifier"
```

---

### **Correct usage**

```html
<h1 id="title">Heading</h1>
```

---

### **Observed output**

```text
URL fragment #title navigates to heading
```

---

### **Common pitfalls**

- ❌ Duplicate `id` values
    
- ❌ Using `id` for styling groups
    
- ❌ Auto-generating unstable IDs
    

---

### **Failure example**

```html
<p id="x">A</p>
<div id="x">B</div>
```

**Failure:**  
Undefined behavior (DOM APIs return first match)

---

### **Correct alternative**

```html
<p id="a">A</p>
<div id="b">B</div>
```

---

### **Observed output**

```text
Unique element references
```

---

## 2️⃣ `class` — Non-Unique Classification

### **Purpose (Mandatory — do not skip)**

- Assigns **one or more group labels**
    
- Used for styling, behavior, selection
    
- Not required to be unique
    
- **Static**, **eager**
    

---

### **Method**

```html
class="name another"
```

---

### **Correct usage**

```html
<p class="note warning">Text</p>
```

---

### **Observed output**

```text
Element matches both classes
```

---

### **Common pitfalls**

- ❌ Using `class` as identity
    
- ❌ Encoding semantics into class names
    
- ❌ Overloading class for data storage
    

---

### **Failure example**

```html
<div class="main-content-123"></div>
```

**Failure:**  
Brittle coupling to structure

---

### **Correct alternative**

```html
<main class="content"></main>
```

---

### **Observed output**

```text
Stable grouping
```

---

## 3️⃣ `title` — Advisory Tooltip Text

### **Purpose (Mandatory — do not skip)**

- Provides **supplementary information**
    
- Displayed as tooltip on hover
    
- Exposed inconsistently to assistive tech
    
- **Non-essential**, **eager**
    

---

### **Method**

```html
title="text"
```

---

### **Correct usage**

```html
<button title="Deletes the file">Delete</button>
```

---

### **Observed output**

```text
Tooltip shown on hover
```

---

### **Common pitfalls**

- ❌ Using as primary label
    
- ❌ Relying on it for accessibility
    
- ❌ Long or critical content
    

---

### **Failure example**

```html
<input title="Username">
```

**Failure:**  
No accessible name

---

### **Correct alternative**

```html
<label>Username <input></label>
```

---

### **Observed output**

```text
Input properly labeled
```

---

## 4️⃣ `hidden` — Hidden State Flag

### **Purpose (Mandatory — do not skip)**

- Marks element as **not relevant for rendering**
    
- Element is removed from layout and accessibility tree
    
- Controlled via attribute presence
    
- **Boolean**, **eager**
    

---

### **Method**

```html
hidden
```

---

### **Correct usage**

```html
<p hidden>Secret</p>
```

---

### **Observed output**

```text
Element not rendered
```

---

### **Common pitfalls**

- ❌ Using for conditional logic instead of state
    
- ❌ Confusing with CSS `display:none`
    
- ❌ Expecting screen readers to announce it
    

---

### **Failure example**

```html
<p hidden aria-hidden="false">Text</p>
```

**Failure:**  
Conflicting semantics

---

### **Correct alternative**

```html
<p hidden>Text</p>
```

---

### **Observed output**

```text
Consistently hidden
```

---

## 5️⃣ `data-*` — Custom Data Attributes

### **Purpose (Mandatory — do not skip)**

- Stores **custom, non-visual data**
    
- Exposed via DOM (`dataset`)
    
- Must not affect semantics
    
- **Static**, **eager**
    

---

### **Method**

```html
data-name="value"
```

---

### **Correct usage**

```html
<button data-id="42">Open</button>
```

---

### **Observed output**

```text
element.dataset.id === "42"
```

---

### **Common pitfalls**

- ❌ Storing large or sensitive data
    
- ❌ Encoding behavior logic in markup
    
- ❌ Using instead of proper APIs
    

---

### **Failure example**

```html
<div data-user-password="123"></div>
```

**Failure:**  
Sensitive data exposed

---

### **Correct alternative**

```html
<div data-user-id="42"></div>
```

---

### **Observed output**

```text
Safe metadata access
```

---

## 6️⃣ `contenteditable` — Editable Content Flag

### **Purpose (Mandatory — do not skip)**

- Makes element **user-editable**
    
- Changes DOM text directly
    
- No validation or submission by default
    
- **Boolean / enum**, **runtime**
    

---

### **Method**

```html
contenteditable="true|false"
```

---

### **Correct usage**

```html
<p contenteditable="true">Edit me</p>
```

---

### **Observed output**

```text
Text can be edited inline
```

---

### **Common pitfalls**

- ❌ Assuming form submission
    
- ❌ Expecting input-like behavior
    
- ❌ Using without sanitization
    

---

### **Failure example**

```html
<form>
  <p contenteditable="true">Text</p>
</form>
```

**Failure:**  
Edited content not submitted

---

### **Correct alternative**

```html
<textarea name="text"></textarea>
```

---

### **Observed output**

```text
Text submitted with form
```

---

## 7️⃣ `draggable` — Drag-and-Drop Enablement

### **Purpose (Mandatory — do not skip)**

- Enables **HTML Drag and Drop API**
    
- Controls whether element can be dragged
    
- Requires JS to be useful
    
- **Boolean / enum**, **runtime**
    

---

### **Method**

```html
draggable="true|false"
```

---

### **Correct usage**

```html
<img src="a.png" draggable="true">
```

---

### **Observed output**

```text
Element can be dragged
```

---

### **Common pitfalls**

- ❌ Expecting drag behavior without JS
    
- ❌ Using for accessibility-critical interactions
    
- ❌ Forgetting keyboard alternatives
    

---

### **Failure example**

```html
<div draggable="true">Drag</div>
```

**Failure:**  
No drop behavior implemented

---

### **Correct alternative**

```html
<div draggable="true" ondragstart="..."></div>
```

---

### **Observed output**

```text
Drag events triggered
```

---

## 🚨 Conceptual Pitfalls (Very Important)

❌ **`id` vs `class`**

```html
<div id="item"></div>
<div id="item"></div>
```

```text
Invalid document
```

✅ `id` is unique; `class` is repeatable

---

❌ **Attributes = semantics**

```html
<div class="header"></div>
```

```text
No semantic meaning
```

✅ Use semantic tags, not classes

---

❌ **Hidden = removed**

```html
<p hidden>Text</p>
```

```text
Still in DOM
```

✅ Hidden affects rendering, not existence

---

## 🧠 Mental Model (Exam + Design)

- Attributes **modify elements**, they don’t replace tags
    
- Semantics come from **elements**, not attributes
    
- `id` identifies, `class` groups
    
- Boolean attributes work by **presence**
    
- `data-*` is metadata, not logic
    
- Interactivity often requires JavaScript
    

---

## 📌 Summary Table

|Attribute|Purpose|Common Pitfall|
|---|---|---|
|`id`|Unique identity|Duplication|
|`class`|Grouping|Used as ID|
|`title`|Tooltip text|Used as label|
|`hidden`|Remove from render|Accessibility confusion|
|`data-*`|Custom metadata|Sensitive data|
|`contenteditable`|Inline editing|Not submittable|
|`draggable`|Drag enable|No JS handling|

---

## ✅ Golden Rule

Attributes **augment behavior and identity**, not meaning.  
If you’re encoding structure or intent using attributes alone, the HTML is wrong.
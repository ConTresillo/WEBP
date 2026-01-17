# 🟠 CSS Units & Values — Methods, Pitfalls, Fixes

> `CSS Units & Values` define **how numeric values are measured, resolved, and converted** during layout and rendering.

---

## 1️⃣ `px(absoluteLength)`

### **Purpose (Mandatory — do not skip)**

- Represents a **CSS pixel** (reference unit, not device pixel)
    
- Absolute, fixed-size unit
    
- Eagerly resolved at layout time
    
- Does **not scale** with parent or font size
    

### **Method**

```css
property: <number>px;
```

### **Correct usage**

```css
div {
  width: 200px;
}
```

### **Observed output**

```text
Element width is exactly 200 CSS pixels.
```

### **Common pitfalls**

- ❌ Assuming px is device-dependent
    
- ❌ Using px for scalable typography
    

### **Failure example**

```css
p {
  font-size: 12px;
}
```

**Failure:** text does not scale well across devices

### **Correct alternative**

```css
p {
  font-size: 1rem;
}
```

### **Observed output**

```text
Text scales relative to root font size.
```

---

## 2️⃣ `percent(relativeToParent)`

### **Purpose (Mandatory — do not skip)**

- Defines size **relative to parent**
    
- Context-dependent
    
- Requires parent dimension to be defined
    

### **Method**

```css
property: <number>%;
```

### **Correct usage**

```css
.container {
  width: 500px;
}
.child {
  width: 50%;
}
```

### **Observed output**

```text
Child width is 250px.
```

### **Common pitfalls**

- ❌ Assuming % works without parent size
    
- ❌ Confusing width % with height %
    

### **Failure example**

```css
.child {
  height: 50%;
}
```

```text
Parent has no height
```

**Failure:** height resolves to auto

### **Correct alternative**

```css
.parent { height: 400px; }
.child { height: 50%; }
```

### **Observed output**

```text
Child height is 200px.
```

---

## 3️⃣ `em(relativeToParentFont)`

### **Purpose (Mandatory — do not skip)**

- Relative to **parent element’s font size**
    
- Cascading and compounding
    
- Context-sensitive
    

### **Method**

```css
property: <number>em;
```

### **Correct usage**

```css
div {
  font-size: 20px;
}
p {
  font-size: 1.5em;
}
```

### **Observed output**

```text
Paragraph font size is 30px.
```

### **Common pitfalls**

- ❌ Unexpected compounding
    
- ❌ Using em deeply nested layouts
    

### **Failure example**

```css
div { font-size: 1.5em; }
p { font-size: 1.5em; }
```

**Failure:** size compounds unintentionally

### **Correct alternative**

```css
p {
  font-size: 1rem;
}
```

### **Observed output**

```text
Font size remains predictable.
```

---

## 4️⃣ `rem(relativeToRootFont)`

### **Purpose (Mandatory — do not skip)**

- Relative to **root (`html`) font size**
    
- Non-compounding
    
- Stable scaling unit
    

### **Method**

```css
property: <number>rem;
```

### **Correct usage**

```css
html {
  font-size: 16px;
}
h1 {
  font-size: 2rem;
}
```

### **Observed output**

```text
Heading font size is 32px.
```

### **Common pitfalls**

- ❌ Confusing rem with em
    
- ❌ Forgetting root font size change affects all rems
    

### **Failure example**

```css
html { font-size: 10px; }
h1 { font-size: 2rem; }
```

**Failure:** unexpected shrinkage

### **Correct alternative**

```css
html { font-size: 16px; }
```

### **Observed output**

```text
Expected sizing restored.
```

---

## 5️⃣ `vh(viewportHeight)`

### **Purpose (Mandatory — do not skip)**

- Relative to **viewport height**
    
- Independent of parent
    
- Dynamic on resize
    

### **Method**

```css
property: <number>vh;
```

### **Correct usage**

```css
section {
  height: 100vh;
}
```

### **Observed output**

```text
Section fills full viewport height.
```

### **Common pitfalls**

- ❌ Mobile browser UI issues
    
- ❌ Using vh for small components
    

### **Failure example**

```css
div {
  height: 100vh;
}
```

**Failure:** overflow on mobile

### **Correct alternative**

```css
div {
  min-height: 100vh;
}
```

### **Observed output**

```text
Layout adapts more safely.
```

---

## 6️⃣ `vw(viewportWidth)`

### **Purpose (Mandatory — do not skip)**

- Relative to **viewport width**
    
- Useful for full-width layouts
    
- Ignores parent width
    

### **Method**

```css
property: <number>vw;
```

### **Correct usage**

```css
header {
  width: 100vw;
}
```

### **Observed output**

```text
Header spans full viewport width.
```

### **Common pitfalls**

- ❌ Horizontal overflow with scrollbars
    
- ❌ Confusing with %
    

### **Failure example**

```css
body {
  margin: 0;
}
div {
  width: 100vw;
}
```

**Failure:** horizontal scroll appears

### **Correct alternative**

```css
div {
  width: 100%;
}
```

### **Observed output**

```text
No horizontal overflow.
```

---

## 7️⃣ `auto(contextDrivenValue)`

### **Purpose (Mandatory — do not skip)**

- Delegates value calculation to browser
    
- Context-dependent resolution
    
- Default for many properties
    

### **Method**

```css
property: auto;
```

### **Correct usage**

```css
div {
  margin: auto;
}
```

### **Observed output**

```text
Element is horizontally centered.
```

### **Common pitfalls**

- ❌ Assuming auto always means zero
    
- ❌ Using auto where unsupported
    

### **Failure example**

```css
div {
  height: auto;
}
```

**Failure:** no visible change expected but none occurs

### **Correct alternative**

```css
div {
  min-height: auto;
}
```

### **Observed output**

```text
Height adjusts to content.
```

---

## 8️⃣ `inherit(valueInheritance)`

### **Purpose (Mandatory — do not skip)**

- Forces property to inherit from parent
    
- Overrides default inheritance rules
    
- Explicit inheritance
    

### **Method**

```css
property: inherit;
```

### **Correct usage**

```css
div {
  color: red;
}
p {
  color: inherit;
}
```

### **Observed output**

```text
Paragraph text is red.
```

### **Common pitfalls**

- ❌ Assuming all properties inherit
    
- ❌ Overusing inherit unnecessarily
    

### **Failure example**

```css
div {
  border: inherit;
}
```

**Failure:** no inherited border exists

### **Correct alternative**

```css
div {
  border-color: inherit;
}
```

### **Observed output**

```text
Border color inherited correctly.
```

---

## 🚨 Conceptual Pitfalls (Very Important)

- ❌ `%` is not always relative to viewport
    
    ```css
    height: 50%;
    ```
    
    ```text
    Requires parent height.
    ```
    
- ✅ `%` is relative to **containing block**
    
- ❌ `em` is stable like `rem`
    
- ✅ `em` compounds, `rem` does not
    

---

## 🧠 Mental Model (Exam + Design)

- Units define **measurement context**
    
- Guarantees:
    
    - Deterministic resolution per unit
        
- Undefined:
    
    - Device pixel mapping
        
- Rules live in:
    
    - CSS Values & Units spec
        
    - Layout engine
        

---

## 📌 Summary Table

|Unit|Purpose|Common Pitfall|
|---|---|---|
|px|Fixed length|Non-scalable|
|%|Parent-relative|Missing parent size|
|em|Parent font-relative|Compounding|
|rem|Root font-relative|Global changes|
|vh|Viewport height|Mobile overflow|
|vw|Viewport width|Scrollbar overflow|
|auto|Browser-calculated|Wrong assumptions|
|inherit|Forced inheritance|No source value|

---

## ✅ Golden Rule

Use **px for precision**, **rem for typography**, **% for layout**, and **viewport units sparingly**.  
Always know **what the value is relative to** before using a unit.

**Next topic:** Colors
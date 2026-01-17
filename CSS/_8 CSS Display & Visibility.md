# 🟠 CSS Display & Visibility — Methods, Pitfalls, Fixes

> `CSS Display & Visibility` control **how elements participate in layout** and **whether they are rendered or interactable**.

---

## 1️⃣ `display:block`

### **Purpose (Mandatory — do not skip)**

- Makes element a **block-level box**
    
- Starts on a new line
    
- Accepts width/height/margin/padding
    
- Participates fully in normal flow
    

### **Method**

```css
display: block;
```

### **Correct usage**

```css
div {
  display: block;
}
```

### **Observed output**

```text
Element occupies full available width and starts on a new line.
```

### **Common pitfalls**

- ❌ Assuming block means fixed width
    
- ❌ Forgetting margins affect layout
    

### **Failure example**

```css
span {
  display: block;
  width: auto;
}
```

**Failure:** expecting inline-like sizing

### **Correct alternative**

```css
span {
  display: inline-block;
}
```

### **Observed output**

```text
Element sizes to content while allowing dimensions.
```

---

## 2️⃣ `display:inline`

### **Purpose (Mandatory — do not skip)**

- Places element **in text flow**
    
- Does **not accept width/height**
    
- Margin applies horizontally only
    

### **Method**

```css
display: inline;
```

### **Correct usage**

```css
span {
  display: inline;
}
```

### **Observed output**

```text
Element flows with text.
```

### **Common pitfalls**

- ❌ Trying to set width/height
    
- ❌ Expecting vertical margins to apply
    

### **Failure example**

```css
span {
  width: 200px;
}
```

**Failure:** width ignored

### **Correct alternative**

```css
span {
  display: inline-block;
  width: 200px;
}
```

### **Observed output**

```text
Width is respected.
```

---

## 3️⃣ `display:inline-block`

### **Purpose (Mandatory — do not skip)**

- Hybrid of inline and block
    
- Stays inline **but** accepts dimensions
    
- Does not force line break
    

### **Method**

```css
display: inline-block;
```

### **Correct usage**

```css
button {
  display: inline-block;
  width: 120px;
}
```

### **Observed output**

```text
Button stays inline and has fixed width.
```

### **Common pitfalls**

- ❌ Ignoring whitespace gaps
    
- ❌ Expecting full-width behavior
    

### **Failure example**

```css
div {
  display: inline-block;
}
```

**Failure:** expecting block stacking

### **Correct alternative**

```css
div {
  display: block;
}
```

### **Observed output**

```text
Elements stack vertically.
```

---

## 4️⃣ `display:none`

### **Purpose (Mandatory — do not skip)**

- Removes element **entirely from layout**
    
- No space reserved
    
- Element is non-interactive
    

### **Method**

```css
display: none;
```

### **Correct usage**

```css
.modal {
  display: none;
}
```

### **Observed output**

```text
Element is not rendered and takes no space.
```

### **Common pitfalls**

- ❌ Confusing with `visibility: hidden`
    
- ❌ Expecting transitions to work
    

### **Failure example**

```css
div {
  transition: opacity 0.3s;
  display: none;
}
```

**Failure:** transition never runs

### **Correct alternative**

```css
div {
  opacity: 0;
  visibility: hidden;
}
```

### **Observed output**

```text
Element fades out smoothly.
```

---

## 5️⃣ `visibility:hidden`

### **Purpose (Mandatory — do not skip)**

- Hides element visually
    
- **Layout space is preserved**
    
- Element is non-interactive
    

### **Method**

```css
visibility: hidden;
```

### **Correct usage**

```css
p {
  visibility: hidden;
}
```

### **Observed output**

```text
Paragraph invisible but space remains.
```

### **Common pitfalls**

- ❌ Expecting layout collapse
    
- ❌ Assuming element is clickable
    

### **Failure example**

```css
button {
  visibility: hidden;
}
```

**Failure:** invisible button still occupies space

### **Correct alternative**

```css
button {
  display: none;
}
```

### **Observed output**

```text
Button removed from layout.
```

---

## 6️⃣ `opacity(alphaValue)`

### **Purpose (Mandatory — do not skip)**

- Applies **visual transparency**
    
- Value range: `0` to `1`
    
- Element remains in layout and interactive
    

### **Method**

```css
opacity: <number>;
```

### **Correct usage**

```css
div {
  opacity: 0.5;
}
```

### **Observed output**

```text
Element is semi-transparent.
```

### **Common pitfalls**

- ❌ Expecting click-through
    
- ❌ Forgetting children are affected
    

### **Failure example**

```css
a {
  opacity: 0;
}
```

**Failure:** invisible but clickable element

### **Correct alternative**

```css
a {
  display: none;
}
```

### **Observed output**

```text
Element fully removed.
```

---

## 🚨 Conceptual Pitfalls (Very Important)

- ❌ `display:none` == `visibility:hidden`
    
    ```css
    display: none;
    ```
    
    ```text
    No layout space.
    ```
    
    ```css
    visibility: hidden;
    ```
    
    ```text
    Space preserved.
    ```
    
- ❌ `opacity: 0` hides element completely
    
- ✅ Element is still **present and interactive**
    

---

## 🧠 Mental Model (Exam + Design)

- `display` controls **layout participation**
    
- `visibility` controls **visual presence**
    
- `opacity` controls **alpha blending**
    
- Guarantees:
    
    - Deterministic layout rules
        
- Undefined:
    
    - User interaction intent
        
- Rules live in:
    
    - CSS Display spec
        
    - Rendering engine
        

---

## 📌 Summary Table

|Property|Purpose|Common Pitfall|
|---|---|---|
|display:block|Full-width block|Assuming fixed size|
|display:inline|Text flow|Width ignored|
|inline-block|Hybrid box|Whitespace gaps|
|display:none|Remove element|No transitions|
|visibility:hidden|Hide visually|Space remains|
|opacity|Transparency|Still clickable|

---

## ✅ Golden Rule

If you want to **remove layout**, use `display:none`.  
If you want to **hide but keep space**, use `visibility:hidden`.  
If you want **fade effects**, use `opacity` — but remember it does not disable interaction.

**Next topic:** Positioning
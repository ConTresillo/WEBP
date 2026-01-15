# 🟠 HTML — Text Formatting Tags

> `HTML Text Formatting` tags provide **inline semantic meaning** to text fragments; they affect **interpretation and accessibility**, not layout logic or document structure.

---

---

## 3️⃣ `<strong>` — Strong Importance

### **Purpose (Mandatory — do not skip)**

- Marks text as **strongly important**
    
- Conveys **semantic emphasis**, not just bold styling
    
- Screen readers announce increased importance
    
- **Inline**, **eager**, **finite**
    

---

### **Method**

```html
<strong> … </strong>
```

---

### **Correct usage**

```html
<p>This is <strong>important</strong> information.</p>
```

---

### **Observed output**

```text
This is important information.
```

(Visually bold by default)

---

### **Common pitfalls**

- ❌ Using `<strong>` purely for bold text
    
- ❌ Replacing headings with `<strong>`
    

---

### **Failure example**

```html
<strong>Main Title</strong>
```

**Failure:**  
Semantic misuse (heading meaning lost)

---

### **Correct alternative**

```html
<h1>Main Title</h1>
```

---

### **Observed output**

```text
Main Title
```

---

## 4️⃣ `<em>` — Emphasis

### **Purpose (Mandatory — do not skip)**

- Indicates **stress emphasis** in text
    
- Changes meaning when spoken aloud
    
- Nested `<em>` increases emphasis level
    
- **Inline**, **eager**
    

---

### **Method**

```html
<em> … </em>
```

---

### **Correct usage**

```html
<p>You must <em>not</em> skip this step.</p>
```

---

### **Observed output**

```text
You must not skip this step.
```

(Italicized by default)

---

### **Common pitfalls**

- ❌ Using `<em>` only for italics
    
- ❌ Confusing with `<i>`
    

---

### **Failure example**

```html
<em>Chapter 1</em>
```

**Failure:**  
Incorrect emphasis semantics

---

### **Correct alternative**

```html
<i>Chapter 1</i>
```

---

### **Observed output**

```text
Chapter 1
```

---

## 5️⃣ `<b>` — Bold (No Semantic Importance)

### **Purpose (Mandatory — do not skip)**

- Applies **visual bold styling only**
    
- No added semantic importance
    
- Ignored by accessibility tools
    
- **Inline**, **eager**
    

---

### **Method**

```html
<b> … </b>
```

---

### **Correct usage**

```html
<p><b>Note:</b> This is informational.</p>
```

---

### **Observed output**

```text
Note: This is informational.
```

---

### **Common pitfalls**

- ❌ Using `<b>` instead of `<strong>`
    
- ❌ Assuming screen readers emphasize it
    

---

### **Failure example**

```html
<b>Critical Warning</b>
```

**Failure:**  
Importance not conveyed to assistive tech

---

### **Correct alternative**

```html
<strong>Critical Warning</strong>
```

---

### **Observed output**

```text
Critical Warning
```

---

## 6️⃣ `<i>` — Italic (Alternate Voice / Term)

### **Purpose (Mandatory — do not skip)**

- Represents **alternate voice, term, or notation**
    
- No emphasis or importance implied
    
- **Inline**, **eager**
    

---

### **Method**

```html
<i> … </i>
```

---

### **Correct usage**

```html
<p>The term <i>latency</i> refers to delay.</p>
```

---

### **Observed output**

```text
The term latency refers to delay.
```

---

### **Common pitfalls**

- ❌ Using `<i>` for emphasis
    
- ❌ Confusing with `<em>`
    

---

### **Failure example**

```html
<i>Do not delete</i>
```

**Failure:**  
No emphasis conveyed

---

### **Correct alternative**

```html
<em>Do not delete</em>
```

---

### **Observed output**

```text
Do not delete
```

---

## 7️⃣ `<u>` — Unarticulated Annotation

### **Purpose (Mandatory — do not skip)**

- Marks text with **non-emphasis annotation**
    
- Historically underline; semantics are weak
    
- **Inline**, **eager**
    

---

### **Method**

```html
<u> … </u>
```

---

### **Correct usage**

```html
<p><u>Spelling error</u></p>
```

---

### **Observed output**

```text
Spelling error
```

(Underlined)

---

### **Common pitfalls**

- ❌ Using `<u>` for links
    
- ❌ Using for emphasis
    

---

### **Failure example**

```html
<u>Click here</u>
```

**Failure:**  
Misleading link affordance

---

### **Correct alternative**

```html
<a href="#">Click here</a>
```

---

### **Observed output**

```text
Clickable link
```

---

## 8️⃣ `<mark>` — Highlighted Text

### **Purpose (Mandatory — do not skip)**

- Marks text as **relevant or highlighted**
    
- Indicates contextual importance
    
- **Inline**, **eager**
    

---

### **Method**

```html
<mark> … </mark>
```

---

### **Correct usage**

```html
<p>Search result: <mark>HTML</mark></p>
```

---

### **Observed output**

```text
Search result: HTML
```

(Yellow highlight by default)

---

### **Common pitfalls**

- ❌ Using `<mark>` for styling only
    
- ❌ Overusing highlights
    

---

### **Failure example**

```html
<mark>Entire paragraph highlighted</mark>
```

**Failure:**  
Semantic dilution

---

### **Correct alternative**

```html
<p>Keyword: <mark>HTML</mark></p>
```

---

### **Observed output**

```text
Keyword: HTML
```

---

## 🚨 Conceptual Pitfalls (Very Important)

❌ **`<b>` vs `<strong>`**

```html
<b>Error</b>
```

```text
Bold text only
```

✅ Use `<strong>` when importance matters

---

❌ **`<i>` vs `<em>`**

```html
<i>Warning</i>
```

```text
Italic without emphasis
```

✅ Use `<em>` for stress emphasis

---

❌ **Formatting vs Meaning**

```html
<strong><i><u>Text</u></i></strong>
```

```text
Visually heavy, semantically unclear
```

✅ Choose one tag that matches intent

---

## 🧠 Mental Model (Exam + Design)

- Formatting tags are **inline semantics**
    
- They modify **meaning**, not structure
    
- Accessibility relies on **correct tag choice**
    
- Visual appearance is browser-default, not guaranteed
    
- CSS can override visuals, not semantics
    

---

## 📌 Summary Table

|Tag|Purpose|Common Pitfall|
|---|---|---|
|`<strong>`|Importance|Used for bold|
|`<em>`|Emphasis|Confused with `<i>`|
|`<b>`|Visual bold|Used for importance|
|`<i>`|Alternate voice|Used for emphasis|
|`<u>`|Annotation|Used like link|
|`<mark>`|Highlight|Overuse|

---

## ✅ Golden Rule

Choose text formatting tags based on **meaning first**,  
and let **CSS handle appearance**.
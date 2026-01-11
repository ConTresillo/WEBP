# 🟠 HTML — Form Validation & Attributes (`required`, `pattern`, `min`, `max`, `step`, `placeholder`, `readonly`, `disabled`) — Methods, Pitfalls, Fixes

> `HTML Form Validation Attributes` define **client-side constraints and behavior** for form controls; they participate in **native validation**, submission blocking, and user feedback, but **do not replace server-side validation**.

---

---

## 1️⃣ `required` — Mandatory Value Constraint

### **Purpose (Mandatory — do not skip)**

- Marks an input as **non-optional**
    
- Prevents form submission if value is missing
    
- Participates in native browser validation
    
- **Eager**, enforced at submit time
    

---

### **Method**

```html
<input required>
```

---

### **Correct usage**

```html
<input type="text" name="username" required>
```

---

### **Observed output**

```text
Form blocked if empty
```

---

### **Common pitfalls**

- ❌ Assuming it validates format
    
- ❌ Using without a visible label
    

---

### **Failure example**

```html
<input required>
```

**Failure:**  
User does not know what is required (UX failure)

---

### **Correct alternative**

```html
<label>
  Username
  <input name="username" required>
</label>
```

---

### **Observed output**

```text
Submission blocked until filled
```

---

## 2️⃣ `pattern` — Regex Constraint

### **Purpose (Mandatory — do not skip)**

- Enforces a **regular-expression-based format**
    
- Applied only to **text-like inputs**
    
- Validation occurs on submit
    
- **Finite**, **eager**
    

---

### **Method**

```html
<input pattern="regex">
```

---

### **Correct usage**

```html
<input type="text" pattern="[0-9]{5}" name="pin">
```

---

### **Observed output**

```text
Only 5-digit values accepted
```

---

### **Common pitfalls**

- ❌ Assuming full JavaScript regex support
    
- ❌ Using without `title` for error hint
    

---

### **Failure example**

```html
<input pattern="\d+">
```

**Failure:**  
Backslash escaping may behave unexpectedly

---

### **Correct alternative**

```html
<input pattern="[0-9]+" title="Digits only">
```

---

### **Observed output**

```text
Helpful validation message shown
```

---

## 3️⃣ `min` — Minimum Value Constraint

### **Purpose (Mandatory — do not skip)**

- Sets **lower bound** for numeric/date inputs
    
- Enforced by browser UI and validation
    
- Applies to `number`, `date`, `range`, etc.
    
- **Eager**, submit-time enforced
    

---

### **Method**

```html
<input min="value">
```

---

### **Correct usage**

```html
<input type="number" name="age" min="18">
```

---

### **Observed output**

```text
Values < 18 rejected
```

---

### **Common pitfalls**

- ❌ Assuming it affects text inputs
    
- ❌ Relying on it for security
    

---

### **Failure example**

```html
<input type="text" min="5">
```

**Failure:**  
Attribute ignored

---

### **Correct alternative**

```html
<input type="number" min="5">
```

---

### **Observed output**

```text
Lower bound enforced
```

---

## 4️⃣ `max` — Maximum Value Constraint

### **Purpose (Mandatory — do not skip)**

- Sets **upper bound** for numeric/date inputs
    
- Works with browser UI controls
    
- Enforced at submission
    
- **Eager**
    

---

### **Method**

```html
<input max="value">
```

---

### **Correct usage**

```html
<input type="number" name="score" max="100">
```

---

### **Observed output**

```text
Values > 100 rejected
```

---

### **Common pitfalls**

- ❌ Assuming inclusive/exclusive ambiguity (it is inclusive)
    
- ❌ Using without `min` when range matters
    

---

### **Failure example**

```html
<input type="text" max="10">
```

**Failure:**  
No effect

---

### **Correct alternative**

```html
<input type="number" max="10">
```

---

### **Observed output**

```text
Upper bound enforced
```

---

## 5️⃣ `step` — Increment Constraint

### **Purpose (Mandatory — do not skip)**

- Restricts **allowed increments**
    
- Applies to numeric/date/range inputs
    
- Validation fails if value not aligned
    
- **Finite**, **eager**
    

---

### **Method**

```html
<input step="value">
```

---

### **Correct usage**

```html
<input type="number" step="0.5">
```

---

### **Observed output**

```text
Only multiples of 0.5 allowed
```

---

### **Common pitfalls**

- ❌ Assuming rounding happens automatically
    
- ❌ Forgetting interaction with `min`
    

---

### **Failure example**

```html
<input type="number" step="2" value="3">
```

**Failure:**  
Invalid step mismatch

---

### **Correct alternative**

```html
<input type="number" step="1">
```

---

### **Observed output**

```text
Valid integer accepted
```

---

## 6️⃣ `placeholder` — Hint Text

### **Purpose (Mandatory — do not skip)**

- Provides **example or hint** inside input
    
- Disappears when user types
    
- Not a label
    
- **Non-semantic**, **visual-only**
    

---

### **Method**

```html
<input placeholder="text">
```

---

### **Correct usage**

```html
<input placeholder="Enter email">
```

---

### **Observed output**

```text
Faded hint text shown
```

---

### **Common pitfalls**

- ❌ Using instead of `<label>`
    
- ❌ Assuming it is submitted
    

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
  <input placeholder="name@example.com">
</label>
```

---

### **Observed output**

```text
Accessible + helpful hint
```

---

## 7️⃣ `readonly` — Immutable but Submittable

### **Purpose (Mandatory — do not skip)**

- Prevents user editing
    
- Value **is submitted**
    
- Input remains focusable
    
- **Eager**, static
    

---

### **Method**

```html
<input readonly>
```

---

### **Correct usage**

```html
<input name="id" value="42" readonly>
```

---

### **Observed output**

```text
id=42
```

---

### **Common pitfalls**

- ❌ Confusing with `disabled`
    
- ❌ Using for security
    

---

### **Failure example**

```html
<input readonly>
```

**Failure:**  
No value to protect

---

### **Correct alternative**

```html
<input value="fixed" readonly>
```

---

### **Observed output**

```text
Value locked and submitted
```

---

## 8️⃣ `disabled` — Inactive Control

### **Purpose (Mandatory — do not skip)**

- Prevents interaction and focus
    
- Value **is NOT submitted**
    
- Removed from validation
    
- **Eager**, static
    

---

### **Method**

```html
<input disabled>
```

---

### **Correct usage**

```html
<input name="token" value="abc" disabled>
```

---

### **Observed output**

```text
token not submitted
```

---

### **Common pitfalls**

- ❌ Expecting value to submit
    
- ❌ Using instead of `readonly`
    

---

### **Failure example**

```html
<input name="x" value="1" disabled>
```

**Failure:**  
Missing data on submit

---

### **Correct alternative**

```html
<input name="x" value="1" readonly>
```

---

### **Observed output**

```text
x=1
```

---

## 🚨 Conceptual Pitfalls (Very Important)

❌ **Client-side validation = security**

```html
<input required>
```

```text
Bypassable
```

✅ Always validate on server

---

❌ **`placeholder` as label**

```html
<input placeholder="Name">
```

```text
Accessibility failure
```

✅ Use `<label>`

---

❌ **`disabled` vs `readonly`**

```html
<input disabled value="5">
```

```text
Value dropped
```

✅ Use `readonly` if submission is required

---

## 🧠 Mental Model (Exam + Design)

- Validation attributes define **constraints, not trust**
    
- Browser enforces rules **only at submit**
    
- `required`, `pattern`, `min/max/step` block submission
    
- `readonly` keeps value; `disabled` removes it
    
- Server-side validation is authoritative
    

---

## 📌 Summary Table

|Attribute|Purpose|Common Pitfall|
|---|---|---|
|`required`|Mandatory input|No label|
|`pattern`|Regex format|Poor regex|
|`min`|Lower bound|Wrong type|
|`max`|Upper bound|Missing min|
|`step`|Increment rule|Step mismatch|
|`placeholder`|Hint text|Used as label|
|`readonly`|Locked value|Confused with disabled|
|`disabled`|Inactive input|Value not submitted|

---

## ✅ Golden Rule

HTML validation **guides users**, it does not enforce trust.  
If correctness matters, assume **all client validation can be bypassed**.
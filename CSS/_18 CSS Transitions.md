
---

# 🟠 CSS Transitions — Methods, Pitfalls, Fixes

> `CSS Transitions` define **how property changes occur over time**, enabling smooth visual interpolation between states.

---

## 1️⃣ `transition-property`

### **Purpose (Mandatory — do not skip)**

- Specifies **which CSS properties are animated**
    
- Only properties that are **animatable** can transition
    
- Does nothing by itself without duration
    

### **Method**

```css
transition-property: <property> | all | none;
```

### **Correct usage**

```css
button {
  transition-property: background-color;
}
```

### **Observed output**

```text
Only background-color changes animate when the value changes.
```

### **Common pitfalls**

- ❌ Assuming all properties animate by default
    
- ❌ Using `all` unnecessarily
    

### **Failure example**

```css
div {
  transition-property: display;
}
```

**Failure:** `display` is not animatable → ignored

### **Correct alternative**

```css
div {
  transition-property: opacity;
}
```

### **Observed output**

```text
Opacity transitions smoothly.
```

---

## 2️⃣ `transition-duration`

### **Purpose (Mandatory — do not skip)**

- Defines **how long the transition takes**
    
- Required for any visible transition
    
- Default value is `0s` (no animation)
    

### **Method**

```css
transition-duration: <time>;
```

### **Correct usage**

```css
button {
  transition-duration: 0.3s;
}
```

### **Observed output**

```text
Transition completes in 0.3 seconds.
```

### **Common pitfalls**

- ❌ Forgetting duration entirely
    
- ❌ Using excessively long durations
    

### **Failure example**

```css
button {
  transition-duration: 0s;
}
```

**Failure:** no visible transition

### **Correct alternative**

```css
button {
  transition-duration: 300ms;
}
```

### **Observed output**

```text
Smooth transition visible.
```

---

## 3️⃣ `transition-timing-function`

### **Purpose (Mandatory — do not skip)**

- Controls **speed curve** of the transition
    
- Does not change duration, only pacing
    
- Affects perceived smoothness
    

### **Method**

```css
transition-timing-function: ease | linear | ease-in | ease-out | ease-in-out;
```

### **Correct usage**

```css
button {
  transition-timing-function: ease-in-out;
}
```

### **Observed output**

```text
Transition starts and ends smoothly.
```

### **Common pitfalls**

- ❌ Thinking it changes duration
    
- ❌ Overusing `linear` for UI elements
    

### **Failure example**

```css
button {
  transition-timing-function: linear;
}
```

**Failure:** robotic, unnatural motion

### **Correct alternative**

```css
button {
  transition-timing-function: ease;
}
```

### **Observed output**

```text
Natural UI motion.
```

---

## 4️⃣ `transition-delay`

### **Purpose (Mandatory — do not skip)**

- Delays the **start** of the transition
    
- Does not affect duration
    
- Can cause perceived lag
    

### **Method**

```css
transition-delay: <time>;
```

### **Correct usage**

```css
button {
  transition-delay: 0.1s;
}
```

### **Observed output**

```text
Transition starts after 0.1 seconds.
```

### **Common pitfalls**

- ❌ Using delay without intent
    
- ❌ Causing unresponsive UI
    

### **Failure example**

```css
button {
  transition-delay: 1s;
}
```

**Failure:** UI feels broken or slow

### **Correct alternative**

```css
button {
  transition-delay: 0s;
}
```

### **Observed output**

```text
Immediate response.
```

---

## 5️⃣ `transition (shorthand)`

### **Purpose (Mandatory — do not skip)**

- Combines all transition sub-properties
    
- Most commonly used form
    
- Missing values revert to defaults
    

### **Method**

```css
transition: <property> <duration> <timing-function> <delay>;
```

### **Correct usage**

```css
button {
  transition: background-color 0.3s ease;
}
```

### **Observed output**

```text
Background color animates smoothly on change.
```

### **Common pitfalls**

- ❌ Wrong order assumptions
    
- ❌ Forgetting property name
    

### **Failure example**

```css
button {
  transition: 0.3s ease;
}
```

**Failure:** property defaults to `all` unintentionally

### **Correct alternative**

```css
button {
  transition: transform 0.3s ease;
}
```

### **Observed output**

```text
Only transform animates.
```

---

## 6️⃣ `hover-based transitions` (Most Common Use)

### **Purpose (Mandatory — do not skip)**

- Transitions occur when **state changes**
    
- Requires both:
    
    - initial state
        
    - changed state (`:hover`, `:focus`, etc.)
        

### **Method**

```css
selector {
  transition: ...;
}
selector:hover {
  property: new-value;
}
```

### **Correct usage**

```css
button {
  transition: transform 0.2s ease;
}
button:hover {
  transform: scale(1.05);
}
```

### **Observed output**

```text
Button smoothly scales on hover.
```

### **Common pitfalls**

- ❌ Putting transition only in `:hover`
    
- ❌ Expecting reverse animation without base state
    

### **Failure example**

```css
button:hover {
  transition: transform 0.2s;
  transform: scale(1.05);
}
```

**Failure:** transition applies only in one direction

### **Correct alternative**

```css
button {
  transition: transform 0.2s;
}
```

### **Observed output**

```text
Smooth enter and exit animation.
```

---

## 🚨 Conceptual Pitfalls (Very Important)

❌ Transitions run automatically

```css
transition: 0.3s;
```

```text
They only run when a value CHANGES.
```

---

❌ Any property can be transitioned

```css
transition: display 0.3s;
```

```text
Non-animatable properties are ignored.
```

---

## 🧠 Mental Model (Exam + Design)

- Transitions exist to:
    
    - Smooth **state changes**
        
- Guarantees:
    
    - Interpolated animation
        
- Does NOT guarantee:
    
    - Complex timelines
        
    - Looping
        
- Rules live in:
    
    - CSS Transitions spec
        
    - Rendering engine
        

---

## 📌 Summary Table

|Property|Purpose|Common Pitfall|
|---|---|---|
|transition-property|What animates|Non-animatable props|
|transition-duration|How long|Missing duration|
|timing-function|Speed curve|Robotic motion|
|transition-delay|Start delay|UI lag|
|transition (shorthand)|Combine all|Unintended `all`|
|hover transitions|State-based motion|One-sided animation|

---

## ✅ Golden Rule

**Transitions animate changes — not elements.**  
If nothing changes, nothing moves.

---

👉 **Next topic:** Transforms
Yes — **relative units like `rem`, `em`, `vh`, `vw`, `%` are valid and expected** in CSS, **but only where the property accepts a `<length>` or `<percentage>` value**.

Below is the precise, exam-safe rule set.

---

## Where relative units **ARE allowed**

Any property that accepts **length values** can use them.

### Common examples (all valid)

```css
width: 50%;
height: 100vh;
margin: 1rem;
padding: 2em;
font-size: 1.25rem;
top: 10vh;
gap: 1rem;
border-radius: 0.5rem;
```

These properties are **unit-agnostic** → they accept:

- `px`
    
- `%`
    
- `em`
    
- `rem`
    
- `vh / vw`
    

---

## Where relative units **ARE NOT allowed**

Properties that expect **keywords, enums, or non-length values**.

### Invalid examples

```css
display: 10px;        /* ❌ expects keyword */
position: 2rem;      /* ❌ expects keyword */
color: 1rem;         /* ❌ expects color */
z-index: 2rem;       /* ❌ expects integer */
font-weight: 2rem;   /* ❌ expects number/keyword */
opacity: 50%;        /* ❌ expects 0–1 number */
```

These properties **do not accept units at all**.

---

## Subtle but important exam traps

### 1️⃣ `%` depends on **context**

```css
height: 50%;
```

✅ Works **only if parent has explicit height**  
❌ Otherwise resolves to `auto`

---

### 2️⃣ `em` compounds, `rem` does not

```css
font-size: 1.5em;  /* relative to parent */
font-size: 1.5rem; /* relative to root */
```

Exams often test this difference.

---

### 3️⃣ `vh / vw` ignore parents

```css
width: 100vw;
```

- Relative to viewport
    
- Can cause horizontal scrollbars  
    (very common MCQ)
    

---

## Exam-safe mental rule

> **If a property accepts `<length>` → you may use `px`, `%`, `em`, `rem`, `vh`, `vw`.**  
> **If a property expects a keyword or number → units are invalid.**

---

## One-line memory hook (use this in exam)

> **Units belong to measurements, not behaviors.**

If you want, next we continue with **Display & Visibility** (this section has many unit-related traps too).
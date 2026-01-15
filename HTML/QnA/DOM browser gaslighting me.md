It’s not gaslighting. You ran into **browser state**, not HTML behavior.  
Now that you’ve shown this screenshot, the situation is unambiguous.

Here is the exact, final explanation.

---

## What actually happened

### 1️⃣ You opened the page at `#images`

Look at your address bar in the screenshot:

```
...Practice-semantic-knowledge-portal.html#images
```

That means:

- The browser **already navigated** to `#images`
    
- So the link **Images** is now in the **visited state**
    
- The browser remembers this in history
    

---

## 2️⃣ Browsers style links by HISTORY, not by HTML

Even with **zero CSS**, the browser applies its own internal CSS called the **user-agent stylesheet**.

Default behavior (simplified):

|State|Browser does|
|---|---|
|unvisited link|blue + underline|
|visited link|different color (often purple / black-ish)|
|hover|underline|
|active|temporary highlight|

So when you previously clicked:

- Introduction
    
- Text Formatting
    
- Lists
    
- Table
    
- Images
    

Each one silently moved from `:link` → `:visited`.

That’s why earlier:

- Some looked blue
    
- Some looked black
    
- Some looked inconsistent
    

Nothing was broken. The browser was remembering your actions.

---

## 3️⃣ Why it suddenly “started working”

You either:

- Opened the page fresh
    
- Navigated directly to `#images`
    
- Or refreshed after history updated
    

So now **all links are clearly links**, and clicking them visibly jumps.

Same HTML.  
Different **browser history state**.

---

## 4️⃣ Why this is confusing (and common)

HTML beginners assume:

> “If it doesn’t look clickable, it isn’t a link.”

That is false.

Correct mental model:

> **HTML defines capability.  
> CSS (including browser default CSS) defines appearance.  
> Browser history modifies appearance again.**

You were debugging **the wrong layer**.

---

## 5️⃣ Absolute proof (no opinions)

If a link were missing `href`:

- Right-click → “Copy link address” would be disabled
    
- URL would not contain `#id`
    
- Clicking would do nothing at all
    

In your case:

- URL updates
    
- Page jumps
    
- History records it
    

So the `href` was **always there**.

---

## Final verdict (locked)

- Your HTML was correct
    
- Your anchors were correct
    
- Your IDs were correct
    
- The browser was not lying
    
- You were seeing **visited-link styling + history state**
    

This is a **real-world debugging lesson**, not a mistake.

---

You’re done with this issue.  
There is nothing left to fix here.

Next sensible step:

- **Semantic refactor** (header/nav/main/section/aside), or
    
- **Project 2: Forms** (much stricter, no browser forgiveness)
    

Say which one.
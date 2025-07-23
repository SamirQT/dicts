## Part 1 – Theory & Code Reading (Explain What Happens)

**Given Code (do NOT edit it during Part 1):**

```python
data = {
    "user": {"name": "Aya", "age": 22},
    "roles": ["author"],
    "taxes": {"US": 0.07, "CA": 0.13}
}

profile = data          # (A)
shadow = data.copy()    # (B)

# Mutations
data["roles"].append("editor")            # (C)
shadow["taxes"]["EU"] = 0.20              # (D)
value = data.get("missing", "N/A")        # (E)
old = data.pop("user")                    # (F)
last_pair = data.popitem()                # (G)

# View objects
k_view = data.keys()                      # (H)
v_view = data.values()                    # (I)
i_view = data.items()                     # (J)

data.setdefault("logs", []).append("ok")  # (K)

# Rebuild from keys
defaults = dict.fromkeys(["a", "b", "c"], 0)  # (L)

# Clean slate
clean = {}
clean.update(defaults)                    # (M)
clean.clear()                             # (N)
```

### Your Tasks

1. **Aliasing vs Copy:**

   * Which line(s) create aliases? Which create copies? Explain (A) and (B).

2. **After (C):**

   * What are the contents of `data["roles"]` and `shadow["roles"]`? Why?

3. **After (D):**

   * What are the contents of `data["taxes"]` and `shadow["taxes"]`? Why?

4. **`get` Behavior:**

   * What is stored in `value` after (E)? Why doesn’t it raise an error?

5. **`pop` vs `del`:**

   * What does `old` hold after (F)?
   * What exactly does `popitem()` (G) return, and how is it chosen?

6. **View Objects:**

   * After (H), (I), (J), are `k_view`, `v_view`, and `i_view` snapshots or live views?
   * Show how adding a new key to `data` would affect them.

7. **`setdefault`:**

   * At (K), explain how `setdefault` works here and what happens if called again with the same key.

8. **`dict.fromkeys`:**

   * What does `defaults` contain after (L)? What happens if you mutate one of the values?

9. **`update` and `clear`:**

   * After (M) and (N), what are the contents of `clean`?
   * Why might `clear()` be safer than reassigning `clean = {}` in some scenarios?

10. **Insertion Order:**

    * Which operations (above) affect insertion order? Which don’t? Explain briefly.

> **Deliverable:** Short written answers for each question. Be precise and refer to line letters (A)…(N).

---

## Part 2 – Hands‑On Coding

### Exercise 1 – “Method Playground” (Use Every Dict Method Once)

**Goal:** Write a script (`methods_playground.py`) that manipulates a given dictionary using **all** of these methods at least once:
`get`, `keys`, `values`, `items`, `update`, `pop`, `popitem`, `clear`, `setdefault`, `dict.fromkeys`

**Starter Data (use exactly):**

```python
prices = {"apple": 0.5, "banana": 0.3, "cherry": 0.8}
tax_rates = {"US": 0.07, "CA": 0.13}
```

**Required Steps (order is up to you, but show each call clearly):**

1. Safely read a non‑existing price with `get` (provide a default).
2. Add a new fruit and update an existing fruit’s price with `update`.
3. Remove one key with `pop` and capture its value.
4. Use `popitem` to remove the last inserted item; store the returned pair.
5. Build a dict of “discounts” with `dict.fromkeys(["apple","banana"], 0.1)` and merge it into your data.
6. Use `setdefault` to ensure there is a `"logs"` list and append a message to it.
7. Show `keys()`, `values()`, `items()` (e.g., print them) and explain in a comment whether they’re live views or snapshots.
8. Finally, copy the dict to a new variable, then `clear()` the original. Print both to show the difference.

**Constraints:**

* No dict/list comprehensions.
* No classes, no imports except `copy` if you really need it (not required here).
* Keep code linear and readable, no fancy algorithms.

**Deliverable:** A runnable `.py` file. Include brief inline comments explaining what each method call is doing.

---

### Exercise 2 – “View Objects & Lists in Sync”

**Scenario:** You’re tracking participants of three workshops. Each workshop has a list of students. You need to:

* Use dict **view objects** to monitor changes live.
* Use lists for the participants (no comprehensions).
* Avoid algorithmic logic: simple appends/removals/prints are fine.

**Starter Data:**

```python
workshops = {
    "Python 101": ["Aya", "Sam"],
    "Web Basics": ["Lina"],
    "Data Entry": []
}
```

**Tasks:**

1. Create `names_view = workshops.keys()` and `groups_view = workshops.values()`. Print them.
2. Add a new workshop key after creating the views. Show that the views reflect the new key.
3. For each workshop, if the list is empty, use `setdefault` to ensure there is a list, then append `"TBD"`.
4. Remove one student from `"Python 101"` using list operations. Show that `groups_view` reflects this change.
5. Take a **snapshot** of current keys and values into two lists (`list(names_view)`, `list(groups_view)`). Then add another workshop and show that the snapshots do NOT change.
6. Use `items()` to iterate and print “Workshop: X has Y students”.
7. Clean up: use `pop` to remove `"Data Entry"`, and finally `popitem()` to remove the last workshop. Print final state.

**Constraints:**

* No comprehensions.
* No classes, no external imports.
* Simple loops (`for w in workshops:`) are okay.

**Deliverable:** A `.py` file with clear prints that demonstrate the live vs snapshot behavior. Comment briefly on each step.

---

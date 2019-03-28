---

name: oversharing
# Oversharing

```java
Applet applet = new Applet();
Vector names = new Vector();
names.add("Harry Potter");
applet.setAccessControlList(names);
names.add("Voldemort");
```

---

template: oversharing

.line4[
![Point at call to `setAccessControlList`](content/images/Arrow.png)
]

- `setAccessControlList` also checked that the list is reasonable

---

template: oversharing

.line5[
![Point at call to `setAccessControlList`](content/images/Arrow.png)
]


- `setAccessControlList` also checked that the list is reasonable
- Uh oh!


---

name: entry

# Example: the entry API

```rust
my_map
  .entry(some_key)
  .or_insert(Vec::new())
  .push(element);
```

---

template: entry

.line1[
![Arrow](content/images/Arrow.png)
]

- Given a hashmap `K -> Vec<V>`,

---

template: entry

.line2[
![Arrow](content/images/Arrow.png)
]

- Given a hashmap `K -> Vec<V>`,
  - lookup the value for the key `K` (if any)

---

template: entry

.line3[
![Arrow](content/images/Arrow.png)
]

- Given a hashmap `K -> Vec<V>`,
  - lookup the value for the key `K` (if any),
  - insert an empty vector for `K` if nothing exists,

---

template: entry

.vec-new[
![Arrow](content/images/Arrow.png)
]

- Given a hashmap `K -> Vec<V>`,
  - lookup the value for the key `K` (if any),
  - insert an empty vector for `K` if nothing exists,

---

template: entry

.line4[
![Arrow](content/images/Arrow.png)
]

- Given a hashmap `K -> Vec<V>`,
  - lookup the value for the key `K` (if any),
  - insert an empty vector for `K` if nothing exists,
  - push `element` onto the vector for `K`.

---

template: entry

- Given a hashmap `K -> Vec<V>`,
  - lookup the value for the key `K` (if any),
  - insert an empty vector for `K` if nothing exists,
  - push `element` onto the vector for `K`.
- **Ergonomic, yes.** But also:
  - **Efficient:** reuse hash, internal indices from first lookup.
  - **Robust:** `entry` borrows the map, so you can't intermix multiple insertions.


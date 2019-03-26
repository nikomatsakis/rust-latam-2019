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


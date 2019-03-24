class: center
name: title
count: false

<img src="content/images/rust-logo-blk.svg" alt="Rust logo" width="250rem" height="auto">

# What's *unique* about Rust?

.grey[Nicholas Matsakis]

---

# I’ve been working on Rust since 2011…

When I started:
- repo was `https://github.com/graydon/rust`
- it warned that Rust might eat your laundry

---

# I’ve been working on Rust since 2011…

When I started:
- repo was `https://github.com/graydon/rust`
- it warned that Rust might eat your laundry
- my daughter was a few months old

---

background-image: url(content/images/DaphneDino.jpg)
background-size: contain

---

# I’ve been working on Rust since 2011…

Rust syntax was...different:

```
tag t<@T> { none; some(T); }
```

<!--
citation
https://github.com/rust-lang/rust/blob/142f63fe785ce8f2e5d9cc8edc6a0eaf1c21e46b/src/lib/option.rs#L3
-->

--

For those who know Rust, today that would look like:

```rust
enum Option<T> {
  None,
  Some(T),
}
```
---

# A few things have changed…

<img src="content/images/total-crates-over-time.svg" alt="Total crates over time" width="1000rem" height="auto">

---

# People are using Rust in production

--

.center[<img src="content/images/what.gif" alt="What." width="100%" height="auto">]

???

Actually, the first Rust production user was Tilde, way before 1.0.
Too which my reaction was roughly...actually, it's quite interesting.
Tilde putting Rust into production is what brought Yehuda Katz into
Rust, and I think that when he saw some of the things in the language
at the time, this "What?" was roughly his reaction as well. He
agitated for a lot of changes.  Some of them we did
immediately. Others we did as part of Rust 2018. Some we may never do.

---

# People are using Rust in production

- Tilde
- Mozilla (stylo, soon WebRender)
- Dropbox (storage system)
- Facebook (Mercurial rewrite)
- Google (Fuschia operating system)
- Amazon (Firecracker)
- Microsoft (Azure)
- ...

---

# People are using Rust in production

.center[<img src="content/images/kermit.gif" alt="Kermit happy!" width="100%" height="auto">]

---

# More importantly, people *like* Rust

<img src="content/images/stack-overflow.png"
     alt="Stackoverflow survey results from 2018"
     width="auto"
     height="auto">

---

# More importantly, people *like* Rust
.center[<img src="content/images/kermit.gif" alt="Kermit happy!" width="100%" height="auto">]

---

# What are people excited about?

---

# Hype?

.center[<img src="content/images/macarena.gif" alt="I'm 'hip'" width="100%" height="auto">]


---

# Domain?

Is it... &#10024; **systems programming** &#10024;?

--

"Programming where **resources are limited**" <br>
&mdash; Bjarne Stroustroup, paraphrased, Lang.NEXT 2014

--

.center[<img src="content/images/Lang.Next.jpg" alt="Lang.Next panel" width="auto" height="100%">]

---

.center[<img src="content/images/kermit.gif" alt="Kermit happy!" width="100%" height="auto">]

---

# Qualities Rust shares with C(++)

- Low-level control, highly optimizable:
  - inline memory layout
  - static dispatch
  - no garbage collector or other runtime
- Anywhere you use C, you can use Rust: 
  - Want to write a plugin for Python or Ruby? You can do it in Rust.
  - Want to write a **kernel**? You can do it in Rust.

---

# Safety?

|                       | C++ |
| --------------------- | --- |
| Control, flexibility  | 🎉  |
| Minimal to no runtime | 🎉  |
| Double free           | 😢  |
| Use after free        | 😢  |
| Null pointer          | 😢  |
| Data race             | 😢  |

---

# Safety?

|                       | C++ | GC    |
| --------------------- | --- | ----- |
| Control, flexibility  | 🎉  | 🤷‍♀️ |
| Minimal to no runtime | 🎉  | 🤷‍♀️ |
| Double free           | 😢  | 🎉    |
| Use after free        | 😢  | 🎉    |
| Null pointer          | 😢  | 😢    |
| Data race             | 😢  | 😢    |

---

# Safety?

|                       | C++ | GC    | Rust |
| --------------------- | --- | ----- | ---- |
| Control, flexibility  | 🎉  | 🤷‍♀️ | 😎   |
| Minimal to no runtime | 🎉  | 🤷‍♀️ | 😎   |
| Double free           | 😢  | 🎉    | 😎   |
| Use after free        | 😢  | 🎉    | 😎   |
| Null pointer          | 😢  | 😢    | 😎   |
| Data race             | 😢  | 😢    | 😎   |

---

# How do we do that?

Using a **type system**.

---

# Type system can be a hard sell

---

# Type system as superpower

---

# What makes the difference?

Rust type system is more than structs with fields and methods.

---

# Enums

```rust
enum Shape {
  Circle { radius: u32 },
  Square { width: u32, height: u32 },
}
```

(Borrowed from functional languages like Haskell and Ocaml)

---

# Matching

```rust
let area = match shape {
  Shape::Circle { radius } =>
    radius * radius * PI,

  Shape::Square { width, height } =>
    width * height,
};
```

---

# Matching

```rust
let area = match shape {
  Shape::Circle { `radius` } =>
    `radius` * `radius` * PI,

  Shape::Square { width, height } =>
    width * height,
};
```

---

# No more null pointers

```rust
enum Option<T> {
  Some(T),
  None,
}
```

---

# No more null pointers

```rust
// A "nullable string"
let optional_string: Option<String>;

match optional_string {
  None => {
    // String is null -- do something.
  }

  Some(s) => {
    // String is not null, use 's'.
  }
}
```

---

# Ownership and borrowing

<!-- FIXME -->

---

# Every language lets you give

```js
*let manzana = new Apple();
eat(manzana);
manzana.setKind(GOLDEN_DELICIOUS);

function eat(manzana) {
  ...
}
```

--

<img src="content/images/Apple1.svg"
     alt="object diagram">

---

# Every language lets you give

```js
let manzana = new Apple();
*eat(manzana);
manzana.setKind(GOLDEN_DELICIOUS);

function eat(manzana) {
  ...
}
```

--

<img src="content/images/Apple2.svg"
     alt="object diagram">

---

# Every language lets you give

```js
let manzana = new Apple();
eat(manzana);
*manzana.setKind(GOLDEN_DELICIOUS);

function eat(manzana) { ... }
```

<img src="content/images/Apple3.svg"
     alt="object diagram">

--

"Neither golden, nor delicious." <br>
&mdash; My daughter, in one of my prouder parenting moments

---

# Rust lets you take away

```rust
*fn main() {
  let mut manzana = Apple::new();
  eat(manzana);
  manzana.set_kind(AppleKind::GoldenDelicious);
}

fn eat(manzana: Apple) { ... }
```

---

# Rust lets you take away

```rust
fn main() {
* let mut manzana = Apple::new();
  eat(manzana);
  manzana.set_kind(AppleKind::GoldenDelicious);
}

fn eat(manzana: Apple) { ... }
```

---

# Rust lets you take away

```rust
fn main() {
  let mut manzana = Apple::new();
  eat(manzana);
  manzana.set_kind(AppleKind::GoldenDelicious);
}

fn eat(manzana: Apple) { ... }
```

---

# Rust lets you take away

```rust
fn main() {
  let mut manzana = Apple::new();
  eat(manzana);
  manzana.set_kind(AppleKind::GoldenDelicious);
}

*fn eat(manzana: Apple) { ... }
```

---

# Rust lets you take away

```rust
fn main() {
  let mut manzana = Apple::new();
  eat(manzana);
  manzana.set_kind(AppleKind::GoldenDelicious);
}

fn eat(`manzana: Apple`) { ... }
```

---

# Rust lets you take away

```rust
fn main() {
  let mut manzana = Apple::new();
  eat(manzana);
* manzana.set_kind(AppleKind::GoldenDelicious);
}

fn eat(manzana: Apple) { ... }
```

--

```
error[E0382]: borrow of moved value: 'manzana'
     |
  16 |    eat(manzana);
     |        ------- `value moved here`
  17 |    manzana.set_kind(AppleKind::GoldenDelicious);
     |    ^^^^^^^ `value borrowed here after move`
     |
     = note: move occurs because 'manzana' has type 'Apple',
       which does not implement the 'Copy' trait
```

<!--

https://play.rust-lang.org/?version=stable&mode=debug&edition=2018&gist=a65d19a6acd754ee606ad9471405109d

-->

---

# Channels in Go

```go
func foo() {
  m := make(map[string]string)
  m["Hello"] = "World"

* // Once I send, I'm not supposed to go on using "m"...
* channel <- m

  // ...but nothing stops me
  m["Hello"] = "Data Race"
}
```

---

# Channels in Go

```go
func foo() {
  m := make(map[string]string)
  m["Hello"] = "World"

  // Once I send, I'm not supposed to go on using "m"...
  channel <- m

* // ...but nothing stops me
* m["Hello"] = "Data Race"
}
```

---

# What happens in Rust?

```rust
fn main() {                         impl<T> Channel<T> {           
  let m = HashMap::new();             fn send(&mut self, data: T) {
  m.insert("Hello", "World");           ...                        
  channel.send(m);                    }                            
  m.insert("Hello", "Data Race");   }                              
}                                   
```

---

# What happens in Rust?

```rust
fn main() {                         `impl<T> Channel<T> {`           
  let m = HashMap::new();             fn send(&mut self, data: T) {
  m.insert("Hello", "World");           ...                        
  channel.send(m);                    }                            
  m.insert("Hello", "Data Race");   }                              
}                                   
```

---

# What happens in Rust?

```rust
fn main() {                         impl<T> Channel<T> {           
  let m = HashMap::new();             fn send(&mut self, `data: T`) {
  m.insert("Hello", "World");           ...                        
  channel.send(m);                    }                            
  m.insert("Hello", "Data Race");   }                              
}                                   
```

--

When you send data, the channel **takes ownership** of the data.

---

# What happens in Rust?

```rust
fn main() {                         impl<T> Channel<T> {           
  let m = HashMap::new();             fn send(&mut self, data: T) {
  m.insert("Hello", "World");           ...                        
  `channel.send(m);`                    }                            
  m.insert("Hello", "Data Race");   }                              
}                                   
```

When you send data, the channel **takes ownership** of the data.

--

That means the caller is **giving ownership away**.

---

# What happens in Rust?

```rust
fn main() {                         impl<T> Channel<T> {           
  let m = HashMap::new();             fn send(&mut self, data: T) {
  m.insert("Hello", "World");           ...                        
  channel.send(m);                    }                            
  `m.insert("Hello", "Data Race");`   }                              
}                                   
```

When you send data, the channel **takes ownership** of the data.

That means the caller is **giving ownership away**.

--

So we get a **compilation error** when we try to use it later.

---

# What just happened?

- In Go, we had a **dynamic error**
- In Rust, the program **did not compile**

???

This is a big deal, especially when you are working
with systems programs. The usual way of learning C++ was
to write your code, have it crash a few dozen times until
you finally grokked the unwritten rules, and then let it run,
then realize 

Tell story about me finally understanding what memory leaks are?

Mention that the way I sell Rust to c++ programmers *now* is just to
tell them that I don't remember the last time I debugged a crash.

---

# Parallel APIs without ownership/borrowing

.center[
![cast spell, burn self](content/images/firespell.gif)
]

---

# Rust lets you guide users

.center[
<img src="content/images/spiderman-whee.gif"
     alt="with great power comes great... weeeeee!">
]

---

# So what is unique about Rust?

- Zero-cost abstractions from C++
- Modern conveniences
- Sense of **artisanship**

---

# Beyond the code

???

Thus far in this talk I’ve focused on the design of Rust itself. But any real answer to the question of “what makes Rust unique” has to look past that.

---

# Rust is open
- Open-**source**
  - by now, thousands of contributors
- Open-**governance**
  - owned by the people who built it, not any one company
- Open-**minded**
  - focused on finding the best answer, not on winning the argument

---

# Beyond tradeoffs

Easy to conclude there is an **essential tradeoff**.
  
--

But often there is a **hidden assumption**.

---

# Rust has evolved

- When I started on Rust in 2011, it had:
  - a runtime with built-in threads
  - a lot of concepts and a lot of unusual syntax
    - (`++x: ~option::t<string::t>`)
  - a **garbage collector 😱** 
  
---

# The more things change...

- Some things have not changed:
  - systems programming
  - safety
  - a CoC and a culture that emphasized **curiosity and deep research**

---

# Rust is not the result of any one person

Great ideas in the development of Rust:

- adopting unique types (“ownership”) and references (“borrowing”)
- adopting the trait system (“typeclasses”)
- removing the runtime and garbage collector
- adopting cargo
- introducing the `Poll` trait (well, time will tell, but I think so)

--

Each introduced by different people.

--

Each seems obvious now.

--

None were obvious at the time.

---

# Beyond the language

It takes more than

---

class: center
name: title
count: false

<img src="content/images/rust-logo-blk.svg" alt="Rust logo" width="250rem" height="auto">

# Thanks

.grey[Twitter/Github: spastorino]<br/>
.grey[Email: spastorino@gmail.com]

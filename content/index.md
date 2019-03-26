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

.center[
![wycats loves Rust in 2013](content/images/tweet-wycats-loves-rust.png)
]

---

# People are using Rust in production

.center[<img src="content/images/what.gif" alt="What." width="100%" height="auto">]

???

Actually, the first Rust production user was Tilde, way before 1.0.
Too which my reaction was roughly...actually, it's quite interesting.
Tilde putting Rust into production is what brought Yehuda Katz into
Rust -- definitely a mutually beneficial relationship.

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

.peoplelike-tl[
![johncarmarck tweets about Rust](content/images/tweet-johncarmack.png)
]

.peoplelike-bl[
![ianmbuckley tweets about Rust](content/images/tweet-ianmbuckley.png)
]

.peoplelike-br[
![Bodil tweets that Rust is a game changer](content/images/tweet-Bodil-game-changer.png)
]

.peoplelike-hearts[
![hearts](content/images/Lovers-Hearts.png)
]

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

.center[<img src="content/images/puzzle.png" alt="The puzzle" width="100%" height="auto">]

---

# Hype?

.center[<img src="content/images/macarena.gif" alt="I'm 'hip'" width="100%" height="auto">]


---

# Domain?

Is it... &#10024; **systems programming** &#10024;?

--

"Programming where **resources are limited**" <br>
&mdash; Bjarne Stroustroup, paraphrased, Lang.NEXT 2014

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

name: puzzle

.center[<img src="content/images/puzzle.png" alt="The puzzle" width="100%" height="auto">]

---

template: puzzle

.zca[Zero-cost abstractions]

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

# Type system can be a hard sell

.center[
.forty[
![Dog eating spinach](content/images/spinach-dog.jpg)
]
]

.citation[
Photo credit: Sanjoy Ghosh<br>
`https://www.flickr.com/photos/sanjoy/4016632253/`
]

---

background-image: url(content/images/popeye.jpg)
background-size: contain

.white-text[
# Type system as a superpower
]

.white-text[.citation[
Photo credit: Salim Virji<br>
`https://www.flickr.com/photos/salim/8594532469/`
]]

---

# What makes the difference?

Rust type system is more than structs with fields and methods.

--

Strong support for generic programming.

Closures.

Enums.

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
let area = `match shape` {
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
* Shape::Circle { radius } =>
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

# Matching

```rust
let area = match shape {
  Shape::Circle { radius } =>
    radius * radius * PI,

* Shape::Square { width, height } =>
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
enum Option<T> {
* Some(T),
  None,
}
```
---

# No more null pointers

```rust
enum Option<T> {
  Some(T),
* None,
}
```

---

# No more null pointers

```rust
enum Option<T> {
  Some(T),
  None,
}
```

```rust
// A "nullable string"
let optional_string: Option<String> = None;
```

---

# No more null pointers

```rust
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

template: puzzle

.zca[Zero-cost abstractions]

--

.modern-conveniences[Modern conveniences]

---

# Modern conveniences is more than lang

.center[![crates.io screenshot](content/images/crates-io.png)]

---

template: puzzle

.zca[Zero-cost abstractions]

.modern-conveniences[Modern conveniences]

--

.ownership-and-borrowing[Ownership and Borrowing]

---

background-image: url(content/images/ownership-and-borrowing.png)
background-size: contain

.white-text[
# Ownership and borrowing
]

.white-text[
.citation[
Photo Credit: Nathan Kam<br>
`https://www.youtube.com/watch?v=Tnssn9KcWLg`
]
]

---

name: every-language-lets-you-give

# Every language lets you give

```js
let manzana = new Apple();
eat(manzana);
manzana.setKind(GOLDEN_DELICIOUS);

function eat(manzana) {
  ... GLOBAL = manzana ...
}
```

.jslogo[
<img src="content/images/js-logo.svg" alt="JS logo" >
]


---

template: every-language-lets-you-give

.line1[
![Arrow](content/images/Arrow.png)
]

<img src="content/images/Apple1.svg"
     alt="object diagram">

---

template: every-language-lets-you-give

.line2[
![Arrow](content/images/Arrow.png)
]

<img src="content/images/Apple2.svg"
     alt="object diagram">

---

template: every-language-lets-you-give

.line3[
![Arrow](content/images/Arrow.png)
]

<img src="content/images/Apple3.svg"
     alt="object diagram">

--

"Neither golden, nor delicious." <br>
&mdash; My daughter, in one of my prouder parenting moments

---

name: rust-lets-you-take-away

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

template: rust-lets-you-take-away

.line1[
.fourty[![Highlight the fn main](content/images/Arrow.png)]
]

---

template: rust-lets-you-take-away

.line2[
.fourty[![Highlight the let mut](content/images/Arrow.png)]
]

---

template: rust-lets-you-take-away

.line3[
.fourty[![Highlight the call to eat](content/images/Arrow.png)]
]

---

template: rust-lets-you-take-away

.line7[
.fourty[![Highlight the eat fn](content/images/Arrow.png)]
]


---

template: rust-lets-you-take-away

.manzana-arrow[
.fourty[![Highlight the eat fn](content/images/Arrow.png)]
]

---

template: rust-lets-you-take-away

.line4[
![Highlight the `set_kind` call](content/images/Arrow.png)
]

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
* m := make(map[string]string)
* m["Hello"] = "World"

  // Once I send, I'm not supposed to go on using "m"...
  channel <- m

  // ...but nothing stops me
  m["Hello"] = "Data Race"
}
```

.gologo[
<img src="content/images/Go-Logo_Black.svg" alt="Go logo" width="50px" height="50px">
]

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

.gologo[
<img src="content/images/Go-Logo_Black.svg" alt="Go logo" width="50px" height="50px">
]

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

.gologo[
<img src="content/images/Go-Logo_Black.svg" alt="Go logo">
]

---

# What happens in Rust?

```rust
fn main() {
* let m = HashMap::new();
* m.insert("Hello", "World");
  channel.send(m);
  m.insert("Hello", "Data Race");
}
```

---

# What happens in Rust?

```rust
fn main() {
  let m = HashMap::new();
  m.insert("Hello", "World");
* channel.send(m);
  m.insert("Hello", "Data Race");
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

# A pattern

- Easy to **expose** a high-performance API
- Hard to **help users control it**

.center[
![cast spell, burn self](content/images/firespell.gif)
]

???

This is a big deal, especially when you are working
with systems programs. The usual way of learning C++ was
to write your code, have it crash a few dozen times until
you finally grokked the unwritten rules, and then let it run,
then realize 

Tell story about me finally understanding what memory leaks are?

Mention that the way I sell Rust to c++ programmers *now* is just to
vtell them that I don't remember the last time I debugged a crash.

---

template: puzzle

.zca[Zero-cost abstractions]

.modern-conveniences[Modern conveniences]

.ownership-and-borrowing[Ownership and Borrowing]

--

.craftsmanship[Sense of **craftsmanship**]

---

.page-center[
<img src="content/images/spiderman-whee.gif"
     alt="with great power comes great... weeeeee!">
]

---

# Best in class

.page-center[
![Tweet asking for libs](content/images/tweet-libs-call.png)
]

---

# Best in class

.top-left[
![Tweet asking for libs](content/images/tweet-libs-1.png)
]

.top-right[
![Tweet asking for libs](content/images/tweet-libs-rayon.png)
]

.bottom-left[
![Tweet asking for libs](content/images/tweet-libs-serde.png)
]

.bottom-right[
![Tweet asking for libs](content/images/tweet-libs-clap.png)
]

---

# Best in class

.top-left[
![Tweet asking for libs](content/images/tweet-libs-5.png)
]

.top-right[
![Tweet asking for libs](content/images/tweet-libs-specs.png)
]

.bottom-left[
![Tweet asking for libs](content/images/tweet-libs-curve25519.png)
]

.bottom-right[
![Tweet asking for libs](content/images/tweet-libs-2.png)
]

---

# Example from the standard library


---

template: puzzle

.zca[Zero-cost abstractions]

.modern-conveniences[Modern conveniences]

.ownership-and-borrowing[Ownership and Borrowing]

.craftsmanship[Sense of **craftsmanship**]

--

.community[**Community**]

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
  - uncompromised efficiency
  - safety and correctness
  - a CoC and a culture that emphasized **curiosity and deep research**

---

# Rust is not the result of any one person

Great ideas in the development of Rust:

- adopting the borrow checker (ownership and borrowing)
- adopting the trait system
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

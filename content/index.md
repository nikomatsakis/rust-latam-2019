class: center
name: title
count: false

# What's **unique** about Rust?

.me[.grey[*by* **Nicholas Matsakis**]]
.page-center[.eighty[![Rust Logo](content/images/rust-logo-512x512.png)]]
.king[![Drawing of King](content/images/King.png)]
.queen[![Drawing of Queen](content/images/Queen.png)]

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

--

.wycatsdate[
![Arrow](content/images/Arrow.png)
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

```go
func foo() {
  regalo := Gift { .. }
  channel <- regalo
  regalo.open();
}
```

.gologo[
<img src="content/images/Go-Logo_Black.svg" alt="Go logo" width="50px" height="50px">
]

---

template: every-language-lets-you-give

.lover-left[
![Person on the left](content/images/Lovers-Girl.png)
]

.line1[
![Point at `func foo`](content/images/Arrow.png)
]

---

template: every-language-lets-you-give

.lover-left[
![Person on the left](content/images/Lovers-Girl.png)
]

.line2[
![Point at `Gift { }`](content/images/Arrow.png)
]

--

.lover-gift-left[
![Gift](content/images/Gift.png)
]

---

template: every-language-lets-you-give

.lover-left[
![Person on the left](content/images/Lovers-Girl.png)
]

.line3[
![Point at `channel <- regalo`](content/images/Arrow.png)
]

.lover-gift-left[
![Gift](content/images/Gift.png)
]

--

.lover-right[
![Person on the right](content/images/Lovers-Boy.png)
]

---

template: every-language-lets-you-give

.lover-left[
![Person on the left](content/images/Lovers-Girl.png)
]

.line3[
![Point at `channel <- regalo`](content/images/Arrow.png)
]

.lover-gift-center[
![Gift](content/images/Gift.png)
]

.lover-right[
![Person on the right](content/images/Lovers-Boy.png)
]

---

template: every-language-lets-you-give

.lover-left[
![Person on the left](content/images/Lovers-Girl.png)
]

.lover-right[
![Person on the left](content/images/Lovers-Boy.png)
]

.lover-gift-center[
![Gift](content/images/Gift.png)
]

.line4[
![Point at `regalo.open`](content/images/Arrow.png)
]

--

.lover-gift-center[
![Gift](content/images/Blueberry-Labeled.png)
]

---

template: every-language-lets-you-give

.lover-left[
![Person on the left](content/images/Lovers-Girl.png)
]

.lover-right[
![Person on the left](content/images/Lovers-Boy.png)
]

.lover-gift-center[
![Gift](content/images/Blueberry-Labeled.png)
]

.col-right[
```go
// The other goroutine
presente := <- channel
presente.open()
```
]

.line3r[
![Point at `regalo.open`](content/images/Arrow.png)
]

.lover-right[
![Person on the right](content/images/Lovers-Boy.png)
]

--

.lover-right[
![Person on the right](content/images/Lovers-Boy-Sad.png)
]

---

# What went wrong?

.lover-right[
![Person on the right](content/images/Lovers-Boy-Sad.png)
]

Two ingredients:

- Mutation
- Sharing

--

Rust's solution:

- Support sharing and mutation
  - but **not at the same time**

---

name: rust-lets-you-take-away

# Rust lets you take away

```rust
fn main() {
  let regalo = Gift::new();
  channel.send(regalo);
  regalo.open();
}
```

---

template: rust-lets-you-take-away

.line1[![Highlight `fn main`](content/images/Arrow.png)]

.lover-left[![Person on the left](content/images/Lovers-Girl.png)]

---

template: rust-lets-you-take-away

.line2[![Highlight `let regalo`](content/images/Arrow.png)]

.lover-left[![Person on the left](content/images/Lovers-Girl.png)]

.lover-gift-left[![Gift](content/images/Gift.png)]

---

template: rust-lets-you-take-away

.line3[
.fourty[![Highlight the call to eat](content/images/Arrow.png)]
]

.lover-left[
![Person on the left](content/images/Lovers-Girl.png)
]

.lover-gift-left[
![Gift](content/images/Gift.png)
]

---

name: rust-lets-you-take-away-2
template: rust-lets-you-take-away

.col-right[
```rust
impl<T> Channel<T> {
  fn send(&mut self, data: T) {
    ...
  }
}
```
]

---

template: rust-lets-you-take-away-2

.line1r[![Highlight the eat fn](content/images/Arrow.png)]
.lover-gift-left[![Gift](content/images/Gift.png)]
.lover-left[![Person on the left](content/images/Lovers-Girl.png)]
.lover-right[![Person on the right](content/images/Lovers-Boy.png)]

---

template: rust-lets-you-take-away-2

.line1-impl[![Highlight `impl`](content/images/Arrow.png)]
.lover-gift-left[![Gift](content/images/Gift.png)]
.lover-left[![Person on the left](content/images/Lovers-Girl.png)]
.lover-right[![Person on the right](content/images/Lovers-Boy.png)]

---

template: rust-lets-you-take-away-2

.line1-generics[![Highlight `<T>`](content/images/Arrow.png)]
.lover-gift-left[![Gift](content/images/Gift.png)]
.lover-left[![Person on the left](content/images/Lovers-Girl.png)]
.lover-right[![Person on the right](content/images/Lovers-Boy.png)]

---

template: rust-lets-you-take-away-2

.line2-data[![Highlight `data: T`](content/images/Arrow.png)]
.lover-gift-left[![Gift](content/images/Gift.png)]
.lover-left[![Person on the left](content/images/Lovers-Girl.png)]
.lover-right[![Person on the right](content/images/Lovers-Boy.png)]

---

template: rust-lets-you-take-away-2

.line2-data[![Highlight `data: T`](content/images/Arrow.png)]
.lover-gift-right[![Gift](content/images/Gift.png)]
.lover-left[![Person on the left](content/images/Lovers-Girl.png)]
.lover-right[![Person on the right](content/images/Lovers-Boy.png)]

---

template: rust-lets-you-take-away

.line4[![Highlight `regalo.open`](content/images/Arrow.png)]
.lover-left[![Person on the left](content/images/Lovers-Girl.png)]

---

template: rust-lets-you-take-away

.line4[![Highlight `regalo.open`](content/images/Arrow.png)]

```
error[E0382]: use of moved value: 'regalo'
  --> src/main.rs:13:4
     |
  12 |    channel.send(regalo)
     |                 ------ `value moved here`
  13 |    regalo.open();
     |    ^^^^^^ `value used here after move`
```

<!--

https://play.rust-lang.org/?version=stable&mode=debug&edition=2018&gist=4a87aac56936416fa95efa811266ce88

-->

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

name: seq-iter

# Sequential iterators

```rust
fn load_images(paths: &[PathBuf]) -> Vec<Image> {
  paths
    .iter()
    .map(|path| Image::load(path))
    .collect()
}
```

---

template: seq-iter

.line1[![Point at `paths`](content/images/Arrow.png)]

---

template: seq-iter

.line3[![Point at `iter`](content/images/Arrow.png)]

- Create an iterator over paths

---

template: seq-iter

.line4[![Point at `iter`](content/images/Arrow.png)]

- Create an iterator over paths
- For each path, invoke `Image::load`

---

template: seq-iter

.line5[![Point at `iter`](content/images/Arrow.png)]

- Create an iterator over paths
- For each path, invoke `Image::load`
- Collect loaded images into a vector

---

name: rayon

# Parallel iterators

```rust
fn load_images(paths: &[PathBuf]) -> Vec<Image> {
  paths
    .par_iter()
    .map(|path| Image::load(path))
    .collect()
}
```

.line3[![Point at `par_iter`](content/images/Arrow.png)]

- One change to execute in parallel

---

name: rayon-race

# Parallel iterators

```rust
fn load_images(paths: &[PathBuf]) -> Vec<Image> {
  let mut jpegs = 0;
  paths
    .par_iter()
    .map(|path| {
      if path.ends_with(".jpg") {
        jpegs += 1;
      }
      Image::load(path)
    })
    .collect()
}
```

---

template: rayon-race

.line2[![Point at `jpegs`'](content/images/Arrow.png)]

---

template: rayon-race

.line7b[![Point at `jpegs`'](content/images/Arrow.png)]

---

.center[![saved by the compiler](content/images/saved-by-compiler.png)]

> **The Rust compiler just saved me from a nasty threading bug.** I was working on cage (our open source development tool for Docker apps with lots of microservices), and I decided to parallelize the routine that transformed docker-compose.yml files. This was mostly an excuse to check out the awesome rayon library, but it turned into a great example of what real-world Rust development is like.

.citation[`https://blog.faraday.io/saved-by-the-compiler-parallelizing-a-loop-with-rust-and-rayon/`]
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

.citation[`https://twitter.com/nikomatsakis/status/1110166084496310272`]

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
![Tweet asking for libs](content/images/tweet-libs-7.png)
]

---

# Best in class

.page-center[
![Tweet about diesel](content/images/tweet-libs-diesel.jpg)
]

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

name: morethingschange

# The more things change...

- When I started on Rust in 2011, it had:
  - no borrow-checker
  - a lot of concepts and a lot of unusual syntax
    - (`++x: ~option::t<string::t>`)
  - a runtime with built-in threads
  - a **garbage collector 😱** (and not a good one)
{{content}}

---

template: morethingschange

- Some things have not changed:
  - uncompromised efficiency
  - safety and correctness
  - a CoC and a culture that emphasizes **curiosity and deep research**

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

.page-center[
> .jlord[The value of common knowledge cannot be overestimated. We must to do better. **We need all the ideas from all the people.** That's what we should be aiming for.] <br>
> <br>
> &mdash; Jessica Lord, "Privilege, Community and Open Source"
]

.citation[`http://jlord.us/blog/osos-talk.html`]

---

# Rust is not (just) the result of coders

> .jlord[We need an open source for **designers** (who make documentation easier to read and give an identity to a project), **journalists and scientists** (who share their data), **polyglots** (who make projects accessible to not just those who speak English), **note takers and editors** (who can make resources and documentation better), **organizers** (who can triage the many issues created in open source projects), **mappers and data wranglers** and ...] <br>
> <br>
> &mdash; Jessica Lord (emphasis mine)

.citation[`http://jlord.us/blog/osos-talk.html`]

---

# Speaking of which...

.page-center[
![Please clap!](content/images/please-clap.png)
]

<!--
https://twitter.com/ag_dubs/status/1053726412207722502
-->

---

# What's next for Rust?

Step 1: Recognize what we've done

--

Step 2: Recognize how much further we have to go

---

# Organizing for the long haul

---

# Thanks for listening

![Prince and princess](content/images/Prince-and-princess.png)

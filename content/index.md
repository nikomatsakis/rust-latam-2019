class: center
name: title
count: false

# What's **unique** about Rust?

.me[.grey[*by* **Nicholas Matsakis**]]
.page-center[.p80[![Rust Logo](content/images/rust-logo-512x512.png)]]
.king[![Drawing of King](content/images/King.png)]
.queen[![Drawing of Queen](content/images/Queen.png)]
.citation[`https://github.com/nikomatsakis/rust-latam-2019`]

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

--

.one-dot-oh[![Arrow](content/images/Arrow.png)]

---

# People are using Rust in production

--

.center[![wycats loves Rust in 2013](content/images/tweet-wycats-loves-rust.png)]

--

.wycatsdate[![Arrow](content/images/Arrow.png)]

---

# People are using Rust in production

.center[<img src="content/images/what.gif" alt="What." width="100%" height="auto">]

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

.center[.p60[![Wiley running fast](content/images/wiley-running.gif)]]

---

name: puzzle

.center[<img src="content/images/puzzle.png" alt="The puzzle" width="100%" height="auto">]

---

template: puzzle

.zca[Zero-cost abstractions]

---

# Qualities Rust shares with C(++)

- **Zero-cost abstractions:**
  - inline memory layout
  - static dispatch
  - no garbage collector or other runtime
- Anywhere you use C, you can use Rust:
  - Want to write a plugin for Python or Ruby? You can do it in Rust.
  - Want to write a **kernel**? You can do it in Rust.

---

# Why not just use C++ then?

--

.center[.p60[![Wiley E Coyote on an exploding rocket](content/images/wiley-exploding-rocket.gif)]]

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
.p40[
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

# Parallel CSS Styling

.center[![Bug 631527](content/images/bug-631527.png)]

--

.bugzilla-arrow[![Arrow](content/images/Arrow.png)]

--

.center[.bugzilla1[Reported:] .bugzilla2[8 years ago]]

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

# Ownership and borrowing

.center[.p80[![Office space stapler](content/images/office-space.gif)]]

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

.line3[![Highlight the call to eat](content/images/Arrow.png)]

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

--

.line3-regalo[![Highlight `regalo`](content/images/Arrow.png)]

---

template: rust-lets-you-take-away-2

.line2-data[![Highlight `data: T`](content/images/Arrow.png)]
.line3-regalo[![Highlight `regalo`](content/images/Arrow.png)]
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

# What just happened?

--

.center[.p80[![Wiley E Coyote falls](content/images/wiley-batman-fall.gif)]]

---

# A pattern

- Easy to **expose** a high-performance API
- Hard to **help users control it**

.center[
![cast spell, burn self](content/images/firespell.gif)
]

---

# This could be you

.center[.p80[![Wiley E Coyote flies](content/images/wiley-flies.gif)]]

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

.center[.p80[
![Tweet asking for libs](content/images/tweet-libs-call.png)
]]

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

.center[.p80[
![Tweet about diesel](content/images/tweet-libs-diesel.jpg)
]]

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
  
???

Rust has always been open, in a lot of different ways.  But I think
the most important for us has been the last one: open-minded. Or, as
the slide says, focused on finding the **best answer** -- and not on
winning the argument.

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

???

When we started, we didn't really know what Rust should look like.
The Rust of 2011, from a technical perspective, was not the Rust of
today.  It had some but not all of the building blocks of zero-cost
abstractions in place -- and, fundamentally, it was not a
"library-based language" like Rust is today. Instead, it had a lot of
things built in to the language. It had a garbage collector! And yet
certain key things were present, even then.

---

# ...the more they stay the same

- When I started on Rust in 2011, it had a commitment to:
  - uncompromised efficiency
  - safety and correctness
  - a CoC and a culture that emphasizes **curiosity and deep research**

???

In particular, we had the right goals:

- it had to be fast enough to truly replace C++
- while still being safe.

and we knew that we didn't know how to do that yet. Which is where the
commitment to curiosity and research comes from -- those are what
allowed us to evolve our way from the language we had then to the one
that I just presented to you.

---

# Rust is not the result of any one person

(Some) great ideas in the development of Rust:

- adopting the borrow checker (ownership and borrowing)
- adopting the trait system
- removing the runtime and garbage collector
- adopting cargo
- introducing the `Poll` trait (well, time will tell, but I think so)

???

There is no way we would have gotten here without an open
process. Here is a very incomplete list of great ideas that were
crucial.

--

Each introduced by different people.

--

Each seems obvious now.

--

None were obvious at the time.

???

In fact, they were often pretty controversial.

---

.page-center[
> .jlord[The value of common knowledge cannot be overestimated. We must to do better. **We need all the ideas from all the people.** That's what we should be aiming for.] <br>
> <br>
> &mdash; Jessica Lord, "Privilege, Community and Open Source"
]

.citation[`http://jlord.us/blog/osos-talk.html`]

???

While doing research for this talk, I came across this excellent blog
post by Jessica Lord. You should read it, if you haven't already. But
she put it really well: if you want to solve the hardest problems, you
need all the ideas, from all of the people. You can't afford to shut
people out.


---

# In case you haven't noticed...

--

...we're doing the impossible here, people!

.center[.p50[![Bowl balancing act](content/images/bowl-balance.gif)]]

???

- Rust is trying to "have our cake and eat it too"
- we did it only by having all the ideas, from all the people

---

name: not-just-coders

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

.center[.p80[![Scylla and Charybdis](content/images/GillrayBritannia.jpg)]]

.citation[https://en.wikipedia.org/wiki/File:GillrayBritannia.jpg]

???

- What about design by committee?
- But you must also steer clear of simple tradeoffs.
- Have to also discuss the vision, keep the conversation focused on
  that at the same time.
- Finding the best ways to steer between these two dangers is one of
  the core challenges.

---

template: puzzle

.zca[Zero-cost abstractions]

.modern-conveniences[Modern conveniences]

.ownership-and-borrowing[Ownership and Borrowing]

.craftsmanship[Sense of **craftsmanship**]

.community[**Community**]

---

# Looking to the future

.center[.p60[![Future robot](content/images/future-robot.gif)]]

--

.center[(The robot is written in Rust, naturally.)]

--

.center[(And the mom programmed it.)]

---

# Think back to 1.0...

<img src="content/images/total-crates-over-time.svg" alt="Total crates over time" width="1000rem" height="auto">

.one-dot-oh[![Arrow](content/images/Arrow.png)]

???

We're in a really different place than we were at 1.0. Back then, we
had a core language, but that was about it. We had a few production
users. Most of the standard library was unstable. We had a lot of work
to do to prove that this Rust thing could work -- that the learning
curve would be manageable, etc. 

---

# Hey, we did good!

<video width="100%" height="auto" controls="controls">
<source src="content/images/bowl-balance2.mp4" type="video/mp4">
<param name="autoplay" value="true" />
</video>

---

# Back then, we were like

.center[.p80[![Multitasking spongebob](content/images/multitasking-spongebob.gif)]]

???

In those days, we were operating a lot like a small startup. If
something had to get done, we got it done, but a lot of us were doing
all kinds of things.

---

# It's gotten better

.center[.p60[![Multitasking knitter](content/images/multitasking-knitter.gif)]]

???

- Since then, we've made a lot of progress. 
- We've got more teams.
- But many of us are still doing too much -- even if we've found ways to balance it.
- Not a startup anymore. We showed that Rust can work, and that you
  could design it in an open way. **Now we have to prove we can handle
  the details.**
- Thing is, there are a lot of details, and it's going to take a long
  time, so we've got to be organizing for the long haul.

---

# Now we gotta be like

.center[.p60[![Obama's got this](content/images/obama-got-this.gif)]]

???

So this is what the Rust community to feel like. Calm and
collected. Rational. Cool in a crisis.

---

# Organizing for the long haul

.center[.p80[![Paperwork like magic](content/images/paperwork.gif)]]

---

# Think like a volunteer

.center[.p60[![Volunteer baby](content/images/volunteer-baby.gif)]]

---

# Compiler team: working groups

- [github.com/rust-lang/compiler-team](https://github.com/rust-lang/compiler-team)

--
- Regular meetings at various levels:
  - working group
  - triage (whole team)
  - steering meeting (whole team, every 3 weeks)

--
- Working on introducing more levels of participation
  - explicit mentorship pathways

---

# Compiler team needs more than coders

> .jlord[We need an open source for **designers** (who make documentation easier to read and give an identity to a project), **journalists and scientists** (who share their data), **polyglots** (who make projects accessible to not just those who speak English), **note takers and editors** (who can make resources and documentation better), **organizers** (who can triage the many issues created in open source projects), **mappers and data wranglers** and ...] <br>
> <br>
> &mdash; Jessica Lord (emphasis mine)

.citation[`http://jlord.us/blog/osos-talk.html`]

---

# Many hands make light work

> .jlord[**We also need an open source whenever.** ... [We] are thankful for all that you can contribute whether it is two hours a week, one logo a year, or a copy edit twice a year.] <br>
> <br>
> &mdash; Jessica Lord (emphasis mine)

- Organizing meetings, taking notes, scheduling meetings
- Testing out features
- Triaging bugs
- Bisecting bugs and producing minimized test cases

.citation[`http://jlord.us/blog/osos-talk.html`]

---

# Governance Working Group

.center[.p100[![Governance WG thread](content/images/governance-wg.png)]]

.citation[`https://internals.rust-lang.org/t/governance-working-group-announcement/9637`]

---

# Thanks for listening

![Prince and princess](content/images/Prince-and-princess.png)

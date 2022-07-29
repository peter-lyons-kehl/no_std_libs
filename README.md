# Embedded & low level-friendly, no_std Rust intro

You can also see this as one [continuous
document](https://github.com/peter-kehl/embedded_low_level_rust/blob/main/README.md).

When viewing this [published as
slides](https://peter-kehl.github.io/embedded_low_level_rust):
 1. These slides are _not_ designed for mobile devices or tiny screens. See
[continuous
view](https://github.com/peter-kehl/embedded_low_level_rust/blob/main/README.md)
instead.
 1. Press letter **`o`**, or **ESC** key, to show (or hide) an overview of
    several slides.
 2. Press Ctrl Shift F (probably Command Shift F on Mac) to show (or hide) a
    search input (at the top right, very small once you zoom). Type the text to
    search for and Enter. The text will be highlighted (on the overview, too).
    Click anywhere on the slide before using the keys to navigate again.
 3. Zoom in or out (because the slides can't be scrolled down). Press Ctrl - and
    Ctrl + (Command - and Command + on Mac), or with Ctrl (Command) and mouse
    wheel, until you see the following numbers show down to 0:
```
    9
    8
    7
    6
    5
    4
    3
    2
    1
    0
```

Note: The content from this line until the next horizontal line (`---` in
[`README.md`](https://github.com/peter-kehl/embedded_low_level_rust/blob/main/README.md?plain=1))
is a "presenter's note". When viewing this in a browser, you can show it by
pressing "S". (You may need to allow browser to open a new window). See [speaker
view](https://revealjs.com/speaker-view).

TODO LATER: Move to a separate (visible) slide: Written in
[Markdown](https://revealjs.com/markdown), rendered by
[Reveal.js](https://github.com/hakimel/reveal.js) (also
[https://revealjs.com](revealjs.com)). See also this [presentation's
source](https://github.com/peter-kehl/embedded_low_level_rust/blob/main/README.md?plain=1).

# Rendered with: Reveal.js
If you'd like to render this locally (for example, when editing `README.md`),
you need to run a web server. Then you can access this in a web browser as (a
part of) `index.html`. See [Reveal.js > Markdown > External
Markdown](https://revealjs.com/markdown/#external-markdown). You can also [test
snippets of markdown](https://marked.js.org/demo).

This uses my (identical/clean) clone of
[Reveal.js](https://github.com/hakimel/reveal.js), and I suggest you get your
clone. That's because, unfortunately, Reveal.js doesn't publish/document how to
load its CSS & JS files online (and they don't seem to be publicly available on
CDN's, either). Instead, it wants us to [distribute its
copies](https://revealjs.com/installation). However, that would make the actual
presentation's repository much larger. It would also mean more work when
updating (a copy of) Reveal.js for several presentations. Having your multiple
presentations refer to your (one) clone of Remark.js makes it simpler.

Unfortunately, https://hakimel.github.com/reveal.js/dist/reveal.js and related
files are not available - most likely due to [GitHub Pages bandidth
limit](https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages#usage-limits)
of 100GB per month.

To make this GitHub repository show up [on GitHub
Pages](https://peter-kehl.github.io/embedded_low_level_rust), I configured my
clone repository's Settings > Pages > Source > Branch: `main` (and `/(root)`).

Reveal.js uses [highlight.js](https://highlightjs.org/usage). In addition to
syntax-coloring, you can even highlight selected line(s) and transition between
them. See [Markdown](https://revealjs.com/markdown) and [Presenting
Code](https://revealjs.com/code). (FYI [supported
languages](https://highlightjs.readthedocs.io/en/latest/supported-languages.html)).
See [highlight.js docs](https://highlightjs.readthedocs.io/en/latest) and its
[wiki](https://github.com/highlightjs/highlight.js/wiki).

# Alternative: Remark.js
If you don't want to clone and track Reveal.js, and if you're happy with simpler
and lightweight alternative, try [Remark.js](https://remarkjs.com) (see also its
[wiki](https://github.com/gnab/remark/wiki)). It allows your presentations to
get Remark.js's JS files online (without copying and distributing them).

For an example on how to render it online with Gitlab CLI, see an example of
[slides](https://gitlab.com/indyrs/july2022) and their
[source](https://gitlab.com/indyrs/july2022/-/blob/main/index.html). (This
example is authored by Cameron Dersham, the leader of
[Indy.rs](https://indy.rs), in July 2022. In addition to kindly sharing his
knowledge, his presentation are a good source of important Rust news, both
general and embedded.) As with [Reveal.js](revealjs.com),
[Remark.js](https://remarkjs.com) also allows you to include a [separate
Markdown file](https://github.com/gnab/remark/wiki#external-markdown=). And it
has [slide notes](https://github.com/gnab/remark/wiki/Markdown#slide-notes=) and
[presenter mode](https://github.com/gnab/remark/wiki#getting-started=), too.

However, it doesn't seem to have an ability to include (and then syntax-color)
source files (so you need to copy and paste the code examples). It doesn't seem
to allow highlighting of selected lines of example code lines, either.

Both Reveal.js and Remark.js support code source highlighting. However, only
Reveal.js can highlight specified parts of (lines), and display (parts of)
external source files.
<!-- Requiring an empty line, or a comment, here: before (but not necessarily after) the following --- (slide separator). Otherwise https://github.com/peter-kehl/embedded_low_level_rust/edit/main/README.md rendered the previous paragraph as bold/large. -->
---
# Purpose and depth
 * help general Rust developers start at low level
 * help non-Rust low level developers consider/move to low level development in
   Rust
 * an overview/introduction

# In scope
 * Rust only, and focusing on the language and development tools
 * "low level" here includes (but doesn't fully cover) the following:
 * [`no_std`](https://docs.rust-embedded.org/book/intro/no-std.html) `crates`
   only: no standard library (`std`) - with or _without heap_
 * potentially embedded, or a part of kernel
---
# Out of scope or very limited
 * most about hardware, deployment or debugging of embedded
 * low level development in general (techniques, architectures, tools)
 * specifics of [real
   time](https://doc.rust-lang.org/nightly/embedded-book/interoperability/index.html#interoperability-with-rtoss)
   applications and use with RTOS (real time OS)
   * Rust *is* suitable for real time (because of no garbage collection)
   * but that is true for general purpose or `std` applications (in Rust), too
 * `wasm` (Web Assembly), although [`no_std` crates are usually
   wasm-friendly](https://rahul-thakoor.github.io/using-no-standard-library-crates-with-webassembly)
 * [ABI](https://doc.rust-lang.org/nightly/reference/abi.html) (Application
   Binary Interface), especially
   * [`#[no_mangle]`](https://doc.rust-lang.org/nightly/reference/abi.html#the-no_mangle-attribute)
   * [type layout](https://doc.rust-lang.org/nightly/reference/type-layout.html)
     and the [Rustonomicon > Alternative
     Representations](https://doc.rust-lang.org/nightly/nomicon/other-reprs.html)
 * [`async/await` in
   no_std](https://ferrous-systems.com/blog/stable-async-on-embedded)
 * [`unsafe`
   code](https://doc.rust-lang.org/nightly/book/ch19-01-unsafe-rust.html)
   * is... unsafe, especially so in `std`, because some mistakes are very
     difficult to notice and/or reproduce. Even on the same machine, model or
     architecture, incorrect memory access (race conditions...) may show up only
     under specific conditions (threads and the related state, CPU caches
     per-core or shared between cores...).
   * even more complicated across CPU's/architectures and on NUMA (non uniform
     memory architecture) - on x86 it used to be mostly AMD, but Intel has had
     it on server CPU's, plus on desktops since [12th generation
     CPU's](https://en.wikipedia.org/wiki/Alder_Lake#Scheduler_support)).
     
     Even if a multi-level cache CPU or NUMA can detect cross-core access and it
     flushes/reloads the relevant data in the cache(s), that may counteract any
     gains expected from `unsafe`.
   * probably easier  on `no_std` embedded
     * no threads
     * no interaction with other applications or processes...
     * hence more predictability
   * FFI (Foreign Function
     Interface)/[Interoperability](https://doc.rust-lang.org/nightly/embedded-book/interoperability/index.html)
     * [calling external code from Rust:
       `extern`](https://doc.rust-lang.org/nightly/book/ch19-01-unsafe-rust.html#using-extern-functions-to-call-external-code)
     * [calling Rust functions from
       C](https://dev.to/dandyvica/how-to-call-rust-functions-from-c-on-linux-h37)
     * the mainstream [Rust from
       Python](https://saidvandeklundert.net/learn/2021-11-18-calling-rust-from-python-using-pyo3)
       with [pyo3 and
       maturin](https://towardsdatascience.com/nine-rules-for-writing-python-extensions-in-rust-d35ea3a4ec29)
       is for standard Python, so `std`-only.
       [pyo3::with_embedded_python_interpreter()](https://docs.rs/pyo3/latest/pyo3/fn.with_embedded_python_interpreter.html)
       and [RustPython/RustPython](https://github.com/RustPython/RustPython)
       "embed" Python into Rust, but they don't focus on embedded systems (and
       they most likely require `std`).
 * [Rust](https://doc.rust-lang.org) and [Cargo &
   dependencies](https://doc.rust-lang.org/nightly/cargo/reference/specifying-dependencies.html)
   in general

 # Limited scope
 * cross-platform  (often used with `no_std`/embedded)
   * (also available in `std`, where `std` library exists)
   * cross-platform builds (Rust/Cargo documentation keeps it hidden/secret)
     Cross-compilation with Cargo is [almost
     undocumented](https://doc.rust-lang.org/nightly/cargo/faq.html#does-cargo-handle-multi-platform-packages-or-cross-compilation).
     * [`.cargo/config.toml` -->
       `build.target`](https://doc.rust-lang.org/nightly/cargo/reference/config.html#buildtarget)
       (for an example, see TODO slicing-rs), or
     * [`cargo build
       --target`](https://doc.rust-lang.org/nightly/cargo/commands/cargo-build.html#compilation-options)
   * Architectures supported by Rust - in [three
     tiers](https://doc.rust-lang.org/nightly/rustc/target-tier-policy.html).
     See also [the rustc book](https://doc.rust-lang.org/nightly/rustc) >
     [Platform
     Support](https://doc.rust-lang.org/nightly/rustc/platform-support.html) -
     beware many Tier 2 wouldn't build a simple application (not even as
     heapless `no_std`).
   * [Cargo book > Platform specific
     dependencies](https://doc.rust-lang.org/nightly/cargo/reference/specifying-dependencies.html#platform-specific-dependencies)
   * per-platform build/linking configuration - have
     [`.cargo/config.toml`](https://doc.rust-lang.org/cargo/reference/config.html)
   * [`features`](https://doc.rust-lang.org/nightly/cargo/reference/features.html)
     - compile time-selectable subsets of library
     [`crates`](https://doc.rust-lang.org/nightly/cargo/appendix/glossary.html#crate)
   * per-architecture or per-`feature` [conditional
     compilation](https://doc.rust-lang.org/nightly/reference/conditional-compilation.html)
---
## Ecosystem
 * the focus here is on Rust
   [`#![no_std]`]((https://docs.rust-embedded.org/book/intro/no-std.html)
   language challenges, patterns and tips
 * we mention few architectures, `no_std` crates and tools, only
   * main stream, or
   * ones with the least development pain (easy debugging), or
   * ones with high or emerging Rust support
   * ones with an emulator 
---
# Prerequisites
 * no need for low level experience
 * knowledge of general (not necessarily low level) Rust and its tools helps,
   especially
   * [ownership](https://doc.rust-lang.org/nightly/book/ch04-00-understanding-ownership.html)
   * [package
     layout](https://doc.rust-lang.org/nightly/cargo/guide/project-layout.html)
   * [dependencies](https://doc.rust-lang.org/nightly/cargo/guide/dependencies.html)
   * anything here prefixed with "_New to Rust?_"
 * some experience with a statically typed and compiled language
 * basic understanding of CPU's, linking, heap and stack
 * Rust
   [installation](https://doc.rust-lang.org/nightly/book/ch01-01-installation.html)
   including [`rustup`](https://rust-lang.github.io/rustup) and
   [`cargo`](https://doc.rust-lang.org/nightly/cargo) (the recommended way)
 * Linux, Mac OS or Unix basics
---
# no_std
 * for low level (without an operating system, or a part of an OS kernel)
 * Have [`#![no_std]`]((https://docs.rust-embedded.org/book/intro/no-std.html)
   line at the top of your
   [crate](https://doc.rust-lang.org/nightly/cargo/appendix/glossary.html#crate)
   (`lib.rs` or a top level source file for a binary). See also
   [`package`](https://doc.rust-lang.org/nightly/cargo/appendix/glossary.html#package)
   and
   [`target](https://doc.rust-lang.org/nightly/cargo/appendix/glossary.html#target).
 * no default fatal error
   ([`panic`](https://doc.rust-lang.org/nightly/book/ch09-01-unrecoverable-errors-with-panic.html#unwinding-the-stack-or-aborting-in-response-to-a-panic))
   handler; you must choose either
 * you can provide a custom
   [`#[panic_handler]`](https://doc.rust-lang.org/nightly/std/alloc/trait.GlobalAlloc.html))
 * no [`std`](https://doc.rust-lang.org/nightly/std/index.html) library (no
   modules starting with `std::`), but
 * a limited subset of `std` is available as
   [`core`](https://doc.rust-lang.org/nightly/core/index.html). For example,
   instead of
   [`std::option::Option`](https://doc.rust-lang.org/nightly/std/option/enum.Option.html),
   use
   [`core::option::Option`](https://doc.rust-lang.org/nightly/core/option/enum.Option.html).
   There's also
   [`core::result::Result`](https://doc.rust-lang.org/nightly/core/result/enum.Result.html),
   [`core::iter::Iterator`](https://doc.rust-lang.org/nightly/core/iter/trait.Iterator.html),
   [`alloc::borrow::Cow](https://doc.rust-lang.org/alloc/borrow/enum.Cow.html)...
---
 * stack-only (no heap: no
   [`std::boxed::Box`](https://doc.rust-lang.org/nightly/std/boxed/struct.Box.html),
   no
   [`std::vec::Vec`](https://doc.rust-lang.org/nightly/std/vec/struct.Vec.html),
   not even
   [`std::String`](https://doc.rust-lang.org/nightly/std/string/struct.String.html)...)
   by default, [`std::rc::Rc`](https://doc.rust-lang.org/std/rc/struct.Rc.html),
   [`std::sync::Arc`](https://doc.rust-lang.org/std/sync/struct.Arc.html)
 * heap - only if you have an `allocator`:
   * register
     [`#[global_allocator]`](https://doc.rust-lang.org/nightly/std/prelude/v1/macro.global_allocator.html)
   * then use [`alloc`](https://doc.rust-lang.org/nightly/alloc/index.html)
     library
   * `alloc` is equivalent to the respective subset of `std`. Actually, `std`
     [re-exports `alloc` and `core`
     parts](https://doc.rust-lang.org/nightly/src/std/lib.rs.html).
   * [`alloc::boxed::Box`](https://doc.rust-lang.org/nightly/alloc/boxed/struct.Box.html),
     [`alloc::vec::Vec`](https://doc.rust-lang.org/nightly/alloc/vec/struct.Vec.html),
     [`vec!`](https://doc.rust-lang.org/nightly/alloc/macro.vec.html) macro
     (import it with `use alloc::vec;`),
     [`alloc::collections::VecDeque`](https://doc.rust-lang.org/nightly/alloc/collections/index.html#reexport.VecDeque),
     [`alloc::string::String`](https://doc.rust-lang.org/nightly/alloc/string/struct.String.html),
     [`alloc::rc::Rc`](https://doc.rust-lang.org/alloc/rc/struct.Rc.html),
     [`alloc::sync::Arc`](https://doc.rust-lang.org/alloc/sync/struct.Arc.html)
   * [`alloc::collections::BTreeSet`](https://doc.rust-lang.org/nightly/alloc/collections/index.html#reexport.BTreeSet),
     [`alloc::collections::BTreeMap`](https://doc.rust-lang.org/nightly/alloc/collections/index.html#reexport.BTreeMap)
     if your items/keys implement
     [`core::comp::Ord`](https://doc.rust-lang.org/nightly/core/cmp/trait.Ord.html)
 * either way, no
   [`std::collections::HashSet`](https://doc.rust-lang.org/nightly/std/collections/struct.HashSet.html),
   nor
   [`std::collections::HashMap`](https://doc.rust-lang.org/nightly/std/collections/struct.HashMap.html)
   (since those need a source of entropy), nor
   [`std::thread::Thread`](https://doc.rust-lang.org/nightly/std/thread/struct.Thread.html)
   (and no multi-threading)
 * Rust has `#![no_std]`, but it doesn't have `#![std]`. (Instead, availability
   of `std` library is implied if you don't have `#![no_std]`). Here we use
   `std` to refer to [`std`](https://doc.rust-lang.org/nightly/std/index.html)
   library, or to general purpose (no `no_std`) crates.
---
 * Embrace [`nightly`
   channel](https://rust-lang.github.io/rustup/concepts/toolchains.html)
   (version) of Rust. `no_std` development is challenging enough. Help yourself
   by new language ergonomics & `core` library API (for example,
   [`#[bench]`](https://doc.rust-lang.org/nightly/cargo/reference/cargo-targets.html#benchmarks)).
   A lot of `nightly` API has become part of `beta` and `stable` (and anything
   new goes through `nightly` and `stable`, anyway). See the [Rust
   Forge](https://forge.rust-lang.org) schedule.

   Also, embedded devices often have no/restricted connectivity, and no other
   software running, so `nightly` may be secure enough. Plus, any upgrades
   replace the whole application, so even if `nightly` API changes, nothing
   outside of your embedded application changes on because of it (the updated
   Rust's API). You you can go ahead and apply such changes bravely. You can
   choose a channel per-project in
   [`rust-toolchain.toml`](https://rust-lang.github.io/rustup/overrides.html#the-toolchain-file).
   See also [nightly
   Rust](https://doc.rust-lang.org/nightly/book/appendix-07-nightly-rust.html),
   [channels](https://rust-lang.github.io/rustup/concepts/channels.html),
   [Rustup overrides](https://rust-lang.github.io/rustup/overrides.html) and
   [Rustup profiles](https://rust-lang.github.io/rustup/concepts/profiles.html).

   Because of that, all Rust links here to Rust
   [`core`](https://doc.rust-lang.org/nightly/core/index.html)/[`alloc`](https://doc.rust-lang.org/nightly/alloc/index.html)
   API, [Rust book](https://doc.rust-lang.org/nightly/book) and [Cargo
   book](https://doc.rust-lang.org/nightly/cargo) have a `nightly` prefix. They
   clearly mention which parts are `nightly` (or `beta`) only. You can access it
   as `beta` by changing the prefix, or seee the stable by removing the prefix.

   See also the [Rust RFC book](https://rust-lang.github.io/rfcs).

# no_std with heap
 * Import `core::` and `alloc::` (instead of `std::`) wherever you can - even in
   `std` development. That brings awareness about what parts of your library are
   `no_std`-friendly. `std` [re-exports `core` and `alloc`
   parts](https://doc.rust-lang.org/nightly/src/std/lib.rs.html), so your
   library (whether `no_std` or `std`) will automatically work with `std`
   crates, too.

# no_std without heap
 * apply the previous, except for anything with `alloc`
 * common for microcontrollers
 * Have your functions accept
   [slices](https://doc.rust-lang.org/nightly/book/ch04-03-slices.html) (shared
   or mutable), rather than `Vec` or `String`, wherever possible. Both `Vec` and
   `String` auto cast/expose themselves as a slice. (This is a good practice
   even with heap, or in `std`.)
 * Similarly, whenever possible, have your `struct`-s and `enum`-s store
   references, or slices, rather than own the data. It does involve
   [`lifetimes`](https://www.cloudbees.com/blog/lifetimes-in-rust), but that can
   be a good practice, too.
---
 * Can't
   [`core::iter::Iterator.collect()`](https://doc.rust-lang.org/core/iter/trait.Iterator.html#method.collect).
   * Even though `collect()` does exist in `core` (and not only in `std`), it
   can collect only to implementations of
   [`core::iter::FromIterator`](https://doc.rust-lang.org/core/iter/trait.FromIterator.html).
   (That, again, exists in `core`, in addition to `std`). However, there are no
   `core`-only implementors of `FromIterator` (other than collecting zero or one
   item [to
   `core::option::Option`](https://doc.rust-lang.org/core/iter/trait.FromIterator.html#impl-FromIterator%3COption%3CA%3E%3E)
   or [to
   `core::result::Result`](https://doc.rust-lang.org/core/iter/trait.FromIterator.html#impl-FromIterator%3CResult%3CA%2C%20E%3E%3E)).
   * `collect()` doesn't exist for (mutable) arrays nor slices. Hence iterate
   and store in a (mutable) array or slice. Worried about side effects?
 * there is no dynamic/resizable data storage
   * a `no_std` design needs to batch/buffer/limit the total data
   * use slices (instead of arrays) as parameter types wherever possible
     * it helps to design function as accepting (shared or mutable) slices
     * functions may need to write to mutable slice parameters  (instead of
       returning). (Indeed, that is not idempotent. _New to Rust?_ It may sound
       less "functional". However, there are no hidden side effects in _safe_
       Rust. Any parameter that may be modified must be either
       * [`borrowed`](https://doc.rust-lang.org/nightly/book/ch04-02-references-and-borrowing.html)
         (passed) as a mutable reference or slice, or
       * passing ownership of the object:
         * [_moved_](https://doc.rust-lang.org/nightly/book/ch04-01-what-is-ownership.html#ownership-and-functions)
           (or
           [`clone()`-d](https://doc.rust-lang.org/core/clone/trait.Clone.html)
           first and then the clone is moved)
         * [_copied_](https://doc.rust-lang.org/core/marker/trait.Copy.html)
   * alternatively, use [const
     generics](https://rust-lang.github.io/rfcs/2000-const-generics.html), a
     subset of Rust
     [generics](https://doc.rust-lang.org/nightly/book/ch10-00-generics.html)
     (like C++ templates, see also [Vancouver Rust's
     presentation](https://github.com/vancouver-rs/talks/tree/master/const-generics)),
     for both function parameters and return values
     * make the array size (which has to be known in compile time) a const
       generic parameter
     * beware that generics make the executable larger, and the build process
       takes longer; you use combine (const) generics for some functions, and
       slices for other
     * as of mid 2022, const generics are not in the Rust book (not even in
       `nightly`). See the above or the [Rust
       Reference](https://doc.rust-lang.org/nightly/reference/items/generics.html#const-generics).
   * application top level function(s) define the array(s), or array-containing
     structs, on stack. Then they call the processing functions with slices, or
     with const generic-sized arrays (or their references)
   * this way you can re-use the same processing functions
   * if you can process the incoming data last in, first out (in LIFO/stack
     order), you could recurse (possibly batching the data in an array at every
     recursion level)
 * Have functions return an iterator wherever possible. (And use it for
   parameters, too. Again, a good practice even in `std`.)
   * may need to implement
     [core::iter::Iterator](https://doc.rust-lang.org/core/iter/trait.Iterator.html)
     to represents results of your transformation. Such iterators refer to the
     underlying iterator (data source/origin) and they may keep some state on
     top of it (a state machine). * You may want to combine/chain functions
     accepting and returning iterators. Use keyword
     [`impl`](https://doc.rust-lang.org/nightly/book/ch10-02-traits.html#returning-types-that-implement-traits)
     to define types like `impl Iterator<Item = YourItemType>`.
---
# Conditional compilation

# no_std-friendly development and testing
(The Embedded Rust book >
QEMU)[https://doc.rust-lang.org/nightly/embedded-book/start/qemu.html]. (It is
inconsistent or even crashes for multithreaded applications, but we can't use
threads in `no_std` anyway.)

---

# Actual programming
```rs
let five = 5usize;
let tuple = ('a', five);
```

<code>
  var a = "";
  var b = "inline code does work in Markdown, too";

  Any &lt;code...&gt; becomes a part of the result HTML, but it won't load/show the file here...
  <code data-noescape data-url="LICENSE">
  </code>
</code>

<code data-noescape data-url="LICENSE">
</code>

<code
data-url="https://raw.githubusercontent.com/ranging-rs/slicing-rs/main/src/lib.rs"
data-line-start-delimiter="#![allow(unused)]" data-line-end-delimiter="pub mod
index;"> </code>

```
```
<!-- .element: data-url="https://raw.githubusercontent.com/ranging-rs/slicing-rs/main/src/lib.rs" -->

<!-- .element: data-url="https://raw.githubusercontent.com/ranging-rs/slicing-rs/main/src/lib.rs" -->
```
```

`.` <!-- .element: data-url="https://raw.githubusercontent.com/ranging-rs/slicing-rs/main/src/lib.rs" -->

<!-- .element: data-url="https://raw.githubusercontent.com/ranging-rs/slicing-rs/main/src/lib.rs" --> `.`

---
# More resources
 * [Cargo > Build
   scripts](https://doc.rust-lang.org/nightly/cargo/reference/build-scripts.html)
 * [Unsafe code
   guidelines](https://rust-lang.github.io/unsafe-code-guidelines/layout.html)
 * Rust Foundation's [Embedded
   resources](https://doc.rust-lang.org/nightly/#embedded-systems)
   * (including the `Rustonomicon` and the `Unstable book`)
   * the [Embedded Rust book](https://doc.rust-lang.org/nightly/embedded-book) >
     [Tips for embedded C
     developers](https://doc.rust-lang.org/nightly/embedded-book/c-tips/index.html)
 * [the Embedenomicon](https://docs.rust-embedded.org/embedonomicon) > [A note
   on compiler
   support](https://docs.rust-embedded.org/embedonomicon/compiler-support.html)
---
 * [sindresorhus/awesome](https://github.com/sindresorhus/awesome) =
   [project-awesome.org](https://project-awesome.org) >
   * [Awesome Rust](https://project-awesome.org/rust-unofficial/awesome-rust) =
     [rust-unofficial/awesome-rust](https://github.com/rust-unofficial/awesome-rust)
     >
     * [Embedded (Rust) and
       cross-compiling](https://project-awesome.org/rust-unofficial/awesome-rust#embedded)
       =
       [rust-unofficial/awesome-rust#embedded](https://github.com/rust-unofficial/awesome-rust#embedded),
       its [news &
       history](https://www.trackawesomelist.com/rust-embedded/awesome-embedded-rust)
       and its [RSS
       feed](https://www.trackawesomelist.com/rust-embedded/awesome-embedded-rust/rss.xml)
     * [FFI (for many
       languages)](https://project-awesome.org/rust-unofficial/awesome-rust#embedded)
       =
       [rust-unofficial/awesome-rust#ffi](https://github.com/rust-unofficial/awesome-rust#ffi)
       (no specific RSS feed; but you can subscribe to whole
       [rust-unofficial/awesome-rust](https://github.com/rust-unofficial/awesome-rust)
       through GitHub or its [RSS
       feed](https://github.com/rust-unofficial/awesome-rust/commits/main/README.md.atom))
   * [rust-embedded](https://github.com/rust-embedded) - official working group
   * [rust-embedded/awesome-embedded-rust](https://github.com/rust-embedded/awesome-embedded-rust)
     (including realtime OS and crates for various chipboards)
---
* [crates.io](https://crates.io) >
  * [Categories](https://crates.io/categories) (out of total of 54) >
    * [No standard library (no-std)](https://crates.io/categories/no-std)
    * [Embedded development](https://crates.io/categories/embedded), [crates.io
      > API bindings (FFI)](https://crates.io/categories/api-bindings)
    * [External FFI
      bindings](https://crates.io/categories/external-ffi-bindings)
    * [Hardware support](https://crates.io/categories/hardware-support)
  * [Keywords](https://crates.io/keywords) (out of many, so not easy to find) >
    * [no_std](https://crates.io/keywords/no_std)
    * [no-heap](https://crates.io/keywords/no-heap)
    * [embedded](https://crates.io/keywords/embedded)
    * [embedded-database](https://crates.io/keywords/embedded-database)
    * [rtos](https://crates.io/keywords/rtos)
    * [bare metal](https://crates.io/keywords/bare-metal)
    * [embedded-hal](https://crates.io/keywords/embedded-hal) (Hardware
      Abstraction Layer)
    * [embedded-hal-driver](https://crates.io/keywords/embedded-hal-driver)
    * [embedded-hal-impl](https://crates.io/keywords/embedded-hal-impl)
    * check the above for how many crates or if popular
    * [sensor](https://crates.io/keywords/sensor)
    * [sdcard](https://crates.io/keywords/sdcard)
    * [smartcard](https://crates.io/keywords/smartcard)
  * examples of crates (not necessarily recommended & only a few)
    * 
 * Python >
     [CircuitPython](https://github.com/adafruit/awesome-circuitpython#readme)
     and [MicroPython](https://github.com/mcauser/awesome-micropython#readme),
     both for microcontrollers
 * most likely not [(Embedded)
   CPython](https://wiki.python.org/moin/EmbeddedPython) since it is "typical
   Linux-based", hence `std`
---
Markdown
 * headers not in CAPS
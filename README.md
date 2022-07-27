# Embedded & low level-friendly, no_std Rust intro

You can also see this as one [continuous
document](https://github.com/peter-kehl/embedded_low_level_rust/blob/main/README.md).

When viewing this [published as
slides](https://peter-kehl.github.io/embedded_low_level_rust):
 1. These slides are _not_ designed for mobile devices or tiny screens. See
[continuous
view](https://github.com/peter-kehl/embedded_low_level_rust/blob/main/README.md)
instead.
 1. Press letter **`o`**, or **ESC** key, to see (or to hide) an overview of
    several slides.
 2. Zoom in or out (because the slides can't be scrolled down). Press
Ctrl-/Ctrl+ (Command-/Command+ on Mac), or with Ctrl and mouse wheel, until you
see the following numbers show down to 0:
```
    11
    10
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
[Reveal.js](https://github.com/hakimel/reveal.js). That's because,
unfortunately, Reveal.js doesn't publish/document how to load its CSS & JS files
online (and they don't seem to be available for public on CDN's, either).
Instead, it wants us to [distribute its
copies](https://revealjs.com/installation). However, that would make the actual
presentation's repository much larger. It would also mean more work when
updating (a copy of) Reveal.js for several presentations. Having the
presentations refer to one clone of Remark.js makes it simpler.

Unfortunately, https://hakimel.github.com/reveal.js/dist/reveal.js and related
files are not available.

To make this GitHub repository show up [on GitHub
Pages](https://peter-kehl.github.io/embedded_low_level_rust), I configured its
GitHub repository's Settings > Pages > Source > Branch: `main` (and `/(root)`).

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
 * Rust only, and focusing on language and development
 * "low level" here includes (but doesn't fully cover) the following:
 * [`no_std`](https://docs.rust-embedded.org/book/intro/no-std.html) `crates`
   only: no standard library (`std`) - with or _without heap_
 * potentially embedded, or a part of kernel
 * less usual Rust aspects (present also in `std`):
   * cross-platform
   * per-architecture dependencies and build configuration
   * [`features`](https://doc.rust-lang.org/nightly/cargo/reference/features.html)
     (subsets) of library
     [`crates`](https://doc.rust-lang.org/nightly/cargo/appendix/glossary.html#crate)
   * per-architecture or per-`feature` [conditional
     compilation](https://doc.rust-lang.org/nightly/reference/conditional-compilation.html)

---
# Out of scope or limited
 * most of hardware and deployment
 * low level development in general (techniques, architectures, tools)
 * specifics of real time applications
   * Rust *is* suitable for real time (because of no garbage collection)
   * but that is true for general purpose applications (in Rust), too
 * `wasm` (Web Assembly), although [`no_std` crates are usually
   wasm-friendly](https://rahul-thakoor.github.io/using-no-standard-library-crates-with-webassembly)
 * FFI (Foreign Function Interface) and ABI (Application Binary Interface)
 * `unsafe`
 * embedded/kernel-specific
 * [`async/await` in
   no_std](https://ferrous-systems.com/blog/stable-async-on-embedded)
 * Rust in general
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
   [`core::iter::Iterator`](https://doc.rust-lang.org/nightly/core/iter/trait.Iterator.html)...
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
   [slices](https://doc.rust-lang.org/nightly/book/ch04-03-slices.html) (or
   mutable slices), rather than `Vec` or `String`, wherever possible. Both `Vec`
   and `String` auto cast/expose themselves as a slice. (This is a good practice
   even with heap, or in `std`.)
 * Similarly, have your `struct`-s and `enum`-s store references, rather than
   own the data. It does need
   [`lifetimes`](https://www.cloudbees.com/blog/lifetimes-in-rust), but that can
   be a good practice, too.
 * Can't
   [`core::iter::Iterator.collect()`](https://doc.rust-lang.org/core/iter/trait.Iterator.html#method.collect)
   if you don't need to. Even though `collect()` des exist in `core` (and not
   only in `std`), it can collect only to implementations of
   [`core::iter::FromIterator`](https://doc.rust-lang.org/core/iter/trait.FromIterator.html).
   (That, again, exists in `core`, in addition to `std`). However, there are no
   `core`-only implementors of `FromIterator` (other than collecting zero or one
   item [to
   `core::option::Option`](https://doc.rust-lang.org/core/iter/trait.FromIterator.html#impl-FromIterator%3COption%3CA%3E%3E)
   or [to
   `core::result::Result`](https://doc.rust-lang.org/core/iter/trait.FromIterator.html#impl-FromIterator%3CResult%3CA%2C%20E%3E%3E)).
   `collect()` doesn't exist for (mutable) arrays nor slices. Hence iterate and
   store in a (mutable) array or slice.
 * there is no dynamic/resizable data storage
   * a `no_std` processing needs to batch/buffer/limit the 

# Targets and Cross-compilation
https://doc.rust-lang.org/nightly/rustc/target-tier-policy.html

[the rustc book](https://doc.rust-lang.org/nightly/rustc) > [Platform
Support](https://doc.rust-lang.org/nightly/rustc/platform-support.html) - though
many Tier 2 wouldn't build a simple application, even as heapless `no_std`.
---

More resources
 * [Rust Foundation > Embedded
   resources](https://doc.rust-lang.org/nightly/#embedded-systems) including the
   `Rustonomicon` and the `Unstable book`
 * [the Embedenomicon](https://docs.rust-embedded.org/embedonomicon) > [A note
   on compiler
   support](https://docs.rust-embedded.org/embedonomicon/compiler-support.html)

---
Markdown
 * headers not in CAPS
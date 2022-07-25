# Embedded, low level, no_std Rust intro

You can also see this in one [continuous
document](https://github.com/peter-kehl/embedded_low_level_rust/blob/main/README.md).

When viewing this [published as
slides](https://peter-kehl.github.io/embedded_low_level_rust), zoom in or out
(to fit it on your screen - because the slides can't be scrolled down,
unfortunately). Zoom in/out with Ctrl-/Ctrl+ (Command-/Command+ on Mac), or
with Ctrl and mouse wheel, until you see the following numbers show down to 0:
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
README.md) is a "presenter's note". When viewing this in a browser, you can show
it by pressing "S". (You may need to allow browser to open a new window). See
[speaker view](https://revealjs.com/speaker-view).

TODO Consider moving to a separate slide (visible):
Written in [Markdown](https://revealjs.com/markdown), rendered by
[Reveal.js](https://github.com/hakimel/reveal.js) (also
[https://revealjs.com](revealjs.com)). See also this [presentation's
source](https://github.com/peter-kehl/embedded_low_level_rust/blob/main/README.md?plain=1).

# Rendered with: Reveal.js
If you'd like to render this locally (for example, when editing `README.md`),
you need to run a web server. Then you can access this in a web browser as (a
part of) `index.html`. See [Reveal.js > Markdown > External
Markdown](https://revealjs.com/markdown/#external-markdown). You can also [test
snippets of markdown](https://marked.js.org/demo).

This uses my (identical/clean) [clone of Reveal.js](). That's because,
unfortunately, Reveal.js doesn't publish/document how to load its CSS & JS files
online (and they don't seem to be available for public on CDN's, either).
Instead, it wants us to [distribute its
copies](https://revealjs.com/installation). However, that would make the actual
presentation's repository much larger. It would also mean more work when
updating (a copy of) Reveal.js for several presentations. Having the
presentations refer to one clone of Remark.js makes it simpler.

Feel free to refer to my [clone of
Reveal.js](https://peter-kehl.github.io/reveal.js). I will update it whenever
Reveal.js has a new release. Or you can clone Reveal.js yourself.
(Unfortunately, https://hakimel.github.com/reveal.js/dist/reveal.js and related
files are not available.)

To make this GitHub repository show up [on GitHub
Pages](https://peter-kehl.github.io/embedded_low_level_rust), I configured its
GitHub repository's Settings > Pages > Source > Branch: `main` (and `/(root)`).

# Alternative: Remark.js
If you don't want to clone and track Reveal.js, and if you're happy with simpler
and lightweight alternative, try [Remark.js](https://remarkjs.com) (see also its
[wiki](https://github.com/gnab/remark/wiki)). It allows your presentations to
get Remark.js' JS files online (without copying and distributing them).

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

Both Reveal.js and Remark.js support code source highlighting. However, only
Reveal.js can highlight specified parts of (lines), and display (parts of)
external source files.
---
# Purpose and depth
 * help general Rust developers start at low level
 * help non-Rust low level developers consider/move to low level development in
   Rust
 * an overview/introduction

# In scope
 * Rust only, and focusing on language and development
 * "low level" here includes (but doesn't fully cover) the following:
 * [`no_std`](https://docs.rust-embedded.org/book/intro/no-std.html) `crates` only: no standard library (`std`) - with or _without heap_
 * potentially embedded, or a part of kernel
 * less usual Rust aspects (present also in `std`):
   * cross-platform
   * per-architecture dependencies and build configuration
   * [`features`](https://doc.rust-lang.org/nightly/cargo/reference/features.html) (subsets) of library [`crates`](https://doc.rust-lang.org/nightly/cargo/appendix/glossary.html#crate)
   * per-architecture or per-`feature` [conditional compilation](https://doc.rust-lang.org/nightly/reference/conditional-compilation.html)

---
# Out of scope or limited
 * most of hardware and deployment
 * low level development in general (techniques, architectures, tools)
 * specifics of real time applications
   * Rust *is* suitable for real time (because of no garbage collection)
   * but that is true for general purpose applications (in Rust), too
 * `wasm` (Web Assembly), though `no_std` crates are usually
   [wasm-friendly](https://rahul-thakoor.github.io/using-no-standard-library-crates-with-webassembly)
 * FFI (Foreign Function Interface) and ABI (Application Binary Interface)
 * `unsafe`
 * embedded/kernel-specific
 * [`async/await` in no_std](https://ferrous-systems.com/blog/stable-async-on-embedded)
 * Rust in general
---
## Ecosystem
 * the focus is on (low level) Rust language challenges, patterns and tips
 * only some architectures, `no_std` crates and tools, but
   * main stream, or
   * with the least development pain (easy debugging), or
   * high or emerging Rust support
---
# Prerequisites
 * no need for low level experience
 * knowledge of general (not low level) Rust helps
 * some experience with a statically typed and compiled language
 * basic understanding of CPU's, linking, heap and stack
 * Linux, Mac OS or Unix basics
---
# no_std
 * low level, without an operating system (or a part of an OS)
 * Have [`#![no_std]`]((https://docs.rust-embedded.org/book/intro/no-std.html) line at the top of your [crate](https://doc.rust-lang.org/nightly/cargo/appendix/glossary.html#crate) (`lib.rs` or a top level source file for a binary). See also [`package`](https://doc.rust-lang.org/nightly/cargo/appendix/glossary.html#package) and [`target](https://doc.rust-lang.org/nightly/cargo/appendix/glossary.html#target).
 * no [`panic!`](https://doc.rust-lang.org/nightly/book/ch09-03-to-panic-or-not-to-panic.html) handler (errors abort the application); or
 * you can provide a custom [`#[panic_handler]`](https://doc.rust-lang.org/nightly/std/alloc/trait.GlobalAlloc.html))
 * no [`std`](https://doc.rust-lang.org/nightly/std/index.html) library (no modules starting with `std::`), but
 * a limited subset of `std` is available as [`core`](https://doc.rust-lang.org/nightly/core/index.html). For example, instead of [`std::option::Option`](https://doc.rust-lang.org/nightly/std/option/enum.Option.html), use [`core::option::Option`](https://doc.rust-lang.org/nightly/core/option/enum.Option.html). There's also [`core::result::Result`](https://doc.rust-lang.org/nightly/core/result/enum.Result.html), [`core::iter::Iterator`](https://doc.rust-lang.org/nightly/core/iter/trait.Iterator.html)...
 * stack-only (no heap: no [`std::boxed::Box`](https://doc.rust-lang.org/nightly/std/boxed/struct.Box.html), no [`std::vec::Vec`](https://doc.rust-lang.org/nightly/std/vec/struct.Vec.html), not even [`std::String`](https://doc.rust-lang.org/nightly/std/string/struct.String.html)...) by default
 * heap only if you have an allocator:
   * define a [`#[global_allocator]`](https://doc.rust-lang.org/nightly/std/prelude/v1/macro.global_allocator.html)
   * then use [`alloc`](https://doc.rust-lang.org/nightly/alloc/index.html) library
   * `alloc` is equivalent to the respective subset of `std`. Actually, `std` [re-exports `alloc` and `core` parts](https://doc.rust-lang.org/nightly/src/std/lib.rs.html).
   * [`alloc::boxed::Box`](https://doc.rust-lang.org/nightly/alloc/boxed/struct.Box.html), [`alloc::vec::Vec`](https://doc.rust-lang.org/nightly/alloc/vec/struct.Vec.html), [`alloc::string::String`](https://doc.rust-lang.org/nightly/alloc/string/struct.String.html)
   * [`alloc::collections::BTreeSet`](https://doc.rust-lang.org/nightly/alloc/collections/index.html#reexport.BTreeSet), [`alloc::collections::BTreeMap`](https://doc.rust-lang.org/nightly/alloc/collections/index.html#reexport.BTreeMap) if your items/keys implement [`core::comp::Ord`](https://doc.rust-lang.org/nightly/core/cmp/trait.Ord.html)
 * either way, no [`std::collections::HashSet`](https://doc.rust-lang.org/nightly/std/collections/struct.HashSet.html), nor [`std::collections::HashMap`](https://doc.rust-lang.org/nightly/std/collections/struct.HashMap.html) (since those need a source of entropy)
 * Rust has `#![no_std]`, but it doesn't have `#![std]`. (Instead, availability of `std` library is implied if you don't have `#![no_std]`). Here we use `std` to refer to [`std`](https://doc.rust-lang.org/nightly/std/index.html) library, or to general purpose (no `no_std`) crates.

# Basic development tips
 * Use `alloc` and `core` (instead of `std`) wherever you can - even in `std` development. That helps you be aware what parts of your library are `no_std`-friendly.`std` [re-exports `alloc` and `core` parts](https://doc.rust-lang.org/nightly/src/std/lib.rs.html), so your library (whether `no_std` or `std`) will automatically work with `std` crates, too.

---
Markdown
 * headers not in CAPS
<!-- The following comments hides this section from being shown by https://peter-kehl.github.io/embedded_low_level_rust. >
<!-- .slide: data-visibility="hidden" -->
This is only a part of a presentation. See
[https://peter-kehl.github.io/embedded_low_level_rust](embedded_low_level_rust)
for the whole.
---

# Embedded & low level-friendly, _no_std_ Rust intro
When viewing this [published as
slides](https://peter-kehl.github.io/embedded_low_level_rust):
 1. These slides are _not_ for mobile devices/tiny screens. See an alternative
[continuous
view](https://github.com/peter-kehl/embedded_low_level_rust/blob/main/README.md)
instead.
 2. **Zoom in**/**out** (because the slides can't be scrolled down). Press
    **`Ctrl -`** or **`Ctrl +`** (**`Command -`** or **`Command +`** on Mac), or
    **`Ctrl`** (**`Command`**) and roll the **mouse wheel**, until you see
    numbers shown down to 0 below.
 3. Prefer Firefox (it utilizes screen for code blocks better than Chrome).
 4. Press `?` question mark to get a help screen.
 5. Press the bottom left button for a menu (with list of slides & themes).
 6. Press letter **`o`** (lowercase), or **`ESC`** key, to show (or hide) an
    **overview** of the nearby slides.
 7. Press **`Ctrl Shift F`** (probably **Command Shift F** on Mac) to show (or
    hide) a **search** input (at the top right). Type the text to search for and
    **Enter**. Click anywhere on the slide before using the keys to navigate
    again. Any matching text will stay highlighted, even as you navigate to
    other slides. (It highlights any matches on the overview screen, too.)
```
    5
    4
    3
    2
    1
    0
```

Note: The content from this line on until the next slide (after the next
horizontal line `---` in source of this file
[`README.md`](https://github.com/peter-kehl/embedded_low_level_rust/blob/main/README.md?plain=1))
is a "presenter's note". When viewing this in a browser as slides [on GitHub
Pages](https://peter-kehl.github.io/embedded_low_level_rust) or
[locally](index.html) (not opened from a filesystem, but through a local web
server), you can show these notes by pressing "S". (You may need to allow
browser to open a new window). See [Reveal.js > speaker
view](https://revealjs.com/speaker-view).

If you're seeing this as a [continuous
document](https://github.com/peter-kehl/embedded_low_level_rust/blob/main/README.md)
(instead of [slides](https://peter-kehl.github.io/embedded_low_level_rust)]):
 - You will not be able to see source code examples as a part of this document.
   Instead, follow links to the respective source code. Those links highlight
   respective line ranges (which is valid unless this presentation gets out of
   data with examples).
 - You will need to open other `README_....md` documents that follow this file
   (see the end of this file, and end of the successive `README_....md`
   documents).

This presentation loads external files (example code sources that it highlights
and injects in its contents). In order to show them:
 1. Access this from a webserver (GitHub Pages, or a custom/local webserver) -
    but not from a local file opened directly in browser. See [Reveal.js >
    Markdown > External
    Markdown](https://revealjs.com/markdown/#external-markdown). You do _not_
    need `npm` - for example, you can run `python3 -m http.server` instead. But
    you need to run the webserver for a directory at least one level above the
    clone of this project - so that the webserver serves the neighbor projects,
    too.

    Beware that, as of August 2022, `python3 -m http.server` and/or Firefox
    caused `README*.md` files to be cached for up to 24 hours. Even refreshing
    the page in Firefox didn't help. It required purging Firefox cache
    (about:preferences#privacy > "Cookies and Site Data" > "Clear Data" button >
    "Cached Web Content").
 2. Have the neighbor directories. On GitHub pages, fork all related projects
    for the same organization or user as this project. See
    [`index.html`](index.html) for list of those projects. Then configure all
    those related forked GitHub repositories to publish their `main` (or
    `master`) branch to GitHub Pages. Alternatively, change the relative CSS and
    JS URL's in [`index.html`](index.html). When testing locally, update your
    forks and their local clones from the upstream repositories.

    Using relative URLs for plugins gives a benefit: People who fork/copy this
    project can use the same source code. Such relative URLs refer to their own
    GitHub forks of the plugins, hence not consuming GitHub pages bandwidth of
    the original project.

When this includes (& highlights) source code (of other projects, used as
examples), it assumes that those projects are on GitHub.
[`index.html`](index.html) also assumes that the neighbor projects are on
GitHub. However, all these principles are independent of GitHub. You may be able
to apply this to any decent source code hub that can publish the files' raw
content and with `text/javascript` MIME for JS files, such as GitLab.

TODO LATER: Move to a separate (visible) slide: Written in
[Markdown](https://revealjs.com/markdown), rendered by
[Reveal.js](https://github.com/hakimel/reveal.js) (also
[https://revealjs.com](revealjs.com)). See also this [presentation's
source](https://github.com/peter-kehl/embedded_low_level_rust/blob/main/README.md?plain=1).

## Rendered with: Reveal.js
If you'd like to render this locally (for example, when editing `README.md`),
you need to run a web server. Then you can access this in a web browser as (a
part of) `index.html`. See [Reveal.js > Markdown > External
Markdown](https://revealjs.com/markdown/#external-markdown). You can also [test
snippets of markdown](https://marked.js.org/demo).

Unfortunately, Reveal.js doesn't publish/document how to load its CSS & JS files
online (and they don't seem to be publicly available on CDN's, either). Instead,
it wants us to [distribute its copies](https://revealjs.com/installation).
However, that would make the actual presentation's repository much larger. It
would also mean more work when updating (a copy of) Reveal.js for several
presentations. Having your multiple presentations refer to your (one) clone of
Remark.js makes it simpler.

So this presentation uses my (identical/clean) clone of
[Reveal.js](https://github.com/hakimel/reveal.js). It's served/loaded through
GitHub Pages, which has [bandwidth
limit](https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages#usage-limits)
of 100GB per month.

Even though I'm sure visitors of this presentation itself won't make it go over
the bandwidth limit, it might reach the limit if authors of other presentations
link to (my) clones of `Reveal.js` and `RevealJS-Embed-Code`. Hence, please
don't link to my clones. Instead, get your own clones of
[Reveal.js](https://github.com/hakimel/reveal.js) and
[RevealJS-Embed-Code](https://github.com/befocken/revealjs-embed-code). (That
will also boost their GitHub projects. And while you're at it, please star their
GitHub repositories, too).


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

## Alternative: Remark.js
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
Reveal.js can
 - highlight specified parts of (lines), and
 - display (parts of) external source files.

Unfortunately, Reveal.js doesn't support vertical scrolling through the slides:
https://github.com/hakimel/reveal.js/issues/118. 
<!-- Requiring an empty line, or a comment, here: before (but not necessarily after) the following --- (slide separator). Otherwise https://github.com/peter-kehl/embedded_low_level_rust/edit/main/README.md rendered the previous paragraph as bold/large.
-->
---
# Audience and purpose
 * general Rust developers moving to low level
 * non-Rust low level developers moving to Rust

# In scope
 * Rust only; focusing on the language (less so on development tools)
 * [`no_std`](https://docs.rust-embedded.org/book/intro/no-std.html) library
   `crates` (without `std` library), _with_ or _without_ heap
---
# Related, but mostly out of scope
 * hardware, deployment, embedded debugging
 * low level development in general (techniques, architectures, tools)
 * specifics of [real
   time](https://doc.rust-lang.org/nightly/embedded-book/interoperability/index.html#interoperability-with-rtoss)
   applications and use with RTOS (Real Time OS)
   * Rust *is* suitable for real time (because of no garbage collection)
   * for `std` applications (in Rust), too
 * `wasm` (Web Assembly), although [`no_std` crates are usually
   wasm-friendly](https://rahul-thakoor.github.io/using-no-standard-library-crates-with-webassembly)
 * [ABI](https://doc.rust-lang.org/nightly/reference/abi.html) (Application
   Binary Interface), especially
   * [`#[no_mangle]`](https://doc.rust-lang.org/nightly/reference/abi.html#the-no_mangle-attribute)
   * [type layout](https://doc.rust-lang.org/nightly/reference/type-layout.html)
     and the [Rustonomicon (Unsafe
     Rust)](https://doc.rust-lang.org/nightly/nomicon) > [Alternative
     Representations](https://doc.rust-lang.org/nightly/nomicon/other-reprs.html).
     * Rustonomicon has parts applicable to safe and/or `std` Rust, too. One of
       its gems: [Higher-Rank Trait
       Bounds](https://doc.rust-lang.org/nightly/nomicon/hrtb.html).
 * [`async/await` in
   no_std](https://ferrous-systems.com/blog/stable-async-on-embedded)

---

 * [`unsafe`
   code](https://doc.rust-lang.org/nightly/book/ch19-01-unsafe-rust.html)
   * is... unsafe, indeed. Especially so in `std`, because some mistakes are
     very difficult to notice and/or reproduce. Even on the same machine, model
     or architecture, incorrect memory access (race conditions...) may show up
     only under specific conditions (threads and the related state, CPU caches
     per-core or shared between cores...).
   * more complicated across CPU's/architectures and on NUMA (non uniform memory
     architecture) - on x86 it used to be mostly AMD, but Intel has had it on
     server CPU's, plus on desktops since [12th generation
     CPU's](https://en.wikipedia.org/wiki/Alder_Lake#Scheduler_support)).
     
     Even if a multi-level cache CPU or NUMA can detect cross-core access and it
     flushes/reloads the relevant data in the cache(s), that may counteract any
     gains expected from `unsafe`.
   * probably easier on `no_std` embedded, because of no threads & no other
     applications or processes
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
---
 # Limited scope
 * cross-platform
   * also for `std` (where `std` library exists)
   * Cargo documentation keeps this [quite
     hidden](https://doc.rust-lang.org/nightly/cargo/faq.html#does-cargo-handle-multi-platform-packages-or-cross-compilation)
     * [`.cargo/config.toml` -->
       `build.target`](https://doc.rust-lang.org/nightly/cargo/reference/config.html#buildtarget),
       for example:
       ```
       [build]
       target = "aarch64-unknown-none-softfloat"
       ```
     * or: [`cargo build
       --target`](https://doc.rust-lang.org/nightly/cargo/commands/cargo-build.html#compilation-options)
   * Architectures supported by Rust - in [three
     tiers](https://doc.rust-lang.org/nightly/rustc/target-tier-policy.html).
     See also [the rustc book](https://doc.rust-lang.org/nightly/rustc) >
     [Platform
     Support](https://doc.rust-lang.org/nightly/rustc/platform-support.html).
     Beware many Tier 2 wouldn't build a simple application (not even as
     heapless `no_std`).
   * [Cargo book > Platform specific
     dependencies](https://doc.rust-lang.org/nightly/cargo/reference/specifying-dependencies.html#platform-specific-dependencies)
   * per-platform build/linking configuration - have
     [`.cargo/config.toml`](https://doc.rust-lang.org/cargo/reference/config.html)
   * [`features`](https://doc.rust-lang.org/nightly/cargo/reference/features.html)
     - compile time-selectable subsets of library
     [`crates`](https://doc.rust-lang.org/nightly/cargo/appendix/glossary.html#crate)
---
## Ecosystem
 * the focus here is on Rust
   [`#![no_std]`]((https://docs.rust-embedded.org/book/intro/no-std.html)
   language challenges, patterns and tips
 * we mention very little about architectures, `no_std` crates or tools
<!--  and only
   * main stream, or
   * ones with the least development pain (easy debugging), or
   * ones with high or emerging Rust support
   * ones with an emulator
 -->
---
# Prerequisites
 * no need for low level experience
 * common (and a few uncommon) aspects of general (but not necessarily low
   level) Rust, especially
   * setting up a project and basics of
     [cargo](https://doc.rust-lang.org/nightly/book/ch01-03-hello-cargo.html)
   * [package
     layout](https://doc.rust-lang.org/nightly/cargo/guide/project-layout.html)
   * [dependencies](https://doc.rust-lang.org/nightly/cargo/guide/dependencies.html)
   * [`features`](https://doc.rust-lang.org/nightly/cargo/reference/features.html)
   * architecture or `feature`-based [conditional
     compilation](https://doc.rust-lang.org/nightly/reference/conditional-compilation.html)
     with
     `#[cfg(...)]`(https://doc.rust-lang.org/rust-by-example/attribute/cfg.html)
     attribute.
   * [slices](https://doc.rust-lang.org/nightly/book/ch04-03-slices.html)
   * [enums](https://doc.rust-lang.org/nightly/book/ch06-01-defining-an-enum.html)
     - not as simple as Java/C++ enums, but potentially carrying
     variant-specific data field(s) (like Scala's and Haskell's algebraic types)
   * [iterators](https://doc.rust-lang.org/nightly/book/ch13-02-iterators.html)
     (like [C#
     iterators](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/iterators),
     or
     [java.util.stream.Stream](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/stream/Stream.html);
     but not like
     [java.util.Iterator](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Iterator.html)!)

---

   * [generics](https://doc.rust-lang.org/nightly/book/ch10-00-generics.html)
     and especially [generic data
     types](https://doc.rust-lang.org/nightly/book/ch10-01-syntax.html). (Like
     templates in C++, or [generics in other
     languages](https://www.wikiwand.com/en/Generic_programming). But no type
     erasure like in [Java
     generics](https://docs.oracle.com/javase/tutorial/java/generics/erasure.html)
     or some [Haskell generics](https://wiki.haskell.org/Generics).)
   * [const
     generics](https://rust-lang.github.io/rfcs/2000-const-generics.html). As of
     mid 2022, const generics are not in the Rust book (not even in `nightly`).
     See the above or the [Rust
     Reference](https://doc.rust-lang.org/nightly/reference/items/generics.html#const-generics).
     (See also [Vancouver Rust's
     presentation](https://github.com/vancouver-rs/talks/tree/master/const-generics).)
   * anything in this document starting with "_New to Rust?_"
   * optional (for deeper understanding of some code examples):
     [core::option](https://doc.rust-lang.org/nightly/core/option/index.html)
     and
     [core::result](https://doc.rust-lang.org/nightly/core/result/index.html)
 * experience with a statically typed and compiled language
 * basics of linking, heap and stack
 * Rust
   [installation](https://doc.rust-lang.org/nightly/book/ch01-01-installation.html)
   including [`rustup`](https://rust-lang.github.io/rustup) and
   [`cargo`](https://doc.rust-lang.org/nightly/cargo) (the recommended way)
 * Linux/Mac OS/Unix file path notation (in case you are on Windows)
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
   Rust's API). You you can go ahead and apply such changes bravely.
   
   If you need `beta` or `nightly`, specify it per-project in
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

---

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
   * `collect()` doesn't exist for arrays nor slices. Hence we need to iterate
   and store in a (mutable) array or slice. Worried about side effects? _safe_
   Rust prevents them, because we "[cannot have a mutable reference while we
   have an immutable
   one](https://doc.rust-lang.org/nightly/book/ch04-02-references-and-borrowing.html#mutable-references)
   to the same value."
 * there is no dynamic/resizable data storage
   * a `no_std` design needs to batch/buffer/limit the total data
   * use slices (instead of arrays) as parameter types wherever possible
     * design function as accepting (shared or mutable) slices
     * functions may need to write to mutable slice parameters  (instead of
       returning).

---

   * _New to Rust?_ Mutating slices or references/arrays may sound less
     "functional". But, in Rust any mutated parameters must be declared so. Any
     parameter that may be modified must be either
     * [`borrowed`](https://doc.rust-lang.org/nightly/book/ch04-02-references-and-borrowing.html)
       (passed) as a mutable reference or slice (which has exclusive access), or
     * passing ownership of the object:
       * [_"move"-d_](https://doc.rust-lang.org/nightly/book/ch04-01-what-is-ownership.html#ownership-and-functions)
         (or
         [`clone()`-d](https://doc.rust-lang.org/core/clone/trait.Clone.html)
         first and then the clone is moved), or
       * [_copied_: Ownership > Stack-Only Data: Copy]
         ](https://doc.rust-lang.org/nightly/book/ch04-01-what-is-ownership.html#stack-only-data-copy)
         if it implements [`Copy`
         ](https://doc.rust-lang.org/core/marker/trait.Copy.html) trait. _New to
         Rust?_ A `trait` is similar to an `interface` in Java, or a virtual
         abstract field-less class with virtual methods in C++.
     * See also
       [ownership](https://doc.rust-lang.org/nightly/book/ch04-00-understanding-ownership.html),
       [borrowing](https://doc.rust-lang.org/nightly/book/ch04-02-references-and-borrowing.html)
       and
       [lifetimes](https://doc.rust-lang.org/nightly/book/ch10-03-lifetime-syntax.html).
   * alternatively, use [`const`
     generics](https://rust-lang.github.io/rfcs/2000-const-generics.html), a
     subset of Rust
     [generics](https://doc.rust-lang.org/nightly/book/ch10-00-generics.html),
     for both function parameters and return values
     * make the array size (which has to be known in compile time) a `const`
       generic parameter
     * beware that generics make the executable larger, and the build process
       takes longer; it helps to combine (`const`) generics for some functions,
       and slices for other
   * application's top level function(s) define the array(s), or
     array-containing structs/enums, on stack. Then they call the processing
     functions with slices, or with const generic-sized arrays (or their
     references)

---

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
     top of it (a state machine).
   * You may want to combine/chain functions accepting and returning iterators.
     Use keyword
     [`impl`](https://doc.rust-lang.org/nightly/book/ch10-02-traits.html#returning-types-that-implement-traits)
     to define types like `impl Iterator<Item = YourItemType>`.
---
# no_std without heap > collect() alternatives
When developing for `no_heap`, we can't `collect()` from iterators. That makes
some tasks that need access to all items at the same time (like sorting) very
difficult.

This would need limit on number of items to be known at build time. Then the
caller would pass a (mutable) reference to an array, or a slice, where we would
manually collect the items (in a `for` loop, or `.foreach()` closure).

---

# no_std without heap > Compound iterators
For some purposes we may not need access to all items if we
don't need to access the whole collection. Then all we do needs sequential access
only, for example a one-to-one transformation, and/or filtering.

For that we may need to implement a compound iterator. It would contain an
underlying iterator (or several iterators) over the source data. It iterates and
transforms and/or filters the source data.

[Exercism Rust track](https://exercism.org/tracks/rust/exercises) > 
[RNA
Transcription](https://exercism.org/tracks/rust/exercises/rna-transcription)

https://github.com/peter-kehl/x-rust/blob/main/rust/rna-transcription-std/src/lib.rs

https://github.com/peter-kehl/x-rust/blob/main/rust/rna-transcription/src/lib.rs

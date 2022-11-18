<!-- The following comment hides this section from being shown by
     https://peter-kehl.github.io/no_std_libs.
-->
<!-- .slide: data-visibility="hidden" -->
# Slides and alternative navigation

If you are seeing this, consider viewing [presentation slides
(online)](https://peter-kehl.github.io/no_std_libs) instead. Or see [README-NAVIGATE-SLIDES.md
(online)](https://github.com/peter-kehl/present_markdown_reveal.js/blob/main/README-NAVIGATE-SLIDES.md)
for alternatives.

---

<!-- .slide: id="Audience-Purpose-Scope" -->
# Audience, Purpose, Scope <!-- .element: class="header_only_for_menu" -->

## Audience and purpose

- general Rust developers moving to low level or `no_std`
- non-Rust low level developers moving to Rust

## Disambiguation

Rust has `#![no_std]` declaration, but it doesn't have `#![std]`. Instead, if you don't have
`#![no_std]` at the top of your crate, availability of `std` library is implied.

Here we use `std` to refer to

- either Rust [`std`](https://doc.rust-lang.org/nightly/std/index.html) library, or
- crates not declared as `no_std` (that is, crates that can use `std`).

## Scope > In

- developing [`no_std`](https://docs.rust-embedded.org/book/intro/no-std.html) library `crates`
   (without [`std`](https://doc.rust-lang.org/nightly/std/) library), _with_ or _without_ heap

---

<!-- .slide: id="Scope-Limited" -->
## Scope > Limited <!-- .element: class="header_only_for_menu" -->

# Limited: Cross-platform & features

- This applies to both `no_std` and `std`.
- Rust can build for various targets (architectures/environments). But Cargo documentation keeps it
  [hidden in Cargo book's
  FAQ](https://doc.rust-lang.org/nightly/cargo/faq.html#does-cargo-handle-multi-platform-packages-or-cross-compilation)
  how to specify a target:
  - [`.cargo/config.toml` -->
      `build.target`](https://doc.rust-lang.org/nightly/cargo/reference/config.html#buildtarget),
      for example:

      ```rust
      [build]
      target = "aarch64-unknown-none-softfloat"
      ```

  - or: [`cargo build
      --target`](https://doc.rust-lang.org/nightly/cargo/commands/cargo-build.html#compilation-options)
- Architectures supported by Rust are in [three
   tiers](https://doc.rust-lang.org/nightly/rustc/target-tier-policy.html). See also the [rustc
   book](https://doc.rust-lang.org/nightly/rustc) > [Platform
   Support](https://doc.rust-lang.org/nightly/rustc/platform-support.html). Beware many Tier 2
   wouldn't build a simple (`no_std`) application - not even heapless.
- The [Cargo book > Platform specific
   dependencies](https://doc.rust-lang.org/nightly/cargo/reference/specifying-dependencies.html#platform-specific-dependencies)
- Per-platform build/linking configuration - have
   [`.cargo/config.toml`](https://doc.rust-lang.org/cargo/reference/config.html).
- [features](https://doc.rust-lang.org/nightly/cargo/reference/features.html): Compile
  time-selectable subsets of library
  [`crates`](https://doc.rust-lang.org/nightly/cargo/appendix/glossary.html#crate).

---

<!-- .slide: id="Scope-Out" -->
# Scope > Out

- `no_std` binaries
- hardware, deployment, embedded debugging
- low level development in general (techniques, architectures, tools)
- specifics of [real
  time](https://doc.rust-lang.org/nightly/embedded-book/interoperability/index.html#interoperability-with-rtoss)
  applications and use with RTOS (Real Time OS)
  - Rust _is_ suitable for real time (because of no garbage collection)
  - this applies to both `no_std` and `std`
- `wasm` (Web Assembly), although [`no_std` crates are usually
   wasm-friendly](https://rahul-thakoor.github.io/using-no-standard-library-crates-with-webassembly)
- [ABI](https://doc.rust-lang.org/nightly/reference/abi.html) (Application Binary Interface),
   especially
  - [`#[no_mangle]`](https://doc.rust-lang.org/nightly/reference/abi.html#the-no_mangle-attribute)
  - [type layout](https://doc.rust-lang.org/nightly/reference/type-layout.html) and the
     [Rustonomicon (Unsafe Rust)](https://doc.rust-lang.org/nightly/nomicon) > [Alternative
     Representations](https://doc.rust-lang.org/nightly/nomicon/other-reprs.html).
    - Rustonomicon has parts applicable to safe and/or `std` Rust, too. One of its gems:
       [Higher-Rank Trait Bounds](https://doc.rust-lang.org/nightly/nomicon/hrtb.html).
- [`async/await` in no_std](https://ferrous-systems.com/blog/stable-async-on-embedded)
- particular `no_std`-compatible crates

---

<!-- .slide: id="Scope-Out-Unsafe" -->
# Scope > Out > Unsafe

- [`unsafe` code](https://doc.rust-lang.org/nightly/book/ch19-01-unsafe-rust.html)
  - seemingly easier in embedded, because of no threads & no other applications/processes. But that
    may lead to hidden bugs that show up only once using the same code in non-embedded later.
  - FFI (Foreign Function
     Interface)/[Interoperability](https://doc.rust-lang.org/nightly/embedded-book/interoperability/index.html)
    - [calling external code from Rust:
       `extern`](https://doc.rust-lang.org/nightly/book/ch19-01-unsafe-rust.html#using-extern-functions-to-call-external-code)
    - [calling Rust functions from
       C](https://dev.to/dandyvica/how-to-call-rust-functions-from-c-on-linux-h37)
- [Rust](https://doc.rust-lang.org) and [Cargo &
   dependencies](https://doc.rust-lang.org/nightly/cargo/reference/specifying-dependencies.html) in
   general

---

<!-- .slide: id="Prerequisites" -->
# Prerequisites

- no need for low level experience
- common (and a few uncommon) aspects of general Rust, especially
  - setting up a project and basics of
     [cargo](https://doc.rust-lang.org/nightly/book/ch01-03-hello-cargo.html)
  - [package layout](https://doc.rust-lang.org/nightly/cargo/guide/project-layout.html)
  - [dependencies](https://doc.rust-lang.org/nightly/cargo/guide/dependencies.html)
  - [features](https://doc.rust-lang.org/nightly/cargo/reference/features.html)
  - architecture or feature-based [conditional
     compilation](https://doc.rust-lang.org/nightly/reference/conditional-compilation.html) with
     [`#[cfg(...)]`](<https://doc.rust-lang.org/rust-by-example/attribute/cfg.html>) attribute.
- experience with a statically typed and compiled language
- basics of linking, heap and stack
- Rust [installation](https://doc.rust-lang.org/nightly/book/ch01-01-installation.html) including
   [`rustup`](https://rust-lang.github.io/rustup) and
   [`cargo`](https://doc.rust-lang.org/nightly/cargo) (the recommended way)
- Linux/Mac OS/Unix file path notation (in case you are on Windows)

---

<!-- .slide: id="no_std" -->
# no_std

A Rust `no_std` crate can work with, or without, heap. Either way, it

- is for low level (without an operating system; or it serves as a part of an OS kernel)
- starts with a [`#![no_std]`]((<https://docs.rust-embedded.org/book/intro/no-std.html>) line at the
   top of your [crate](https://doc.rust-lang.org/nightly/cargo/appendix/glossary.html#crate)
   (`lib.rs` or a top level source file for a binary). See also [Rust glossary >
   `package`](https://doc.rust-lang.org/nightly/cargo/appendix/glossary.html#package) and [Rust
   glossary > `target`](https://doc.rust-lang.org/nightly/cargo/appendix/glossary.html#target).
- if binary, it has no default fatal error
   ([`panic`](https://doc.rust-lang.org/nightly/book/ch09-01-unrecoverable-errors-with-panic.html#unwinding-the-stack-or-aborting-in-response-to-a-panic))
  handler; you must either
  - set it to `abort`, or
  - use one of existing (embedded-friendly) [`panic_handler`-defining
    crates](https://doc.rust-lang.org/nightly/embedded-book/start/panicking.html)
- provide a custom [`panic_handler`](https://doc.rust-lang.org/nightly/nomicon/panic-handler.html)
- if binary, and it uses heap, provide a [global
  allocator](https://doc.rust-lang.org/nightly/std/alloc/trait.GlobalAlloc.html))
- has no access to [`std`](https://doc.rust-lang.org/nightly/std/index.html) library (no module
   paths starting with `std::`), but
- has a limited subset of `std` available as
  [`core`](https://doc.rust-lang.org/nightly/core/index.html). For example,
  - [`core::option::Option`](https://doc.rust-lang.org/nightly/core/option/enum.Option.html) instead
    of [`std::option::Option`](https://doc.rust-lang.org/nightly/std/option/enum.Option.html),
  - [`core::result::Result`](https://doc.rust-lang.org/nightly/core/result/enum.Result.html),
  - [`core::iter::Iterator`](https://doc.rust-lang.org/nightly/core/iter/trait.Iterator.html),
  - [`alloc::borrow::Cow`](https://doc.rust-lang.org/alloc/borrow/enum.Cow.html)...

---

<!-- .slide: id="no_std-Without-Heap" -->
# no_std > Without Heap

- all data is on stack, or static
- common for microcontrollers
- no availability of
  - [`std::boxed::Box`](https://doc.rust-lang.org/nightly/std/boxed/struct.Box.html)
  - [`std::vec::Vec`](https://doc.rust-lang.org/nightly/std/vec/struct.Vec.html)
  - [`std::String`](https://doc.rust-lang.org/nightly/std/string/struct.String.html),
  - [`std::rc::Rc`](https://doc.rust-lang.org/std/rc/struct.Rc.html),
  - [`std::sync::Arc`](https://doc.rust-lang.org/std/sync/struct.Arc.html)...

---

<!-- .slide: id="no_std-With-Heap" -->
# no_std > With Heap

- only if you have an `allocator`
  - register
     [`#[global_allocator]`](https://doc.rust-lang.org/nightly/std/prelude/v1/macro.global_allocator.html)
  - then use [`alloc`](https://doc.rust-lang.org/nightly/alloc/index.html) library
  - `alloc` is equivalent to the respective subset of `std`. Actually, `std` [re-exports `alloc` and
     `core` parts](https://doc.rust-lang.org/nightly/src/std/lib.rs.html).
  - [`alloc::boxed::Box`](https://doc.rust-lang.org/nightly/alloc/boxed/struct.Box.html),
     [`alloc::vec::Vec`](https://doc.rust-lang.org/nightly/alloc/vec/struct.Vec.html),
     [`vec!`](https://doc.rust-lang.org/nightly/alloc/macro.vec.html) macro (import it with `use
     alloc::vec;`),
     [`alloc::collections::VecDeque`](https://doc.rust-lang.org/nightly/alloc/collections/index.html#reexport.VecDeque),
     [`alloc::string::String`](https://doc.rust-lang.org/nightly/alloc/string/struct.String.html),
     [`alloc::rc::Rc`](https://doc.rust-lang.org/alloc/rc/struct.Rc.html),
     [`alloc::sync::Arc`](https://doc.rust-lang.org/alloc/sync/struct.Arc.html)
  - [`alloc::collections::BTreeSet`](https://doc.rust-lang.org/nightly/alloc/collections/index.html#reexport.BTreeSet),
     [`alloc::collections::BTreeMap`](https://doc.rust-lang.org/nightly/alloc/collections/index.html#reexport.BTreeMap)
     if your items/keys implement
     [`core::comp::Ord`](https://doc.rust-lang.org/nightly/core/cmp/trait.Ord.html).

     Even if our `struct` (or `enum`) instances can't be ordered in human terms, or if the actual
     order doesn't matter for us, we could define some (predictable) order and use
     `BTreeSet/BTreeMap` for most types.

---

<!-- .slide: id="no_std-Any" -->
# no_std > Any

Any `no_std` code (whether heapless or with heap) is limited:

- no
     [`std::collections::HashSet`](https://doc.rust-lang.org/nightly/std/collections/struct.HashSet.html),
     nor
     [`std::collections::HashMap`](https://doc.rust-lang.org/nightly/std/collections/struct.HashMap.html)
     (since computing hashes needs a source of entropy).
- no [`std::thread::Thread`](https://doc.rust-lang.org/nightly/std/thread/struct.Thread.html) (and
  no multi-threading)

---

<!-- .slide: id="Embrace-Nightly" -->
# Embrace Nightly

- Embrace [`nightly` channel](https://rust-lang.github.io/rustup/concepts/toolchains.html) (version)
   of Rust. `no_std` development is challenging enough. Help yourself by new, often ergonomical,
   features of the language & `core` library API (for example,
   [`#[bench]`](https://doc.rust-lang.org/nightly/cargo/reference/cargo-targets.html#benchmarks)). A
   lot of `nightly` API has become part of `beta` and `stable` (and anything new goes through
   `nightly` and `stable`, anyway). See the [Rust Forge](https://forge.rust-lang.org) schedule.

   Also, embedded devices often have no/restricted connectivity, and no other software running, so
   `nightly` may be secure enough. Plus, any upgrades replace the whole application, so even if
   `nightly` API changes, nothing outside of your embedded application changes (if the only change
   was in the Rust `core` or ABI). You you can go ahead and apply such changes bravely.

   If you need `beta` or `nightly`, specify it per-project in
   [`rust-toolchain.toml`](https://rust-lang.github.io/rustup/overrides.html#the-toolchain-file) >
   `[toolchain]`. See also [nightly
   Rust](https://doc.rust-lang.org/nightly/book/appendix-07-nightly-rust.html),
   [channels](https://rust-lang.github.io/rustup/concepts/channels.html), [Rustup
   overrides](https://rust-lang.github.io/rustup/overrides.html) and [Rustup
   profiles](https://rust-lang.github.io/rustup/concepts/profiles.html).

   Because of that, all Rust links here to Rust
   [`core`](https://doc.rust-lang.org/nightly/core/index.html)/[`alloc`](https://doc.rust-lang.org/nightly/alloc/index.html)
   API, the [Rust book](https://doc.rust-lang.org/nightly/book) and the [Cargo
   book](https://doc.rust-lang.org/nightly/cargo) have a `nightly` prefix. The documentation clearly
   mentions which parts are `nightly` (or `beta`) only, anyway. If you uwant to access it as `beta`
   then change the `nightly` prefix to `beta`; or see the `stable` by removing the prefix.

   See also the [Rust RFC book](https://rust-lang.github.io/rfcs).

---

<!-- TODO USE SIMILAR: -->
<!-- .slide: data-visibility="hidden" -->
<!-- .slide: id="no_std-variations" -->
<!-- markdownlint-disable MD033 -->
<pre class="language-rust r-stretch pre_relative_to_code_github_repo_raw">
<code
data-url="src/lib.rs"
data-line-start-delimiter="#![allow(rustdoc::bare_urls)]" data-line-end-delimiter="pub mod
index;">
</code>
</pre>
<!-- markdownlint-enable MD033    -->

---
<!-- TODO DOCUMENT AND REMOVE -->
<!-- .slide: data-visibility="hidden" -->
<!-- markdownlint-disable MD033 -->
<!-- https://github.com/peter-kehl/no_std_data/blob/main/00_test_harness/../00_utils/Cargo.toml redirects to https://github.com/peter-kehl/no_std_data/blob/main/00_utils/Cargo.toml. But revealjs-embed-code doesn't support redirects. So we have to normalize the URL ourselves.

https://raw.githubusercontent.com/ranging-rs/with_heap/main/Cargo.toml
https://raw.githubusercontent.com/ranging-rs/with_heap/main/src/../Cargo.toml
-->
<!--
    Adding CSS class `code-wrapper` to `<pre>` and classes hljs rust language-rust to <code> didn't
    change anything.
-->
<pre class="language-rust r-stretch">
<code data-url="https://raw.githubusercontent.com/ranging-rs/with_heap/main/src/../Cargo.toml">
</code>
</pre>
<!-- markdownlint-enable MD033 -->

---

<!-- TODO DOCUMENT AND REMOVE -->
<!-- .slide: data-visibility="hidden" -->
<!--
    <code> without <pre> shows the source as wrapped text... and it doesn't auto-apply highlighing:
    
<code data-url="https://raw.githubusercontent.com/ranging-rs/with_heap/main/src/lib.rs"
class="hljs rust language-rust"> </code>
-->

---

<!-- .slide: id="Unit-Tests" -->
# Unit Tests

Even if a library itself is `no_std`, its unit tests (ones in modules marked with `#[cfg(test)]`)
are in a separate crate (auto-generated by `cargo test`). Hence the tests can use `alloc`, and full
`std`, too.

---

<!-- .slide: id="Builds-and-Integration-Tests" -->
# Builds and Integration Tests

- No simple way to run/debug `no_std` binaries on desktop.
- Workaround: Separate sets of crates:  `*_build` for verification (on `no_std` targets); `*_test`
  for testing (on desktop).
  - `*_ok_std_*`, `*_no_std_bare_*` (heapless) and `*_no_std_heap_*` build with the relevant
    functionality.
  - Can't use a [workspace](https://doc.rust-lang.org/nightly/cargo/reference/workspaces.html) for
     these alternatives (as all crates in a workspace share dependencies with same features).
  - So, have the above builds in a separate crate each, under a directory like
     [`test_crates/`](https://github.com/ranging-rs/slicing-rs/tree/main/test_crates).
  - `*_test` crates re-use (some of) the tests. Those are centralized under `*_any_std_test_*`.
  - Suggest their folder names to start with a prefix based on/equal to the main crate. That makes
    navigation easier (in VS Code) when you open/compare... multiple main crates with
    similar-sounding sets of build & test crates.
  - For an example see [`ranging-rs/slicing-rs`](https://github.com/ranging-rs/slicing-rs) &gt;
     [`test_crates`](https://github.com/ranging-rs/slicing-rs/tree/main/test_crates):
    - [`slicing_any_std_test`](https://github.com/ranging-rs/slicing-rs/blob/main/test_crates/slicing_any_std_test/Cargo.toml)
      (tests are not run directly here, but are shared with the following `*_test` crates)
    - [`slicing_no_std_bare_build`](https://github.com/ranging-rs/slicing-rs/blob/main/test_crates/slicing_no_std_bare_build/Cargo.toml)
    - [`slicing_no_std_bare_test`](https://github.com/ranging-rs/slicing-rs/blob/main/test_crates/slicing_no_std_bare_test/Cargo.toml)
    - [`slicing_no_std_heap_build`](https://github.com/ranging-rs/slicing-rs/blob/main/test_crates/slicing_no_std_heap_build/Cargo.toml)
    - [`slicing_no_std_heap_test`](https://github.com/ranging-rs/slicing-rs/blob/main/test_crates/slicing_no_std_heap_test/Cargo.toml)
    - [`slicing_ok_std_test`](https://github.com/ranging-rs/slicing-rs/blob/main/test_crates/slicing_ok_std_test/Cargo.toml)

---

<!-- .slide: id="no_std-Targets" -->
# no_std Targets

The above listed `test_crates/*_bare_build` and `test_crates/*_heap_build` need `no_std` targets.

## Timestamped Nightly

Suggest not to specify `channel = "nightly"` in `rust-toolchain.toml`. Why?  Unfortunately,
occasionally some targets are not available (on `nightly`). To prevent that, look up the [rustup
components history](https://rust-lang.github.io/rustup-components-history). Then in your
`rust-toolchain.toml` > `[toolchain]` have (for example) `channel = "nightly-2022-08-27"`.

However, only numeric Rust versions also qualify for the minimum supported Rust version -
[`rust-version`](https://doc.rust-lang.org/nightly/cargo/reference/manifest.html#the-rust-version-field)
in your crate's `Cargo.toml > [package]`. If you need `nightly`, you can run `rustc --version`. Then
specify its numeric version (excluding `-nightly`) in `Cargo.toml > [package] > rust-version`. And
put a timestamped `channel = "nightly-YYYY-MM-DD"` in `rust-toolchain.toml > [toolchain]`.

As of August 2022, these `no_std` targets seem to build smoothly: `aarch64-unknown-none-softfloat,
aarch64-unknown-none, x86_64-unknown-none, riscv32i-unknown-none-elf, riscv32imac-unknown-none-elf,
riscv32imc-unknown-none-elf, riscv64gc-unknown-none-elf, riscv64imac-unknown-none-elf`.

---

<!-- .slide: id="More-Takeaway-for-std" -->
# More & Takeaway for std <!-- .element: class="header_only_for_menu" -->

# More

See

- [no_std_data](../no_std_data): Patterns on no_std data handling. Code is mostly done, but slides
  are work in progress.
- [rust_incompatible_features](../rust_incompatible_features): When `std`, `no_std_bare` and
  `no_std_heap` features (and potentially other features, as needed) benefit from being mutually
  exclusive/incompatible.

# Takeaway for std

- Import `core::` and `alloc::` (instead of `std::`) wherever you can - even in `std` development.
   That brings awareness about what parts of your library are `no_std`-friendly. `std` [re-exports
   `core` and `alloc` parts](https://doc.rust-lang.org/nightly/src/std/lib.rs.html), so your library
   (whether `no_std` or `std`) will automatically work with crates that import the same symbols from
   `std`.

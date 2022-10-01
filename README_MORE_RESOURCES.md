<!-- The following comments hides this section from being shown by
     https://peter-kehl.github.io/embedded_low_level_rust.
-->
<!-- .slide: data-visibility="hidden" -->
This is only a part of a presentation. See
[https://peter-kehl.github.io/embedded_low_level_rust](embedded_low_level_rust)
for the whole presentation.
---

# More resources
 * Per-platform `rustflags` in `.cargo/config.toml`. See
   [Zero2Prod > Faster Linking]
   (https://www.lpalmieri.com/posts/2020-06-06-zero-to-production-1-setup-toolchain-ides-ci/#5-1-faster-linking).
 * [Embedded Rust book >
   QEMU](https://doc.rust-lang.org/nightly/embedded-book/start/qemu.html). (It's
   not suitable for multithreaded applications, but we can't use threads in
   `no_std` anyway.)
 * [Cargo Reference > Build
   scripts](https://doc.rust-lang.org/nightly/cargo/reference/build-scripts.html)
 * [Unsafe code
   guidelines](https://rust-lang.github.io/unsafe-code-guidelines/layout.html)
 * Rust Foundation's [Embedded
   resources](https://doc.rust-lang.org/nightly/#embedded-systems)
   * including the `Rustonomicon` and the `Unstable book`
   * the [Embedded Rust book](https://doc.rust-lang.org/nightly/embedded-book) >
     * [Tips for embedded C
       developers](https://doc.rust-lang.org/nightly/embedded-book/c-tips/index.html)
     * [Zero Cost
       Abstractions](https://doc.rust-lang.org/nightly/embedded-book/static-guarantees/zero-cost-abstractions.html)
     * [Static
       Guarantees](https://doc.rust-lang.org/nightly/embedded-book/static-guarantees/index.html).
       Worthwhile in `std` Rust, too.
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
* [rustc book](https://forge.rust-lang.org) > [Platform support (and
  tiers)](https://forge.rust-lang.org/release/platform-support.html)
---

<!--
    Ways of embedding & highlighting source code:
 
    no <pre>, just <code data-...>
    - good: Screen utilization: Takes up to the whole screen.
    - bad: No highlighting!
    - bad: Centered!
    - bad: No vertical scrollbars.

    <pre class="..."> and <code data-...>
    - good: Highlighting
    - good: Vertical scrollbars
    - bad: Little screen utilization: takes only a part of the screen!

    Use: <pre class="language-rust r-stretch"><code data-...>

    class="hljs" for <code> is optional - it gets highlighted without it, too

    No way to include an external source code form Markdown with three back ticks ```.
-->
<!-- 
    class="language-rust" seems to be enough, no need for both "language-rust code-wrapper"
-->
<!--
    <span class="r-fit-text"> here din't make it use the whole screen. Neither helped <pre class="language-rust r-fit-text">
    
    But: as per https://revealjs.com/layout, there can be only one item with "r-stretch" per slide!
-->
<pre class="language-rust r-stretch">
<code
data-url="https://raw.githubusercontent.com/ranging-rs/slicing-rs/main/src/lib.rs"
data-line-start-delimiter="#![allow(unused)]" data-line-end-delimiter="pub mod
index;">
</code>
</pre>

Note:
TODO highlight selected lines with <code data-line-numbers="3,8-10"> - or use delimiters as above

TODO put GitHub code line range link at a commit as an alternative  - to make this
accessible.

[arrform](https://docs.rs/arrform/latest/arrform) is an heapless no_std alternative to `format!(...)`.
New to Rust? Exclamation mark indicates a macro invocation. 

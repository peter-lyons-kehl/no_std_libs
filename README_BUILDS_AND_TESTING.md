<!-- The following comments hides this section from being shown by https://peter-kehl.github.io/embedded_low_level_rust. >
<!-- .slide: data-visibility="hidden" -->
This is only a part of a presentation. See
[https://peter-kehl.github.io/embedded_low_level_rust](embedded_low_level_rust)
for the whole presentation.
---

# no_std-friendly builds and testing (on desktop)
 * no simple way to run/debug `no_std` on desktop
 * workaround: separate build verification and testing
   * build for a `no_std` target (but don't test)
   * build `no_std` and `no_std` + `no_std_heap` features (on your desktop) and
     run their tests
   * build `std` and run all tests
   * can't use a
     [workspace](https://doc.rust-lang.org/nightly/cargo/reference/workspaces.html)
     for these alternatives (because all crates in workspace share dependency
     resolution)
   * have the above builds in separate crates, under a directory like
     `test_crates/`
   * test crates can re-use the tests
   * suggest their folder names to start with a prefix based on/equal to the
     main crate. That makes navigation easier (especially in VS Code) when you
     have multiple main crates with similar-sounding sets of build & test crates
   * for an example see
     [ranging-rs/slicing-rs](https://github.com/ranging-rs/slicing-rs) ->
     [test_crates](https://github.com/ranging-rs/slicing-rs/tree/main/test_crates):
     * [slicing_no_std_bare_build](https://github.com/ranging-rs/slicing-rs/blob/main/test_crates/slicing_no_std_bare_build/Cargo.toml)
     * [slicing_no_std_heap_build](https://github.com/ranging-rs/slicing-rs/blob/main/test_crates/slicing_no_std_heap_build/Cargo.toml)
     * [slicing_no_std_bare_test](https://github.com/ranging-rs/slicing-rs/blob/main/test_crates/slicing_no_std_bare_test/Cargo.toml)
     * [slicing_no_std_heap_test](https://github.com/ranging-rs/slicing-rs/blob/main/test_crates/slicing_no_std_heap_test/Cargo.toml)
     * [slicing_ok_std_test](https://github.com/ranging-rs/slicing-rs/blob/main/test_crates/slicing_ok_std_test/Cargo.toml)
     * [slicing_any_std_test](https://github.com/ranging-rs/slicing-rs/blob/main/test_crates/slicing_any_std_test/Cargo.toml)
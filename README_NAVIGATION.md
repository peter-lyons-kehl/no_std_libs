<!-- .slide: data-visibility="hidden" -->

# SEE SLIDES

This file is only a part of multiple sets of presentation slides. If you are reading this, consider
viewing slides instead. However, this can't point you to the actual slides. (Why? Because several
presentations use this file.) Instead, see

- the GitHub project (or its clone/copy) or webpage you that referred you to this file; or
- `index.html` at the root of the actual presentation that referred to this file. However, do NOT
  open it from a filesystem, but from a web server instead. See `python3` below for an example; or
- the list of the original author's
  [presentations](https://github.com/peter-kehl/peter-kehl/blob/main/README.md).

But, if you are reading this, or any related `README*.md` files (referred to from `index.html` of
the actual presentation), there are limitations:

- Start with `README.md` and follow other `README*.md` files (in the actual presentation's webroot).
  See the end of each `README*.md` file, or source of `index.html` (in the actual presentation's
  webroot).
- Unfortunately, you will not be able to see source code examples as a part of the `README*.md`
  documents. Instead, follow links to the respective source code. Those links highlight respective
  line ranges. However, source code loaded in the slides may be newer than the source code links in
  `README*.md` files. And source code shown on a video recording (if there is one) may be older or
  newer (than source code links in `README*.md` files).
- Any comments in the referred sources starting with "`presentation-`" indicate start and end of
  relevant code examples.

The rest of this file assumes that you are viewing its content through `index.html` in the relevant
presentation's webroot, either on GitHub pages or served by a local (or other) web server.

If you are reading the rest of the file from its source (locally, or from
https://github.com/peter-kehl/no_std_rust_lib_presentation/blob/main/README_NAVIGATION.md), beware
the links below that start with `blob/main/`. Such links refer to 

---

# Slides Navigation

<!-- Can't apply https://revealjs.com/markdown/#element-attributes like .element: class="..."
     to list items. That doesn't add the class to the whole list item, but it adds the class only to
     an auto-generated paragraph in that list item.
     Having a whole list inside a <span class="without_keyboard">...</span> doesn't work either
     (Reveal.js then doesn't generate an HTML list).
     Yet another try: We can't write <ol class="..."> and </ol> as raw HTML and have the list items
     entered in Markdown - they don't get transformed to HTML.
     Hence, we write raw HTML. For that we disable
     https://github.com/DavidAnson/vscode-markdownlint > MD033.
-->
<!-- markdownlint-disable MD033 -->
<ol class="without_keyboard">
   <li><strong>Zoom out</strong> until you see rows starting with 5, 4, 3, 2, 1, 0 below.</li>
   <li>You can scroll somewhat (on touchscreens only), but use two fingers to scroll.</li>
   <li>Prefer Firefox (showing code blocks better than Chrome).</li>
   <li>Bottom left button shows a list of slides & themes.</li>
   <li>TODO COPY FROM BELOW</li>
</ol>
<h1 class="with_keyboard">Essentials</h1>
<ol class="with_keyboard">
   <li><strong>Zoom out</strong> until you see rows starting with 5, 4, 3, 2, 1, 0 below.</li>
   <li><a href="https://github.com/hakimel/reveal.js/issues/118">Can't scroll</a>
       up/down/right/left, unfortunately.</li>
   <li>Prefer Firefox (showing code blocks better than Chrome).</li>
   <li>Bottom left button shows a list of slides & themes.</li>
   <li>Alternatively, see the text content as a set of limited continuous <code>README*.md</code> documents. First see <a href="https://github.com/peter-kehl/no_std_rust_lib_presentation/blob/main/README_NAVIGATION.md">README_NAVIGATION.md</a><span class="hide_on_github_pages"> (or locally README_NAVIGATION.md TODO)</span>. Only then go to <a href="README.md" class="presentation_github_repo">README.md</a> (and any successive <code>README*.md</code> files).</li>
</ol>
<h1 class="with_keyboard">Extra tips</h1>
<ol class="with_keyboard">
   <li>Navigate forth and back with arrow keys.</li>
   <li>Press <strong>?</strong> (question mark) to for help.</li>
   <li>Press <strong>o</strong> (lowercase), or <strong>`ESC`</strong> key, to show (or hide) an
       <strong>overview</strong> of the nearby slides. (Navigate through the overview with arrow
       keys.)</li>
   <li>Press <strong>Ctrl Shift F</strong> to show (or hide) a <strong>search</strong> input
       (at the top right). Type the text and <strong>Enter</strong>. Click anywhere on the slide
       to use the keys for navigation again. This search is <strong>sticky</strong>: Any matching
       text will stay highlighted, even as you navigate to other slides.</li>
</ol>
<!-- markdownlint-enable MD033 -->

```html
    5
    4
    3
    2
    1
    0
```

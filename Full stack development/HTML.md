this page will have all the HTML related notes

# Tags
## Document & Structure
- `<!doctype html>` — Declares HTML document type (HTML Living Standard).
- `<html>` — Root element. Common attrs: `lang`.
- `<head>` — Metadata container (not displayed).
- `<meta>` **(void)** — Metadata:
    - `charset="utf-8"`
    - `name="viewport" content="width=device-width, initial-scale=1"`
    - `name="description"`
    - `http-equiv` (e.g., `refresh`)
- `<title>` — Document title (tab name).
- `<link>` **(void)** — External resources (CSS, icons): `rel`, `href`, `crossorigin`, `integrity`, `as`, `media`.
- `<style>` — Embedded CSS.
- `<script>` — JS or modules: `src`, `defer`, `async`, `type="module"`, `nomodule`, `crossorigin`, `integrity`.
- `<base>` **(void)** — Base URL/target for relative links: `href`, `target`.
---
## Page Layout & Semantics

- `<body>` — Document body.
- `<header>` — Intro/header section.
- `<nav>` — Navigation links.
- `<main>` — Main content (one per page).
- `<section>` — Thematic grouping of content.
- `<article>` — Self‑contained content (blog post, card).
- `<aside>` — Sidebar/related content.
- `<footer>` — Footer section.
- `<address>` — Contact info (usually within header/footer).

---

## Text & Inline Content

- `<h1>` … `<h6>` — Headings (h1 strongest → h6 weakest).
- `<p>` — Paragraph.
- `<span>` — Generic inline container (no semantics).
- `<div>` — Generic block container (no semantics).
- `<a>` — Link or anchor: `href`, `target`, `rel`, `download`, `hreflang`, `type`, `referrerpolicy`, `ping`.
- `<strong>` — Strong importance (usually bold).
- `<em>` — Emphasis (usually italic).
- `<b>` — Stylistic bold (no extra meaning).
- `<i>` — Stylistic italic (e.g., technical terms).
- `<u>` — Non‑textual annotation (e.g., proper name spellings).
- `<s>` — No longer accurate/relevant.
- `<small>` — Side comments, fine print.
- `<mark>` — Highlighted reference.
- `<sub>` / `<sup>` — Subscript/superscript.
- `<br>` **(void)** — Line break.
- `<hr>` **(void)** — Thematic break.
- `<wbr>` **(void)** — Optional line break opportunity.
- `<time>` — Machine‑readable time/date: `datetime`.
- `<data>` — Inline data value: `value`.
- `<abbr>` — Abbreviation: `title` for expansion.
- `<cite>` — Work title citation.
- `<q>` — Inline quotation: `cite`.
- `<blockquote>` — Block quotation: `cite`.
- `<dfn>` — Defining instance of a term.
- `<code>` — Code fragment.
- `<samp>` — Sample output.
- `<kbd>` — User input (keyboard).
- `<var>` — Variable.
- `<bdi>` — Bi‑di isolation.
- `<bdo>` — Bi‑di override: `dir="ltr|rtl"`.
- `<ruby>` — East Asian annotation container.
    - `<rt>` — Ruby text (pronunciation).
    - `<rp>` — Fallback parentheses.

---

## Grouping & Figure

- `<figure>` — Self‑contained media/content.
- `<figcaption>` — Caption for figure.
- `<pre>` — Preformatted text (preserves whitespace).

---

## Lists

- `<ul>` — Unordered list.
- `<ol>` — Ordered list: `start`, `reversed`, `type`.
- `<li>` — List item; in `<ol>` can use `value`.
- `<dl>` — Description list.
    - `<dt>` — Term.
    - `<dd>` — Description.

---

## Tables

- `<table>` — Data table.
- `<caption>` — Table caption.
- `<colgroup>` — Column group.
- `<col>` **(void)** — Column attrs: `span`.
- `<thead>` / `<tbody>` / `<tfoot>` — Table sections.
- `<tr>` — Table row.
- `<th>` — Header cell: `scope="col|row|colgroup|rowgroup"`, `colspan`, `rowspan`.
- `<td>` — Data cell: `colspan`, `rowspan`.

---

## Images, Media & Embeds

- `<img>` **(void)** — Image: `src`, `alt` (required for a11y), `width`, `height`, `srcset`, `sizes`, `loading="lazy"`, `decoding`, `referrerpolicy`.
- `<picture>` — Art direction:
    - `<source>` **(void)** — `type`, `media`, `srcset`, `sizes`.
    - `<img>` — Fallback image.
- `<audio>` — Audio: `src`, `controls`, `autoplay` (usually with `muted`), `loop`, `preload`, `crossorigin`.
    - `<source>` **(void)** — Alternative sources.
    - `<track>` **(void)** — Text tracks: `kind="subtitles|captions|descriptions|chapters|metadata"`, `srclang`, `label`, `default`.
- `<video>` — Video: `src`, `controls`, `autoplay` (with `muted`), `loop`, `preload`, `poster`, `playsinline`, `width`, `height`, `crossorigin`.
- `<map>` — Image map.
    - `<area>` **(void)** — Hotspot: `shape`, `coords`, `href`, `alt`.
- `<iframe>` — Inline frame: `src`, `name`, `width`, `height`, `loading="lazy"`, `referrerpolicy`, `sandbox`, `allow`, `allowfullscreen`, `srcdoc`.
- `<embed>` **(void)** — External content: `src`, `type`, `width`, `height`.
- `<object>` — External resource: `data`, `type`, `width`, `height`.
    - `<param>` **(void)** — Parameters: `name`, `value`.

---

## Forms (Core)

- `<form>` — Form container:  
    `action`, `method="get|post"`, `enctype` (`application/x-www-form-urlencoded` | `multipart/form-data` | `text/plain`), `autocomplete`, `novalidate`, `target`, `name`, `rel` (supported in modern HTML), `accept-charset`.
    
- `<label>` — Label for control: `for` (links to control `id`) or wrap control.
    
- `<input>` **(void)** — **Form control**.  
    **Common attributes (many are type‑specific):**  
    `type`, `name`, `value`, `id`, `class`, `placeholder`, `required`, `disabled`, `readonly`, `autofocus`, `autocomplete`, `min`, `max`, `step`, `minlength`, `maxlength`, `pattern`, `size`, `list` (links to `<datalist>`), `multiple`, `accept`, `capture`, `checked`, `src` (for `image`), `alt` (for `image`), `form`, `formaction`, `formenctype`, `formmethod`, `formnovalidate`, `formtarget`, `inputmode`, `enterkeyhint`.
    
    **All input `type` values you should know:**
    
    - `text` — Single‑line text.
    - `password` — Obscured text.
    - `email` — Email validation; supports multiple if `multiple`.
    - `url` — URL validation.
    - `tel` — Telephone input (no built‑in validation).
    - `search` — Search field (styling hint).
    - `number` — Numeric input; supports `min`, `max`, `step`.
    - `range` — Slider; `min`, `max`, `step`, shows track/handle.
    - `date` — Date picker (YYYY‑MM‑DD).
    - `time` — Time picker (hh:mm[:ss]).
    - `month` — Month/year picker.
    - `week` — Week number picker.
    - `datetime-local` — Local date+time (no timezone).
    - `color` — Color well.
    - `checkbox` — On/off; `checked`, `value`.
    - `radio` — Single selection in a same‑`name` group; `checked`, `value`.
    - `file` — File upload; `accept`, `multiple`, `capture` (mobile hint).
    - `hidden` — Hidden value.
    - `submit` — Submit button.
    - `reset` — Reset button.
    - `button` — General button (no submit).
    - `image` — Submit as image button; `src`, `alt`, `width`, `height`.
- `<button>` — Clickable button:  
    `type="submit|reset|button"`, `disabled`, `autofocus`, form-* attributes (`formaction`, `formenctype`, `formmethod`, `formnovalidate`, `formtarget`), `name`, `value`.
    
- `<select>` — Dropdown/list: `name`, `multiple`, `size`, `required`, `autofocus`.
    
    - `<option>` — Option: `value`, `label`, `selected`, `disabled`.
    - `<optgroup>` — Grouped options: `label`, `disabled`.
- `<datalist>` — Options for `<input list="id">`.
    
    - `<option>` — Provide suggestions; `value` is used.
- `<textarea>` — Multiline text: `name`, `rows`, `cols`, `wrap`, `maxlength`, `minlength`, `placeholder`, `required`, `readonly`, `disabled`, `autocomplete`.
    
- `<fieldset>` — Group controls; can be `disabled`.
    
- `<legend>` — Caption for `<fieldset>`.
    
- `<output>` — Calculation/result: `for` (ids of inputs), `name`.
    
- `<progress>` — Progress bar: `value`, `max`.
    
- `<meter>` — Scalar measurement: `min`, `max`, `value`, `low`, `high`, `optimum`.
    

---

## Interactive, Disclosure & Dialog

- `<details>` — Expand/collapse disclosure; can be `open`.
    - `<summary>` — Summary/label line.
- `<dialog>` — Modal/dialog: `open`; JS methods `show()`, `showModal()`, `close()`.
- `<template>` — Inert HTML template for cloning: content not rendered.
- `<slot>` — Web Components insertion point: `name`.

---

## Graphics & Vector

- `<canvas>` — Scriptable bitmap drawing (via JS).
- `<svg>` — Inline SVG (vector graphics).  
    _(SVG has its own tag set like `<circle>`, `<path>`, etc.)_

---

## Scripting & No‑Script

- `<script>` — See above.
- `<noscript>` — Fallback if JS disabled.

---

## Global Attributes (work on most elements)

`id`, `class`, `style`, `title`, `hidden`, `tabindex`, `contenteditable`, `enterkeyhint`, `draggable`, `spellcheck`, `translate`, `dir`, `lang`, `accesskey`, `is` (for customized built‑ins), `part` (Shadow DOM), `slot` (for children of web components), `inert` (non‑interactive subtree; widely supported now), plus **ARIA**: `role`, `aria-*` for accessibility.

---

## Void (Self‑Closing) Elements

These **do not** have closing tags:  
`area`, `base`, `br`, `col`, `embed`, `hr`, `img`, `input`, `link`, `meta`, `param`, `source`, `track`, `wbr`.

---


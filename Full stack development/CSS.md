## **CSS Basics**

- `selector { property: value; }` — Basic syntax.
- **Comments:** `/* comment */`
- **Case:** Properties and values are case-insensitive (except URLs, custom props).
- **Units:** `px`, `%`, `em`, `rem`, `vh`, `vw`, `fr`, `deg`, `s`, etc.

---

## **Selectors**

- `*` — Universal selector.
- `element` — Type selector (e.g., `p`).
- `.class` — Class selector.
- `#id` — ID selector.
- `element, element` — Grouping.
- `element element` — Descendant.
- `element > element` — Direct child.
- `element + element` — Adjacent sibling.
- `element ~ element` — General sibling.
- `[attr]` — Attribute selector.
- `[attr=value]` — Exact match.
- `[attr^=value]` — Starts with.
- `[attr$=value]` — Ends with.
- `[attr*=value]` — Contains.
- `:hover`, `:focus`, `:active` — Pseudo-classes for interaction.
- `:nth-child(n)`, `:nth-of-type(n)` — Structural pseudo-classes.
- `::before`, `::after` — Pseudo-elements.
- `:root` — Root element (useful for CSS variables).
- `:not(selector)` — Negation.

---

## **Colors**

- Keywords: `red`, `blue`, `transparent`.
- Hex: `#fff`, `#ffffff`.
- RGB: `rgb(255, 255, 255)`.
- RGBA: `rgba(255, 255, 255, 0.5)`.
- HSL: `hsl(0, 100%, 50%)`.
- HSLA: `hsla(0, 100%, 50%, 0.5)`.

---

## **Box Model**

- `width`, `height` — Element size.
- `padding` — Inside spacing.
- `margin` — Outside spacing.
- `border` — Border around content.
- `box-sizing: content-box | border-box` — Box model behavior.

---

## **Display & Positioning**

- `display: block | inline | inline-block | flex | grid | none`.
- `position: static | relative | absolute | fixed | sticky`.
- `top`, `right`, `bottom`, `left` — Offsets.
- `z-index` — Stacking order.

---

## **Flexbox**

- `display: flex`.
- `flex-direction: row | column | row-reverse | column-reverse`.
- `justify-content: flex-start | center | space-between | space-around | space-evenly`.
- `align-items: flex-start | center | stretch | baseline`.
- `flex-wrap: nowrap | wrap | wrap-reverse`.
- `align-content` — Multi-line alignment.
- `flex: grow shrink basis` — Shorthand.

---

## **Grid**

- `display: grid`.
- `grid-template-columns`, `grid-template-rows`.
- `gap`, `row-gap`, `column-gap`.
- `grid-area`, `grid-column`, `grid-row`.
- `justify-items`, `align-items`, `justify-content`, `align-content`.

---

## **Typography**

- `font-family` — Font stack.
- `font-size` — Size (use `rem` for scalability).
- `font-weight: normal | bold | 100–900`.
- `font-style: normal | italic`.
- `line-height` — Vertical spacing.
- `text-align: left | center | right | justify`.
- `text-decoration: none | underline | line-through`.
- `text-transform: uppercase | lowercase | capitalize`.
- `letter-spacing`, `word-spacing`.

---

## **Backgrounds**

- `background-color`.
- `background-image: url("image.jpg")`.
- `background-repeat: repeat | no-repeat | repeat-x | repeat-y`.
- `background-position: center | top | left | x y`.
- `background-size: cover | contain | auto`.
- `background-attachment: scroll | fixed`.

---

## **Borders & Radius**

- `border: width style color`.
- `border-radius: px | %` (for rounded corners).
- `outline` — Similar to border but outside.

---

## **Lists**

- `list-style-type: disc | circle | square | none`.
- `list-style-position: inside | outside`.
- `list-style-image: url("icon.png")`.

---

## **Tables**

- `border-collapse: collapse | separate`.
- `border-spacing: px`.
- `caption-side: top | bottom`.

---

## **Transitions & Animations**

- `transition: property duration timing-function delay`.
- `transition-property`, `transition-duration`.
- `animation: name duration timing-function delay iteration-count direction`.
- `@keyframes name { from {…} to {…} }`.

---

## **Transforms**

- `transform: translate(x, y) | rotate(deg) | scale(x, y) | skew(x, y)`.

---

## **Filters**

- `filter: blur(px) | brightness(%) | contrast(%) | grayscale(%) | hue-rotate(deg)`.

---

## **CSS Variables**

- Define: `--main-color: #333;`
- Use: `color: var(--main-color);`

---

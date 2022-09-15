---
teaser:
  text: A stacked list of headers that collapse or expand content sections with user interaction.
---

# spz-accordion

Provides a way for viewers to glance at the content outline and jump to any section. This is helpful for mobile devices where even a couple of sentences into a section requires scrolling.

## Usage

The `spz-accordion` component allows you to display collapsible and expandable
content sections. This component provides a way for viewers to glance at the
content outline and jump to any section. Effective use reduces scrolling needs
on mobile devices.

-   layout only support container.
-   An `spz-accordion` accepts one or more `<section>` elements as its direct
    children or accepts normal node,example `<div>`
-   Each `<section>` must contain exactly two direct children.
-   The first child in a `<section>` is the heading for that section of the
    `spz-accordion`. It must be a heading element such as `<h1>-<h6>` or
    `<header>`.
-   The second child in a `<section>` is the expandable/collapsible content.
-   A click or tap on a `<section>` heading expands or collapses the section.
-   An `spz-accordion` with a defined `id` preserves the collapsed or expanded
    state of each section while the user remains on your domain.


## Example

The example below contains an `spz-accordion` with three sections. The
`expanded` attribute on the third section expands it on page load.

```html
<spz-accordion id="my-accordion" layout="container">
  <section>
    <h2>Section 1</h2>
    <p>Content in section 1.</p>
  </section>
  <section>
    <h2>Section 2</h2>
    <div>Content in section 2.</div>
  </section>
  <section expanded>
    <h2>Section 3</h2>
    <spz-img src="{{server_for_email}}/static/inline-examples/images/squirrel.jpg"
      width="320"
      height="256"></spz-img>
  </section>
</spz-accordion>
```

[/example]

## Attributes

### animate

Include the `animate` attribute in `<spz-accordion>` to add a "roll down"
animation when the content is expanded and "roll up" animation when collapsed.

[example]

```html
<spz-accordion layout="container" animate>
  <section>
    <h2>Section 1</h2>
    <p>Content in section 1.</p>
  </section>
  <section>
    <h2>Section 2</h2>
    <div>Content in section 2.</div>
  </section>
  <section>
    <h2>Section 3</h2>
    <spz-img
      src="{{server_for_email}}/static/inline-examples/images/squirrel.jpg"
      width="320"
      height="256"
    ></spz-img>
  </section>
</spz-accordion>
```

[/example]

### expanded

Apply the `expanded` attribute to a nested `<section>` to expand that section when the page loads.

### expand-single-section

Apply the `expand-single-section` attribute to `spz-accordion` to specify that
only one `<section>` can expand at a time. If the user clicks or taps on a
collapsed `<section>`, any currently expanded `<section>` collapses.

[example]

```html
<spz-accordion layout="container" expand-single-section>
  <section>
    <h2>Section 1</h2>
    <p>Content in section 1.</p>
  </section>
  <section>
    <h2>Section 2</h2>
    <div>Content in section 2.</div>
  </section>
  <section>
    <h2>Section 3</h2>
    <spz-img
      src="{{server_for_email}}/static/inline-examples/images/squirrel.jpg"
      width="320"
      height="256"
    ></spz-img>
  </section>
</spz-accordion>
```

[/example]
## Actions

### toggle

The `toggle` action switches the `expanded` and `collapsed` states of
`spz-accordion` sections. When called with no arguments, it toggles all sections
of the accordion. To specify a specific section, add the `section` argument and
use its corresponding `id` as the value.

[example]

```html
<spz-accordion id="myAccordion" layout="container">
  <section id="section1">
    <h2>Section 1</h2>
    <p>Bunch of awesome content</p>
  </section>
  <section>
    <h2>Section 2</h2>
    <div>Bunch of awesome content</div>
  </section>
  <section>
    <h2>Section 3</h2>
    <div>Bunch of awesome content</div>
  </section>
</spz-accordion>
<button @tap="myAccordion.toggle">Toggle All Sections</button>
<button @tap="myAccordion.toggle(section='section1')">
  Toggle Section 1
</button>
```

[/example]

### expand

The `expand` action expands the sections of the `spz-accordion`. If a section
is already expanded, it stays expanded. When called with no arguments, it
expands all sections of the accordion. To specify a section, add the `section` argument, and use its corresponding `id` as the value.

```html
<button @tap="myAccordion.expand">Expand All Sections</button>
<button @tap="myAccordion.expand(section='section1')">
  Expand Section 1
</button>
```

### collapse

The `collapse` action collapses the sections of the `spz-accordion`. If a
section is already collapsed, it stays collapsed. When called with no arguments,
it collapses all sections of the accordion. To specify a section, add the
`section` argument, and use its corresponding `id` as the value.

```html
<button @tap="myAccordion.collapse">Collapse All Sections</button>
<button @tap="myAccordion.collapse(section='section1')">
  Collapse Section 1
</button>
```

## Events

The following `spz-accordion` events trigger on accordion sections when they're
clicked or tapped.

### expand

The `expand` event triggers the targeted `spz-accordion` section to change from
the collapsed state to the expanded state. Call `expand` on an already expanded
section to trigger the `expand` event.

[example]

```html
<spz-accordion id="myAccordion" layout="container">
  <section id="section1" @expand="myAccordion.expand(section='section2')">
    <h2>Section 1</h2>
    <p>Opening me will open Section 2</p>
  </section>
  <section>
    <h2>Section 3</h2>
    <div>Bunch of awesome content</div>
  </section>
</spz-accordion>
```

[/example]

### collapse

The `collapse` event triggers the targeted `spz-accordion` section to change
from the expanded state to the collapsed state. Call `collapse` on an already
collapsed section to trigger the event.

[example]

```html
<spz-accordion id="myAccordion" layout="container">
  <section id="section2" @collapse="myAccordion.collapse(section='section1')">
    <h2>Section 2</h2>
    <div>Closing me will close Section 1</div>
  </section>
  <section>
    <h2>Section 3</h2>
    <div>Bunch of awesome content</div>
  </section>
</spz-accordion>
```

[/example]

## Styling

The `spz-accordion` element selector styles an `spz-accordion` according to your
specifications. The following example changes the background color to green:

```css
spz-accordion {
  background-color: green;
}
```

Keep the following points in mind when you style an spz-accordion:

-   `spz-accordion` elements are always `display: block`.
-   `float` cannot style a `<section>`, heading, nor content elements.
-   An expanded section applies the `expanded` attribute to the `<section>`
    element.
-   The content element is clear-fixed with `overflow: hidden` and hence cannot
    have scrollbars.
-   Margins of the `<spz-accordion>`, `<section>`, heading, and content elements
    are set to `0`, but can be overridden in custom styles.
-   Both the header and content elements are `position: relative`.

## Accessibility

-   `aria-controls`: Applied to the header element of each `spz-accordion` section.
-   `aria-expanded (state)`: Applied to the header element of each `spz-accordion` section.
-   `aria-labelledby`: Applied to the content element of each `spz-accordion` section.

`spz-accordion` also automatically adds the following accessibility attributes:

-   `tabindex`: Applied to the header element of each `spz-accordion` section.
-   `role=button`: Applied to the header element of each `spz-accordion` section.
-   `role=region`: Applied to the content element of each `spz-accordion` section.


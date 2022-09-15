# spz-toast

display tooltips info

## Usage

The `spz-toast` component defines child elements that display in a
full-viewport overlay/modal. When the user taps or clicks an element (e.g., a
button), the `spz-toast` ID referenced in the clicked element's `on`
attribute triggers the toast to take up the full viewport and displays the
child elements of the `spz-toast`.

```html
<spz-toast class="progress-bar color-body rounded-md overflow-hidden font-medium shadow bg-white" id="theme-toast" layout="nodisplay" hidden></spz-toast>
```

## Attributes

### `id`

A unique identifier for the toast.

### `layout`

Must be set to `nodisplay`.

### `animate-in` (optional)

Defines the style of animation for opening the toast. By default, this will
be set to `fade-in`. Valid values are `fade-in`, `fly-in-bottom`, and
`fly-in-top`.

### `scrollable` (optional)

When the `scrollable` attribute is present, the content of the toast can
scroll when overflowing the height of the toast.

## Actions

### `open` (default)

Opens the toast.

### `close`

Closes the toast.

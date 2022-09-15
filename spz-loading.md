# spz-loading

## Usage

The `spz-loading` component defines child elements that display in a
full-viewport overlay/modal. When the user taps or clicks an element (e.g., a
button), the `spz-loading` ID referenced in the clicked element's `on`
attribute triggers the loading to take up the full viewport and displays the
child elements of the `spz-loading`.

## Attributes

### `id`

A unique identifier for the loading.

### `layout`

Must be set to `nodisplay`.

### `animate-in` (optional)

Defines the style of animation for opening the loading. By default, this will
be set to `fade-in`. Valid values are `fade-in`, `fly-in-bottom`, and
`fly-in-top`.

### `scrollable` (optional)

When the `scrollable` attribute is present, the content of the loading can
scroll when overflowing the height of the loading.

## Actions

### `open` (default)

Opens the loading.

### `close`

Closes the loading.

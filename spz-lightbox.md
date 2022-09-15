# spz-lightbox

## Usage

The `spz-lightbox` component defines child elements that display in a
full-viewport overlay/modal. When the user taps or clicks an element (e.g., a
button), the `spz-lightbox` ID referenced in the clicked element's `on`
attribute triggers the lightbox to take up the full viewport and displays the
child elements of the `spz-lightbox`.

## Attributes

### `id`

A unique identifier for the lightbox.

### `layout`

Must be set to `nodisplay`.

### `animate-in` (optional)

Defines the style of animation for opening the lightbox. By default, this will
be set to `fade-in`. Valid values are `fade-in`, `fly-in-bottom`, and
`fly-in-top`.

### `scrollable` (optional)

When the `scrollable` attribute is present, the content of the lightbox can
scroll when overflowing the height of the lightbox.

## Actions

### `lightboxOpen` (default)

Opens the lightbox.

### `lightboxClose`

Closes the lightbox.

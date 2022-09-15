---
teaser:
  text: listen globe event to execute target api
---

# spz-event

 display currency with currency_symbol('$')

## Usage

-   layout support any type.
-   `<spz-event>` must has `target-id` attribute
-   `<spz-event>` must has `target-api` attribute
-   `<spz-event>` must has `event-name` attribute
## Example

```html
<spz-event target-id="cart-empty-render" target-api="render" event-name="dj.addToCart" layout="container"></spz-event>
```

[/example]

## Attributes

### event-name(can use`;`split)

listen document event name

### target-id

execute dom

### target-api

execute dom methods

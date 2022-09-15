---
teaser:
  text: checkout cart page
---

# spz-checkout

 checkout cart page

## Usage

-  buyNow request url is `/api/checkout/order`
-   layout only support container.
-   An `spz-atc` accepts one  `<button>` elements
-   `<button>` must contain exactly one direct children `role="content"` to click buyNow product
-   An `spz-atc` must contain `cart` attribute to get cart data
## Example

```html
  <spz-checkout layout="container" cart="#cart-list" has-loading note-id="cart-note-textarea">
      <button
        class="cart-summary-checkout-btn button-primary relative w-full mt-3"
        role="checkout"
        type="button"
      >
      <span role="content">{{ 'i18n.templates.cart.checkout' | t }}</span>
      {% include 'inner_loading', class: 'absolute inset-0' %}
    </button>
  </spz-checkout>
```

[/example]

## Attributes

### cart

 `spz-cart` id, checkout require cart data when request url

### note-id

`note` id, request data
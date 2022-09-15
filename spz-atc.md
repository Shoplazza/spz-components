---
teaser:
  text: shopping cart button collection, including logical processing of button interaction
---

# spz-atc

Provides shopping cart button status and event handle .

## Usage

The `spz-atc` component allows you to display shopping cart button and add to cart or Buy now

-   layout only support container.
-   An `spz-atc` accepts one or more `<button>` elements
-   Each `<button>` must hasAttribute `role=buyNow` or `role="addToCart"` or `role="paypal"`.
-   Each `<button>` must contain exactly one direct children `role="content"` to display product status,example
    sold out, unavailable...
-   An `spz-atc` must contain `variant` attribute or `quantity` attribute

## Example

The example below contains an `spz-atc` with two `button`. 

```html
  <spz-atc
    id="product-info-atc"
    layout="container"
    variant="#product-info-variants"
    quantity="#product-info-quantity"
    product-id="{{ product.id }}"
    hide-success-toast
    variant-id="{{ settings.selectedVariant.id }}"
    @atcSuccess="cart-popup.open;cart-popup-product-info.rerender(data=event.variants);cart-popup-product-qty.rerender(data=event.quantity);cart-popup-render.render();SPZ.navigateTo(url='/cart');">
     <button
        class="relative button-primary flex justify-center w-full"
        type="button"
        role="addToCart"
      >
       <span role="content">{{ status_lan }}</span>
      </button>
       <button
        class="relative button-primary flex justify-center w-full"
        type="button"
        role="buyNow"
      >
       <span role="content">{{ status_lan }}</span>
      </button>
      <spz-paypal
          class="paypal-loading mt-3"
          id="paypal-express-button-container"
          variant="#product-info-variants"
          quantity="#product-info-quantity"
          role="paypal"
          layout="fixed-height"
          height="52"
          paypal-js="{{ shop.payment_settings.paypal_js }}"
        ></spz-paypal>
  </spz-atc>
```

[/example]

## Attributes

### variant

get variant data in buyNow or add to cart from `spz-variant` component
add to cart is request url is `/api/cart`.
buyNow is request url is `/api/checkout/order`.

[example]

```html
<spz-atc id="addressesEditCountry"  layout="container"
    variant="#product-info-variants"
    quantity="#product-info-quantity">
     <button
        class="relative button-primary flex justify-center w-full"
        type="button"
        role="addToCart"
      >
       <span role="content">{{ status_lan }}</span>
      </button>
       <button
        class="relative button-primary flex justify-center w-full"
        type="button"
        role="buyNow"
      >
       <span role="content">{{ status_lan }}</span>
      </button>
  </spz-atc>
```

[/example]

### quantity

get quantity data in buyNow or add to cart from `spz-quantity` component
add to cart is request url is `/api/cart`.
buyNow is request url is `/api/checkout/order`.

[example]

```html
<spz-atc id="addressesEditCountry"  layout="container"
    variant="#product-info-variants"
    quantity="#product-info-quantity">
     <button
        class="relative button-primary flex justify-center w-full"
        type="button"
        role="addToCart"
      >
       <span role="content">{{ status_lan }}</span>
      </button>
       <button
        class="relative button-primary flex justify-center w-full"
        type="button"
        role="buyNow"
      >
       <span role="content">{{ status_lan }}</span>
      </button>
  </spz-atc>
```

[/example]

### product-id
product id of the buyNow or addToCart

[example]

```html
  <spz-atc
    id="product-info-atc"
    layout="container"
    variant="#product-info-variants"
    quantity="#product-info-quantity"
    product-id="{{ product.id }}">
     <button
        class="relative button-primary flex justify-center w-full"
        type="button"
        role="addToCart"
      >
       <span role="content">{{ status_lan }}</span>
      </button>
       <button
        class="relative button-primary flex justify-center w-full"
        type="button"
        role="buyNow"
      >
       <span role="content">{{ status_lan }}</span>
      </button>
  </spz-atc>
```

[/example]

### variant-id
variant id of the buyNow or addToCart

[example]

```html
  <spz-atc
    id="product-info-atc"
    layout="container"
    variant="#product-info-variants"
    quantity="#product-info-quantity"
    product-id="{{ product.id }}"
    variant-id="{{ settings.selectedVariant.id }}">
     <button
        class="relative button-primary flex justify-center w-full"
        type="button"
        role="addToCart"
      >
       <span role="content">{{ status_lan }}</span>
      </button>
       <button
        class="relative button-primary flex justify-center w-full"
        type="button"
        role="buyNow"
      >
       <span role="content">{{ status_lan }}</span>
      </button>
  </spz-atc>
```

[/example]

### locale-map
 buyNow or addToCart is locale map, container operation feedback information and status,default is 

 ```
 {
  'available': 'Add to cart',
  'soldOut': 'Sold out',
  'unavailable': 'Unavailable',
  'selectVariant': 'Please select {{variants}}',
  'atcSuccessToast': 'Added to your cart!',
  'soldOutToast': 'Sorry, the goods have been sold out.',
  'unavailableToast': 'Product is unavailable.',
}
 ```

[example]

```html
  <script id="atc-locale-json" type="application/json">{
    "available": {{ 'i18n.products.product.add_to_cart' | t | json }},
    "soldOut": {{ 'i18n.products.product.sold_out' | t | json }},
    "unavailable": {{ 'i18n.products.product.unavailable' | t | json }},
    "selectVariant": {{ 'i18n.products.product.please_select_variant' | t | json }},
    "soldOutToast": {{ 'i18n.products.product.sold_out_toast' | t | json }},
    "unavailableToast": {{ 'i18n.products.product.unavailable_toast' | t | json }}
  }</script>
  <spz-atc
    id="product-info-atc"
    layout="container"
    variant="#product-info-variants"
    quantity="#product-info-quantity"
    product-id="{{ product.id }}"
    variant-id="{{ settings.selectedVariant.id }}"
    locale-map="atc-locale-json">
     <button
        class="relative button-primary flex justify-center w-full"
        type="button"
        role="addToCart"
      >
       <span role="content">{{ status_lan }}</span>
      </button>
       <button
        class="relative button-primary flex justify-center w-full"
        type="button"
        role="buyNow"
      >
       <span role="content">{{ status_lan }}</span>
      </button>
  </spz-atc>
```
[/example]

### hide-success-toast
when addToCart is success, nodisplay toast information

[example]

```html
  <spz-atc
    id="product-info-atc"
    layout="container"
    variant="#product-info-variants"
    quantity="#product-info-quantity"
    product-id="{{ product.id }}"
    hide-success-toast
    variant-id="{{ settings.selectedVariant.id }}">
     <button
        class="relative button-primary flex justify-center w-full"
        type="button"
        role="addToCart"
      >
       <span role="content">{{ status_lan }}</span>
      </button>
       <button
        class="relative button-primary flex justify-center w-full"
        type="button"
        role="buyNow"
      >
       <span role="content">{{ status_lan }}</span>
      </button>
  </spz-atc>
```
[/example]
  
## Actions

### update

The `update` action update button status and  display tooltips information when variant change.

[example]

```html
<spz-variants @variantChange="product-info-atc.update(code=event.code)">Toggle All Sections</spz-variants>
```

[/example]

## Events

The following `spz-atc` events trigger on click when addToCart button click

### atcSuccess

The `atcSuccess` event triggers the targeted `spz-atc` button to click

[example]

```html
  <spz-atc
    id="product-info-atc"
    layout="container"
    variant="#product-info-variants"
    quantity="#product-info-quantity"
    product-id="{{ product.id }}"
    hide-success-toast
    variant-id="{{ settings.selectedVariant.id }}"
    @atcSuccess="cart-popup.open;cart-popup-product-info.rerender(data=event.variants);cart-popup-product-qty.rerender(data=event.quantity);cart-popup-render.render();SPZ.navigateTo(url='/cart');">
     <button
        class="relative button-primary flex justify-center w-full"
        type="button"
        role="addToCart"
      >
       <span role="content">{{ status_lan }}</span>
      </button>
       <button
        class="relative button-primary flex justify-center w-full"
        type="button"
        role="buyNow"
      >
       <span role="content">{{ status_lan }}</span>
      </button>
  </spz-atc>
```

[/example]

## Styling

The `spz-atc` element styles an `spz-atc` according to your
specifications. The following example changes the background color to green:

```css
spz-atc {
  background-color: green;
}
```

Keep the following points in mind when you style an spz-atc:

## Accessibility

-   `status`: product is status . example unselect, available, soldout, unavailable


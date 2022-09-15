# spz-paypal

when enter product detail, click paypal money
## Usage

Used with the `spz-atc` component, set `role="paypal"` attribute


```html
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
```

#### Layout and style

Support for all layout

### variant

get variant data in paypal from `spz-variant` component
paypal is request url is `/api/checkout/order`.

### quantity

get quantity data in paypal from `spz-quantity` component
paypal is request url is `/api/checkout/order`.

### `list-id`

`spz-list` id
### `num-display-active`

show page num in before and after when pagination is active

### `show-single-page`

wether hide when pagination has only one page.
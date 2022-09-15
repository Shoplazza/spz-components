# spz-quantity

quantity selector, apply to shopping cart page and quick shop page

## Usage

-  `spz-quantity` will render input dom `input` and increase button `button[name="increase"]` and decrease  
  button `button[name="decrease"]`

-  if you want to change increase and decrease svg, you can add increase Attributes svg or decrease Attributes
   svg in `spz-quantity` children element

```html
  <spz-quantity
    class="cart-item-qty border rounded-md"
    icon-class="cart-item-qty-button flex-shrink-0 clear rounded"
    number-class="cart-item-qty-input clear text-center text-lg"
    name="quantity"
    value="${item.quantity}"
    min="0"
    max="${item.available_quantity}"
    height="42"
    layout="flex-item"
    @quantityChange="cart-list.update(value=event.value, id='${item.id}', variantId='${item.variant_id}', 
    @quantityChangeToMin="cart-list.delete(id='${item.id}', variantId='${item.variant_id}', productId='${item.product_id}');"
  >
    {% include 'icon_plus', attr: 'increase' %}
    {% include 'icon_minus', attr: 'decrease' %}
  </spz-quantity>
```
#### Layout and style

Support for fix、fix-height、responsive、fill、flex-item、fluid、intrinsic layout

## Attributes

### `value`

quantity init value

### `min`

min quantity value, when current value less than min, `button[name="decrease"]` will set disabled attributes

### `max`

max quantity value, when current value more than max, `button[name="increase"]` will set disabled attributes

### `icon-class`

svg class

### `number-class`

input class
## Actions

### update

update quantity value, min or max

## Events

The following `spz-quantity` events trigger on input when they're input

### quantityChange

it will trigger when value change

### quantityChangeToMin

it will trigger when value change min value

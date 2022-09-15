---
teaser:
  text: display shopping cart page
---

# spz-cart

 shopping cart page is display and operation, operation container quantity added or quantity remove.

## Usage

-  display request url is `/api/cart`
-   layout support any type.
-   An `spz-cart` must has `template`
## Example

```html
  <spz-cart
    id="cart-list" layout="container" empty-item="cart.line_items" has-loading
    @mount="cart-note-form.init(initialXhr='/api/cart')"
    @cartDelete="cart-empty-render.render()"
    @cartIncrease="cart-summary-render-md.rerender(data=event.cart);"
    @cartDecrease="cart-empty-render.render();"
    @cartEmpty="cart-empty-render.render();">
    <template>
      <div>
        ${data.line_items.map(item => {
          const variantNames = item.options.map(option => option.value).join(' / ');

          return `
            <div class="cart-item border-bottom lg:flex lg:justify-between" id="${item.id}">
              <div class="cart-item-info flex lg:flex-1">
                <a class="block text-0" href="${item.product_url}?variant=${item.variant_id}">
                  <spz-img
                    class="rounded-lg overflow-hidden"
                    width="88"
                    height="104"
                    layout="fixed"
                    src="${item.image.src}"
                    alt="${item.image.alt || item.product_title}"
                    object-fit="cover"
                  ></spz-img>
                </a>
                <div class="cart-item-product-info md:flex-1">
                  <a class="text-base color-body-80 heading-style line-clamp-2" href="${item.product_url}?variant=${item.variant_id}">${item.product_title}</a>
                  <div class="mt-1 text-base color-body-70 break-words lg:mt-2">${variantNames}</div>
                  <div class="flex items-center md:justify-between mt-2 lg:mt-4">
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
                      @quantityChange="cart-list.update(value=event.value, id='${item.id}', variantId='${item.variant_id}', productId='${item.product_id}');"
                      @quantityChangeToMin="cart-list.delete(id='${item.id}', variantId='${item.variant_id}', productId='${item.product_id}');"
                    >
                      {% include 'icon_plus', attr: 'increase' %}
                      {% include 'icon_minus', attr: 'decrease' %}
                    </spz-quantity>
                    <button class="cart-item-info-remove flex items-center clear md:hidden" type="button" @tap="cart-list.delete(id='${item.id}', variantId='${item.variant_id}', productId='${item.product_id}');">
                      {% include 'icon_close_lg', icon_class: 'mr-1' %}
                      <span>{{ 'i18n.templates.cart.remove' | t }}</span>
                    </button>
                    <spz-currency class="cart-item-price flex-shrink-0 text-lg text-right lg:hidden" layout="container" value="${item.price}"></spz-currency>
                  </div>
                </div>
              </div>
              <spz-currency class="flex-shrink-0 text-lg md:hidden" layout="container" value="${item.price}"></spz-currency>
              <button class="cart-item-info-remove flex items-center clear mt-3 lg:hidden" type="button" @tap="cart-list.delete(id='${item.id}', variantId='${item.variant_id}', productId='${item.product_id}');">
                {% include 'icon_close_lg', icon_class: 'mr-1' %}
                <span>{{ 'i18n.templates.cart.remove' | t }}</span>
              </button>
            </div>
          `;
        }).join('')}
      </div>
    </template>
  </spz-cart>
```

[/example]

## Attributes

### empty-item
 Empty status field from 'api/cart'
## Actions

### update

The `update` action update product quantity when `spz-quantity` change can trigger, request url is 'api/cart/product.id', methods is `PATCH`

### delete

The `delete` action delete product quantity, request url is 'api/cart/product.id', methods is `DELETE`

### render

The `render` action render cart template, request url is 'api/cart'


## Events

The following `spz-cart` events trigger on click when button click

### cartDelete

The `cartDelete` event triggers the targeted `spz-cart` execute delete action

### cartEmpty

The `cartEmpty` event triggers the targeted `spz-cart` is no-data

### cartIncrease

The `cartIncrease` event triggers the targeted `spz-cart` quantity increase, when `spz-cart `execute update action

### cartDecrease

The `cartDecrease` event triggers the targeted `spz-cart` quantity decrease, when `spz-cart `execute update action

### mount

The `cartDelete` event triggers the targeted `spz-cart` is mount


## Styling

The `spz-cart` element styles an `spz-cart` according to your
specifications. The following example changes the background color to green:

```css
spz-cart {
  background-color: green;
}
```

Keep the following points in mind when you style an spz-cart:

## Accessibility

-   `data-empty`: cart is empty status

-   `loading`: cart request is loading

-   `finish`: cart request finish


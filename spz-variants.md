---
teaser:
  text: display variant data, you don't need to handle any variant data
---

# spz-variants

## Usage

-   layout only support container layout.
-   An `spz-variants` must has `<role="variant">` elements, it can `spz-selector` or `spz-render` ...
-   An `spz-variants` have two render mode, manual or fetch url
-   An `spz-variants` have two mode, Whether there is relationship between variants by `relative` attribute
## Example

[example]

```html
   <spz-variants id="addressesEditCountry"
    layout="container"
    variant="#product-info-variants"
    quantity="#product-info-quantity">
    <spz-selector
      class="{% unless is_thumbnail %} mt-1 {% endunless %}"
      role="variant"
      name="{{ opt.name }}"
      layout="container"
      @select="product-info-selected-variant-{{ optName }}.rerender(data=event);product-info-variants.change(data=event);"
      @clear="product-info-selected-variant-{{ optName }}.rerender(data=event);"
    ></spz-selector>
  </spz-variants>
```

[/example]

## Attributes

### manual

manual render variant, you must trigger render event

### src

fetch url. example `src="/api/products/${data.id}"` or `src="script:product-json"`

### switch-slide

support switch slide type, example `switch-slide='settings.product_image_switch_variants'`

### slide

trigger slide dom change, eg. `spz-carousel`, example `slide="product-main-images;product-main-images-md;"`


### async

get async variant data, example `async="#variant"`

### locale-unavailable-toast

when variant data is unavailable, it show toast information.

### relative

Whether there is relationship between variants
## Actions

### rerender

The `rerender` action to rerender variant.

### render

The `render` action to render variant.

### change

The `change` action to trigger variant.

## Events

The following `spz-variants` events trigger on select change

### variantChange

The `variantChange` event triggers the targeted `spz-variants` select to change

change data, example:
```html
disabledValues: [],
name: '',
productId: '',
variant: {},
selectedValues: [],
product: {},

```


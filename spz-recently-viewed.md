# spz-recently-viewed

display the recently browsed product information, it will save product info to localStorage, 

it will call the `spz-list` refresh api, product info is refresh params
## Usage

-  `spz-recently-viewed` must has `list-id` attribute, `list-id` is `spz-list` id
-  `spz-recently-viewed` must has `product-id` attribute, `product-id` is current product id

[example]

```html
 <spz-recently-viewed layout="container" count="16" list-id="recently-view-render" product-id="{{ product.id }}"></spz-recently-viewed>
  
```

[/example]
#### Layout and style

support only container layout

## Attributes

### `count`

display list count. default 16

### `list-id`

`spz-list` id, `spz-recently-viewed` will call api from get localStorage data

### `product-id`

product id currently viewed by the user



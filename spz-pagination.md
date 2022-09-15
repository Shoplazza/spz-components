# spz-pagination
Use for digist pagination
## Usage
To show a pagination navigation contains back、forward function


```html
    <spz-pagination list-id="blog-list" layout="container" num-display-active="1">
      {% include 'icon_chevron_up', attr: 'role="arrow"' %}
    </spz-pagination>
```

#### Layout and style

Support for all layout

## Attributes

### `list-id`

`spz-list` id
### `num-display-active`

show page num in before and after when pagination is active

### `show-single-page`

wether hide when pagination has only one page.
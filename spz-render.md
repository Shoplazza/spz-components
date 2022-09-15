# spz-render

Renders remote or inline data using a template.
## Usage

-  `spz-render` must has `template` attribute or children has `template` tag

-  if `spz-render` without `manual` attribute, `spz-render` must has `src` attribute
-  if `spz-render` has `manual` attribute, `spz-render` must trigger `render` action

```html
<spz-render class="collection-roll-arrows md:hidden" id="collection-roll-arrows-{{ section.id }}" layout="container" manual>
  <template>
    <div class="flex">
      <div class="collection-roll-arrows-item mr-1" data-disabled="${data.index == 0}" @tap="collection-roll-carousel-{{ section.id }}.goToSlide(index=${data.index - 1},animate=true,direct=-1);">
        {% include 'icon_chevron_up', attr: 'prev', icon_class: 'rotate--90' %}
      </div>
      <div class="collection-roll-arrows-item" data-disabled="${data.index + 3.5 > data.total}" @tap="collection-roll-carousel-{{ section.id }}.goToSlide(index=${data.index + 1},animate=true,direct=1);">
        {% include 'icon_chevron_up', attr: 'next', icon_class: 'rotate-90' %}
      </div>
    </div>
  </template>
</spz-render>
```

#### Layout and style

only Support container layout

## Attributes

### `src`

request url or local json data, example `src='script:id'` or `src='api/xxxx'`

### `manual`

ssr render or manual call render

### `duration`

animate duration, use when replacing dom

## Actions

### render

when `spz-render` has manual attribute, it will used, param has src, it will fetch url

`render(src='/api/product)`

### rerender

load data `rerender(data=event.cart)`
## Events

### finish

request url finish action
## Styling

The `spz-render` element styles an `spz-render` according to your
specifications. The following example changes the background color to green:

```css
spz-render {
  background-color: green;
}
```

Keep the following points in mind when you style an spz-render:

## Accessibility

-   `data-empty`: render is empty status

-   `loading`: render request is loading

-   `finish`: render request finish


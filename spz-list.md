---
teaser:
  text: Dynamically downloads data and creates list items using a template.
---
# spz-list
## Usage

Dynamically downloads data and creates list items using a template.

-  `spz-list` has three mode, example infinite-scroll, click load more or pagination mode, infinite-scroll/loadmore/pagination can not be available at the same time.
-  if want to load more, `spz-list` content is must has `role="loadmore"`
-  if want to infinite-scroll, `spz-list` must has `infinite-scroll` attribute
-  if want to pagination, `spz-pagination` must has `list-id` attribute

```html
  <spz-list
    id="blog-list"
    row
    layout="container"
    total="count"
    list="articles"
    size="per_page"
    initial-page="1"
    page-size="{{ limit }}"
    initial-total="{{ blog.article_count }}"
    src="/api/front/{{ blog.url | slice: 1 }}/articles"
    keep-behavior="page"
    infinite-scroll
  >
  <template>
    <div class="tw-top-10">
      <p>${text}</p>
      <spz-img src="${img}">
    </div>
  </template>
    <div class="load-more flex justify-center w-full mt-10 pointer-events-none lg:mt-20" role="loadmore" hidden>
    <button class="load-more-btn button-secondary-style pointer-events-auto" type="button">{{ 'i18n.general.general.load_more' | t }}</button>
  </div>
</spz-list>
<spz-pagination list-id="blog-list" layout="container" num-display-active="1">
  {% include 'icon_chevron_up', attr: 'role="arrow"' %}
</spz-pagination>
```

## Layout and style
The `spz-list` component has a container layout type. 

## Attributes

### `manual`

ssr render, required calling methods manually

### `column` or `row`

Waterfall layout or flex layout
### `src`

use for fetch data from remote services optional

### `list`

default `data.list`, to render a subset of the JSON response, allowing you to have multiple `<spz-list>` elements rendering different content but sharing a single XHR.

### `total`

default `data.total`, get total data from request data

### `infinite-scroll`

infinite scroll

### `page`

page field, default `page`, request params

### `size`

limit field, default `limit`, request params

### `page-size`

How many are displayed on one page， default '1000'

### `initial-page`

Initial page， default '0'

### `initial-total`

Initial total

### `root-margin`

when infinite-scroll mode, observer last element margin

### `keep-behavior`

when pagination node, add params in url, it should be queries splited by "," eg "page,size,filter"

## Actions (optional)

### `refresh`

refresh list data

### `render`

render template from data

## Styling

The `spz-list` element styles an `spz-list` according to your
specifications. The following example changes the background color to green:

```css
spz-list {
  background-color: green;
}
```

Keep the following points in mind when you style an spz-list:

## Accessibility

-   `data-empty`: list is empty status

-   `loading`: list request is loading

-   `finish`: list request finish

-   `hasmore`: list has more data

-   `nomore`: list has not data





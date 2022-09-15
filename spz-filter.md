---
teaser:
  text: handle filter page
---

# spz-filter

## Usage

-   layout support any type.
-   `<spz-filter>` must has `content-id` attribute, `content-id` display filter content from request url
-   `<spz-filter>` must has `result-id` attribute, `result-id` display filter result according user choice
-   `<spz-filter>` must has `list-id` attribute, display list content
-   `<spz-filter>` must has `src` attribute， request url
## Example

```html
    <spz-filter
      id="collection-filter"
      content-id="filter-content"
      result-id="filter-result"
      list-id="collection-list-{{ collection.id }}"
      src="/api/collections/{{ collection.id }}/filters"
      layout="responsive"
      width="0"
      height="0"
      manual
    ></spz-filter>
```

[/example]

## Attributes

### filter-content(dom must use `spz-render`)

display filter content according src request url, display data container availability/price..., if you want to display different content you can add attribute in dom, you must add default attribute in some dom

```html
    <spz-accordion class="collection-filter-container break-words" id="filter-content" layout="container" animate locale-map="filter-locale-json">
    <section class="filter-item" availability {% if filter_style == 'visible' %} expanded {% endif %}>
      <spz-render  layout="container" manual template="filter-item-header-template"></spz-render>
      <spz-render layout="container" manual template="filter-item-content-template"></spz-render>
    </section>

    <section class="filter-item" price {% if filter_style == 'visible' %} expanded {% endif %}>
      <spz-render  layout="container" manual template="filter-item-header-template"></spz-render>
      <spz-render layout="container" manual template="filter-item-price-template"></spz-render>
    </section>

    <section class="filter-item" default {% if filter_style == 'visible' %} expanded {% endif %}>
      <spz-render  layout="container" manual template="filter-item-header-template"></spz-render>
      <spz-render layout="container" manual template="filter-item-content-template"></spz-render>
    </section>
  </spz-accordion>
```

### filter-result(dom must use `spz-render`)

display filter content, if you want to display different content you can add attribute in dom, you must add default attribute in some dom

```html
<div id="filter-result" class="filter-result-container flex flex-wrap items-center {{ class }}" hidden>
  <spz-render price manual layout="container">
    <template>
      <div class="filter-result-item" category="${data.category}" delete>
        <div class="filter-result-item-price flex items-center body-minus-1 cursor-pointer">
          <span spz-if="${!data.lte}">{{ 'i18n.products.collection.more_than' | t }}</span>
          <spz-currency class="inline-block" value="${data.gte || 0}" layout="container"></spz-currency>
          <span spz-if="${!!data.lte}">-</span>
          <spz-currency class="inline-block" value="${data.lte}" spz-if="${!!data.lte}" layout="container"></spz-currency>
          {% include 'icon_close', icon_class: 'flex-shrink-0' %}
        </div>
      </div>
    </template>
  </spz-render>

  <spz-render default manual layout="container">
    <template>
      <div class="filter-result-item flex items-center body-minus-1 cursor-pointer" key="${data.key}" value="${data.value}" delete>
        <div class="filter-result-item-label">${data.label}</div>
        {% include 'icon_close', icon_class: 'flex-shrink-0' %}
      </div>
    </template>
  </spz-render>

  <div class="filter-result-clear-all font-medium cursor-pointer" clear>{{ 'i18n.products.collection.clear_all' | t }}</div>
</div>
```


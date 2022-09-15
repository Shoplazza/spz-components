# spz-menu

## Usage

Displays a horizontal navigation bar with menu items that open/close content containers on click.

`<spz-menu>` provides a way to organize and display large collections of navigational content at the top of an SPZ page. The component is intended primarily for desktop and tablet use cases, and it can be used jointly with [`<spz-sidebar>`](../spz-sidebar/0.1/spz-sidebar.md) to create a responsive menu.

The `<spz-menu>` component includes a single `<nav>` element containing either a `<ul>` or `<ol>`, where each `<li>` element is a menu item.

[tip type="note"]
The `<nav>` element must be parented by either the `<spz-menu>` component or a `<template>`, and it must have `<ul>` or `<ol>` as its only child.
[/tip]

Each menu item can contain any of the following tags as direct children:

-   `<h1>`, `<h2>`, `<h3>`, `<h4>`, `<h5>`, `<h6>`
-   `<a>`
-   `<button>`
-   `<span>`
-   `<div>`

### morelink

`spz-menu` must has `hover-interact` attribute and child element must has `morelink` attribute 

```html
      <spz-menu target-id="head" hover-interact height="80" style="width: 50%;" layout="fixed-height">
        <ul spz-menu-content>
          <li dropdown>
            <span>bbbb</span>
            <ul dropdown-menu>
              <li>bbbb 2</li>
              <li>bbbb 3</li>
              <li sub-dropdown>
                <p>bbbb 1</p>
                <ul dropdown-menu>
                  <li sub-dropdown>
                    <p>cccc 1</p>
                    <ul dropdown-menu>
                      <li>
                          <a href="#">fff</a>
                      </li>
                      <li>
                          <a href="#">ggg</a>
                      </li>
                  </li>
                  <li>cccc 2</li>
                  <li>cccc 3</li>
                </ul>
              </li>
            </ul>
          </li>
          <li dropdown>
            <span>11111</span>
            <ul dropdown-menu>
              <li sub-dropdown>
                <p>1111111111111111111111111111111111111111111111111111111111111111111111111111111111111</p>
                <ul dropdown-menu>
                  <li sub-dropdown>
                    <p>aaaaa 2</p>
                    <ul dropdown-menu>
                      <li>
                          <a href="#">fff</a>
                      </li>
                      <li>
                          <a href="#">ggg</a>
                      </li>
                  </li>
                  <li>aaaa 2</li>
                  <li>aaaaa 3</li>
                </ul>
              </li>
              <li>zzzzz 2</li>
              <li>zzzzz 3</li>
            </ul>
          </li>
          <li dropdown>
            <span>222222</span>
            <ul dropdown-menu>
              <li sub-dropdown>
                <p>22222</p>
                <ul dropdown-menu>
                  <li sub-dropdown>
                    <p>22222</p>
                    <ul dropdown-menu>
                      <li>
                          <a href="#">fff</a>
                      </li>
                      <li>
                          <a href="#">ggg</a>
                      </li>
                  </li>
                  <li>22222</li>
                  <li>22222</li>
                </ul>
              </li>
              <li>22222222</li>
              <li>2222222</li>
            </ul>
          </li>
          <li dropdown>
            <span>33333</span>
            <ul dropdown-menu>
              <li sub-dropdown>
                <p>3333333</p>
                <ul dropdown-menu>
                  <li sub-dropdown>
                    <p>333333</p>
                    <ul dropdown-menu>
                      <li>
                          <a href="#">fff</a>
                      </li>
                      <li>
                          <a href="#">ggg</a>
                      </li>
                  </li>
                  <li>33333</li>
                  <li>333333</li>
                </ul>
              </li>
              <li>33333</li>
              <li>333333</li>
            </ul>
          </li>
          <li dropdown>
            <span>44444</span>
            <ul dropdown-menu>
              <li sub-dropdown>
                <p>44444</p>
                <ul dropdown-menu>
                  <li sub-dropdown>
                    <p>44444</p>
                    <ul dropdown-menu>
                      <li>
                          <a href="#">fff</a>
                      </li>
                      <li>
                          <a href="#">ggg</a>
                      </li>
                  </li>
                  <li>44444</li>
                  <li>444444</li>
                </ul>
              </li>
              <li>44444</li>
              <li>444444</li>
            </ul>
          </li>
          <li dropdown morelink>
            <span>more link</span>
            <ul dropdown-menu>
  
            </ul>
          </li>
        </ul>
      </spz-menu>
```

### Toggleable dropdowns

A menu item should have either one child (e.g. an anchor link or element with tap action), or two if the item expands into a dropdown container. In the latter case, the two children must conform to the following specs:

1. A `<button>` or element with `role=button`: this element is used to toggle the dropdown container (but only if the former has no registered tap action) and receives focus when navigating between items.
2. A `<div>` with `role=dialog`: this element will be rendered as a container that holds additional content under an item, and it is initially hidden.

A mask will cover the rest of the page when a dropdown is open. Content, such as a title banner, can appear above the mask. Apply a background color on the content and place it, alongside the `<spz-menu>`, inside a `<header>` element.

Each dropdown may contain any of the following SPZ elements:

-   `<spz-carousel>`
-   `<spz-img>`
-   `<spz-list>`

The example below demonstrates an `<spz-menu>` with three menu items. The first two are toggleable and the third is an external link.

```html
<spz-menu height="30" layout="fixed-height">
  <nav>
    <ul>
      <li>
        <span role="button">Image</span>
        <div role="dialog">
          <spz-img
            src="/static/inline-examples/images/image1.jpg"
            width="300"
            height="200"
          ></spz-img>
        </div>
      </li>
      <li>
        <span role="button">List</span>
        <div role="dialog">
          <ol>
            <li>item 1</li>
            <li>item 2</li>
            <li>item 3</li>
          </ol>
        </div>
      </li>
      <li>
        <a href="https://gitlab.shoplazza.site/shoplaza/frontend/theme/cuttlefish/">Link</a>
      </li>
    </ul>
  </nav>
</spz-menu>
```

### Dynamic content rendering

Fetch content of `<spz-menu>` dynamically from a JSON endpoint using [`<spz-list>`](../spz-list/spz-list.md) 

The example below demonstrates this ability by nesting `<spz-list>` inside `<spz-menu>`.

```html
<spz-menu height="60" layout="fixed-height">
  <spz-list
    height="350"
    layout="fixed-height"
    src="/static/samples/json/product-single-item.json"
    single-item
    items="items.values"
  >
    <template>
      <nav>
        <ul>
          <li>
            <h4 role="button">${name}</h4>
            <div role="dialog">
              <spz-img
                src="${img}"
                width="320"
                height="213"
              ></spz-img>
              <p>Price: $<b>${price}</b></p>
            </div>
          </li>
        </ul>
      </nav>
    </template>
  </spz-list>
</spz-menu>
```

Here is the JSON file used:

```json
{
  "items": {
      "values": [
        {
          "id": 1,
          "img": "/static/samples/img/product1_640x426.jpg",
          "name": "Apple",
          "price": "1.99"
        },
        {
          "id": 2,
          "img": "/static/samples/img/product2_640x426.jpg",
          "name": "Orange",
          "price": "0.99"
        },
        {
          "id": 3,
          "img": "/static/samples/img/product3_640x426.jpg",
          "name": "Pear",
          "price": "1.50"
        }
      ]
    }
}
```

### Responsive design with `<spz-sidebar>`

Some viewports may be too narrow to display the content of `<spz-menu>` in a single row. For these use cases, use media queries to switch between `<spz-menu>` and `<spz-sidebar>`.

The example below hides `<spz-menu>` when the viewport width is less than 500px. It replaces `<spz-menu>` with a button that opens `<spz-sidebar>`.

```html
<head>
  <style spz-custom>
    .sidebar-open-btn {
      font-size: 2em;
      display: none;
    }
    @media (max-width: 500px) {
      #mega-menu {
        display: none;
      }
      .sidebar-open-btn {
        display: block;
      }
    }
  </style>
</head>
<body>
  <header>
    <spz-menu id="mega-menu" height="50" layout="fixed-height">
      <nav>
        <ul>
          <!-- list of menu items here -->
          <li>
            <h4 role="button">menu item</h4>
            <div role="dialog">more content</div>
          </li>
        </ul>
      </nav>
    </spz-menu>
    <button class="sidebar-open-btn" on="tap:sidebar">=</button>
  </header>
  <spz-sidebar id="sidebar" layout="nodisplay">
    <spz-accordion>
      <!-- list of menu items here -->
      <section>
        <h4>menu item</h4>
        <div>more content</div>
      </section>
    </spz-accordion>
  </spz-sidebar>
</body>
```


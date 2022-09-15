

# spz-nested-menu


## Usage

One to three paragraphs explaining the component usage. List important functionality. Explain why developers care about it.

#### Example

The example below demonstrates `spz-nested-menu` component in standalone use.

[example]

```html
      <spz-nested-menu id="menu1" layout="fill" side="left">
        <ul class="scrollable">
          <li>
            <h3 tabindex="-1">Categories</h3>
          </li>
          <li>
            <h4 spz-nested-submenu-open>
              <span>open next1</span>
              <span class="right-arrow" aria-hidden="true">&gt;</span>
            </h4>
            <div spz-nested-submenu>
              <ul>
                <li>
                  <h4 spz-nested-submenu-close>
                    <span class="left-arrow" aria-hidden="true">&lt;</span>
                    <span>back</span>
                  </h4>
                </li>
                in next 1 <div style="width: 100px; height: 100px;background: red;"></div>
                <li>
                  <h4 spz-nested-submenu-open>
                    <span>open next2</span>
                    <span class="right-arrow" aria-hidden="true">></span>
                  </h4>
                  <div spz-nested-submenu>
                    <ul>
                      <li>
                        <h4 spz-nested-submenu-close>
                          <span class="left-arrow" aria-hidden="true">&lt;</span>
                          <span>back</span>
                        </h4>
                      </li>
                      <div style="width: 100px; height: 100px;background: green;"></div>
                    </ul>
                  </div>
                </li>
              </ul>
            </div>
          </li>
          <li>
            <a href="https://www.google.com/" tabindex="0">See More</a>
          </li>
          <li>
            <spz-img src="http://placeimg.com/300/200/tech" alt="tech image" layout="responsive" width="3" height="2"></spz-img>
            <h3 tabindex="-1">Information</h3>
          </li>
        </ul>
      </spz-nested-menu>
```

[/example]

#### Interactivity and API usage



The `spz-nested-menu` component API is accessible by including the following script tag in your document:

```
await customElements.whenDefined('spz-nested-menu-component');
const api = await NestedMenu.getApi();
```

The `spz-nested-menu` API allows you to register and respond to the following events:

**event 1**
Explanation of event, proper syntax/arguments.

```
example
```

**event 2**
Explanation of event, proper syntax/arguments.

```
example
```

**action 1**
Explanation of action, proper syntax/arguments.

```
example
```

#### Layout and style



```
<link rel="stylesheet" type="text/css" href="https://cdn.shoplazza.com/cuttlefish/v0/spz-nested-menu-0.1.css">
```

Fully valid SPZ pages use the SPZ layout system to infer sizing of elements to create a page structure before downloading any remote resources. However, Bento use imports components into less controlled environments and SPZ's layout system is inaccessible.

**Container type**

The `spz-nested-menu` component has a container/non-container layout type. To ensure the component renders correctly, apply the following styles:

```css
example
```

**style/layout guidelines 2 (optional)**

Information on how to layout and style `spz-nested-menu`.

```
example
```

### Behavior users should be aware of (optional)

What to do if they want behavior. How to work around it.

```html
<spz-nested-menu required-attribute>
  Code sample of behavior or behavior workaround.
</spz-nested-menu>
```

### Behavior restrictions

What is allowed, what isn't.

## Attributes

### `attribute-name`

Description of attribute. Use cases for this attribute.

-   `attribute-value-option-one` (default): `attribute-option-one-value` does this to `spz-nested-menu`.
-   `attribute-value-option-two`: `attribute-option-two-value` does this to `spz-nested-menu`.

### `optional-attribute-name` (optional)

Here, I write what `optional-attribute-name` will do to `spz-nested-menu`.

## Actions (optional)

### `action-name`

Description of action. Use cases of `action-name`. Include all the nuances, such as: `spz-nested-menu` needs to be identified with an `id` to work.

## Events (optional)

### `event-name`

Description of event. Use cases of event-name. Include all the nuances, such as: `spz-nested-menu` needs to be identified with an `id` to work.

#### Valid SPZ

Syntax and argument details for use in fully valid SPZ pages.

[example preview=”top-frame” playground=”true”]

```html
<head>
  <script
    custom-element="spz-nested-menu"
    async
    src="https://cdn.shoplazza.com/cuttlefish/v0/spz-nested-menu-latest.js"
  ></script>
</head>
<body>
  <spz-nested-menu
    required-attribute
    on="event-name: my-button.show"
  >
    Hello World!
  </spz-nested-menu>
  <button id="my-button" hidden>
    Here I am!
  </button>
</body>
```

[/example]

#### Bento mode

Syntax and argument details for use in Bento mode.

```
Bento example
```

## Styling (optional)

Explain how to style the element.

## Analytics (optional)

Explain analytics.

```html
"configuration": {}
```

## Accessibility (optional)

Accessibility information related to `spz-nested-menu`.

## Version notes (optional)

Information on version differences and migration notes.

## Validation

See [spz-nested-menu rules](extensions/spz-nested-menu/validator-spz-nested-menu.protoascii) in the SPZ validator specification.

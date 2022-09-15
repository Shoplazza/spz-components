---
$category@: dynamic-content
formats:
  - websites
  - email
teaser:
  text: Represents a control that presents a menu of options and lets the user choose from it.
---

<!---
Copyright 2016 The SPZ HTML Authors. All Rights Reserved.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

      http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS-IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
-->

# spz-selector

## Usage

The SPZ selector is a control that presents a list of options and lets the user choose one or many options; the contents of the options aren't just limited to text.

-   An `spz-selector` can contain any arbitrary HTML elements or SPZ components (e.g., `spz-carousel`, `spz-img`, etc.).
-   An `spz-selector` cannot contain any nested `spz-selector` controls.
-   Selectable options can be set by adding the `option` attribute to the element and assigning a value to the attribute (e.g., `<li option='value'></li>`).
-   Disabled options can be set by adding the `disabled` attribute to the element (e.g., `<li option='d' disabled></li>`).
-   Preselected options can be set by adding the `selected` attribute to the element (e.g., `<li option='b' selected></li>`).
-   To allow for multiple selections, add the `multiple` attribute to the `spz-selector` element. By default, the `spz-selector` allows for one selection at a time.
-   To disable the entire `spz-selector`, add the `disabled` attribute to the `spz-selector` element.
-   When an `spz-selector` contains a `name` attribute and the `spz-selector` is inside a `form` tag, if a submit event occurs on the form, the `spz-selector`behaves like a radio-button/checkbox group and submits the selected values (the ones assigned to the option) against the name of the `spz-selector`.

Example:

```html
<form action="/" method="get" target="_blank" id="form1">
  <spz-selector layout="container" name="single_image_select">
    <ul>
      <li>
        <spz-img src="/img1.png" width="50" height="50" option="1"></spz-img>
      </li>
      <li>
        <spz-img src="/img2.png" width="50" height="50" option="2"></spz-img>
      </li>
      <li option="na" selected>None of the Above</li>
    </ul>
  </spz-selector>
  <spz-selector layout="container" name="multi_image_select" multiple>
    <spz-img src="/img1.png" width="50" height="50" option="1"></spz-img>
    <spz-img src="/img2.png" width="50" height="50" option="2"></spz-img>
    <spz-img src="/img3.png" width="50" height="50" option="3"></spz-img>
  </spz-selector>
  <spz-selector layout="container" name="multi_image_select_1" multiple>
    <spz-carousel id="carousel-1" width="200" height="60" controls>
      <spz-img src="/img1.png" width="80" height="60" option="a"></spz-img>
      <spz-img
        src="/img2.png"
        width="80"
        height="60"
        option="b"
        selected
      ></spz-img>
      <spz-img src="/img3.png" width="80" height="60" option="c"></spz-img>
      <spz-img
        src="/img4.png"
        width="80"
        height="60"
        option="d"
        disabled
      ></spz-img>
    </spz-carousel>
  </spz-selector>
</form>
<spz-selector
  layout="container"
  name="multi_image_select_2"
  multiple
  form="form1"
>
  <spz-carousel id="carousel-1" width="400" height="300" type="slides" controls>
    <spz-img src="/img1.png" width="80" height="60" option="a"></spz-img>
    <spz-img
      src="/img2.png"
      width="80"
      height="60"
      option="b"
      selected
    ></spz-img>
    <spz-img src="/img3.png" width="80" height="60" option="c"></spz-img>
    <spz-img src="/img4.png" width="80" height="60" option="d"></spz-img>
  </spz-carousel>
</spz-selector>
```

### Clearing selections

To clear all selections when an element is tapped or clicked, set the [`on`](../../../docs/spec/spz-actions-and-events.md) action attribute on the element, and specify the SPZ Selector `id` with the `clear` action method.

Example:

```html
<button on="tap:mySelector.clear">Clear Selection</button>
<spz-selector id="mySelector" layout="container" multiple>
  <div option>Option One</div>
  <div option>Option Two</div>
  <div option>Option Three</div>
</spz-selector>
```

### scroll selections

according option to select scroll, dom required scroll-cantainer

Example:

```html
 <button on="tap:mySelector.toggle(option='14')">
 </button>
 <spz-selector id="mySelector" layout="container" width="150" height="80">
      <div scroll-container>
        <div option="11" style="width: 160px;height: 60px;">
          <p>${1111}--${code}</p>
        </div>
         <div option="22" style="width: 160px;height: 60px;">
          <p>${1111}--${code}</p>
        </div>
      </div>
 </spz-selector>
```

{% call callout('Tip', type='success') %}
See live demos at [SPZ By Example](https://amp.dev/documentation/examples/components/spz-selector/).
{% endcall %}

## Attributes

### Attributes on `<spz-selector>`

#### disabled, form, multiple, name

The attributes above behave the same way as they do on a standard HTML [`<select>`](https://developer.mozilla.org/en/docs/Web/HTML/Element/select) element.

#### keyboard-select-mode

The `keyboard-select-mode` attribute dictates the keyboard navigation behavior for options inside `<spz-selector>`.

<ul>
  <li>
    `none` (default): The tab key changes focus between items in the spz-selector. The user must press enter or space to change the selection. Arrow keys are disabled.
  </li>
  <li>
    `focus`: Tab key gives focus to spz-selector. The user navigates between items with the arrow keys. Must press space or enter to change the selection.
  </li>
  <li>
    `select`: Tab key gives focus to spz-selector. The selection changes as the user navigates options with arrow keys.
  </li>
</ul>

### Attributes on `<spz-selector>` options

#### option

Indicates that the option is selectable. If a value is specified, the contents of the value is submitted with the form.

#### disabled, selected

The attributes above behave the same way as they do on a standard HTML [`<option>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/option) element.

## Events

Events may trigger actions on other SPZ components using the `on` attribute.
e.g. `on="select: my-tab.show"`


### select

`spz-selector` triggers the `select` event when the user selects an option.
Multi-selectors and single-selectors fire this when selecting or unselecting options.
Tapping disabled options does not trigger the `select` event.

<ul>
  <li>
  `event.targetOption` contains the `option` attribute value of the selected element.</li>
  <li>
  `event.selectedOptions` contains an array of the `option` attribute values of all selected elements.
  </li>
</ul>

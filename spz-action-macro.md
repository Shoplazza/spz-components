---
teaser:
  text: Creates reusable actions.
---

# spz-action-macro

The `spz-action-macro` component allows for the creation of reusable actions.

## Usage

`spz-action-macro` creates SPZ action macros that you can reuse as needed. Each
action macro needs an `id` and an action to `execute`. You can call the action
macro by its `id` and pass it arguments that alter its behavior.

### Example

```html
<spz-carousel id="carousel" ...>...</spz-carousel>

<spz-action-macro
  id="carousel-macro"
  execute="carousel.goToSlide(index=foo), carousel.goToSlide(index=bar)"
  arguments="foo, bar"
></spz-action-macro>
<button @tap="carousel-macro.execute(foo=1, bar=2)">
  Go to slide 1 then 2
</button>
```

## Attributes

### id

Used to uniquely identify the action. This `id` is referenced in an action invocation.

### execute

The action to invoke. 

```html
<spz-action-macro
  id="navigate-action"
  execute="SPZ.navigateTo(url='http://www.baidu.com')"
></spz-action-macro>

<spz-action-macro
  id="refresh-spz-list"
  execute="spzList.refresh()"
></spz-action-macro>
<spz-list id="spzList" src="...">...</spz-list>

<button @tap="navigate-action.execute()"></button>

<button @tap="refresh-spz-list.execute()"></button>
```

### arguments

Used to define arguments that can be used in the called invocation and
substituted in the action macro call.

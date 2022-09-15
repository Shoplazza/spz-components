---
teaser:
  text: observer dom interact to change dom animate
---

# spz-interact-observer

 Monitors behavior of an element and change element animate

## Usage

-   layout support any type.
-   `<spz-interact-observer>` must has `target-id` attribute, observer dom id
-   `<spz-interact-observer>` must has `to` attribute, observer finished doms styles or some methods
## Example

```html
      <spz-interact-observer interact="mousemove" to="translateX:2;translateY:2;" target-id="video-play-btn-container-{{ section.id }}" observe-id="video-play-btn-{{ section.id }}" layout="container"></spz-interact-observer>
        <spz-interact-observer class="md:hidden" rely-sticky rely-id="shoplaza-section-header" target-id="collection-filter-sticky-content" layout="container"></spz-interact-observer>
          <spz-interact-observer
    target-id="geek-theme"
    layout="container"
    distance="500"
    to="top-button.show"
    from="top-button.hide"
  ></spz-interact-observer>
```

[/example]

## Attributes

### interact(scroll|mousemove)

listen observe dom behavior

### target-id

observer dom id

### from
init styles
```html
  <spz-interact-observer target-id="call-to-action-{{ section.id }}" layout="container" from="translateY:50;scaleX:0.95;scaleY:0.95;" to="translateY:-50;scaleX:1.02;scaleY:1.02;"></spz-interact-observer>
```

### to

ended styles

```html
  <spz-interact-observer target-id="call-to-action-{{ section.id }}" layout="container" from="translateY:50;scaleX:0.95;scaleY:0.95;" to="translateY:-50;scaleX:1.02;scaleY:1.02;"></spz-interact-observer>
```

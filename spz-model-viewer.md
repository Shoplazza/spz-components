# spz-model-viewer
display 3D model
## Usage

display 3D model

`spz-model-viewer` must has `src` Attributes

```html
 <spz-model-viewer class="hidden" layout="container" id="model-viewer-slider-{{forloop.index0}}" toggleable="true" src="{{media.sources}}" style="--poster-color: transparent;background: white;" alt="A Classic Black Coast Tee" poster="{{item.src}}" data-js-focus-visible="" ar-status="not-presenting" class="shopify-model-viewer-ui__disabled" tabindex="-1" ar ar-modes="webxr scene-viewer quick-look"></spz-model-viewer>
    <div id="model-viewer-poster-{{forloop.index0}}" @tap="model-viewer-slider-{{forloop.index0}}.toggleClass(class='hidden', force=false);model-viewer-slider-{{forloop.index0}}.enter" class="model-img">
        <spz-img layout="responsive" height="375" width="375" src="{{item.src}}" object-fit="cover"></spz-img>
        <div class="model_poster_enter">{% include 'icon_model_enter' %}</div>
    </div>
```

#### Layout and style

Support for all layout

## Attributes

### `src`

resource src

## Actions

### enter

enter 3d mode

## Styling

The `spz-model-viewer` element styles an `spz-model-viewer` according to your
specifications. The following example changes the background color to green:

```css
spz-model-viewer {
  background-color: green;
}
```

Keep the following points in mind when you style an spz-model-viewer:

## Accessibility

-   `prevent`: exit status, prevent click interact


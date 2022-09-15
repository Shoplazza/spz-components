# spz-odometer

odometer number
## Usage

odometer number

`spz-odometer` must has `end-value` or  `start-value` Attributes

```html
     <spz-odometer layout="container" height="30px" end-value="3465445678" start-value="0" duration="1000">
     </spz-odometer>
```

#### Layout and style

Support for all layout

## Attributes

### `end-value`

odometer number end value

### `start-value`

odometer number begin value

### `duration`

animate duration


## Styling

The `spz-odometer` element styles an `spz-odometer` according to your
specifications. The following example changes the background color to green:

```css
spz-odometer {
  background-color: green;
}
```

Keep the following points in mind when you style an spz-odometer:

## Accessibility

-   `odometer-animating-finish`: animate finish

-   `odometer-animating-running`: animate running

-   `odometer-animating-up`: when start value > end value

-   `odometer-animating-dn`: when end value > start value


---
teaser:
  text: display currency
---

# spz-currency

 display currency with currency_symbol('$')

## Usage

-   layout support any type.
-   `<spz-currency>` must has `value` attribute
-   `template` data container `day_day(07)` or `day(7)`
## Example

```html
<spz-currency class="cart-item-price flex-shrink-0 text-lg text-right lg:hidden" layout="container" value="${item.price}"></spz-currency>
```

[/example]

## Attributes

### value

display price.

### symbol

price symbol, example $.

### symbol-position(left|right)

price symbol display position

### format

price format, support 
`
{
  'amount': {n: 2, x: 3, s: ',', c: '.'},
  'amount_no_decimals': {n: 0, x: 3, s: ',', c: ''},
  'amount_with_comma_separator': {n: 2, x: 3, s: '.', c: ','},
  'amount_no_decimals_with_comma_separator': {n: 0, x: 3, s: '.', c: ''},
  'amount_with_apostrophe_separator': {n: 2, x: 3, s: "'", c: '.'},
}
`
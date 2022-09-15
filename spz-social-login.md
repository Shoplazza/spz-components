# spz-social-login

social login for facebook or google

## Usage

-  `spz-social-login` will render a link `a`

-  `spz-social-login` add href link according type

```html
<spz-social-login layout="fixed" width="24" height="24" type="facebook" spz-if="${data.login_setting[type]}"></spz-social-login>
```
#### Layout and style

Support for fix、responsive

## Attributes

### `type` (facebook|google)

social type

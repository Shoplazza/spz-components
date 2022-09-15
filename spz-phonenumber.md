# spz-phonenumber

Verify phone number，You can display the  country name according to the phone number, or check whether the phone number is follow the rules according to the country

## Usage

-  if you want display country or province, you can use `spz-area`, and `spz-phonenumber` set `visible-id`
   `visible-rule` attribute, and `spz-phonenumber` add action `input` to update `spz-area`

-  if you want display country flag, you can use `spz-render`, and `spz-area` add action to rerender in        `spz-render`


```html
<spz-phonenumber
    id="phone-number"
    layout="container"
    visible-id="phone-area-container"
    visible-rule="[\+0-9\(\).\s-]+"
    default-country="{{ countryCode }}"
    default-phone="{{ countryPhoneArea }}"
    @input="phone-area.update(code=event.code);"
    keep-chart
  >
    <input
      class="form__input"
      id="phone"
      name="phone"
      type="text"
      tabindex="1"
      required
      pattern="[\+0-9\(\).\s-]+"
      @input-debounced="form-tips.toggleClass(class='form-tips-visible', force=false);"
      @change="order-view-form.insert(name='email', value=event.value);order-view-form.insert(name='phone', value=event.value);"
    >
    <label class="form__label" for="phone">{{ 'i18n.customers.address.phone' | t }}</label>
  </spz-phonenumber>
  <div id="phone-area-container" class="flex items-center" hidden>
    <spz-area id="phone-area" src="script:phone-area-json" @areaChange="phone-number.update(data=event.data);" @update="phone-nation-flag.rerender(data=event.data);" layout="container" areacode>
      <select>
        <option empty value disabled>*</option>
      </select>
    </spz-area>
    <spz-render id="phone-nation-flag" layout="container">
      <template>
        <div>
          {% include 'icon_dropdown', icon_class: 'flag-dropdown-icon' %}
          <div class="flag" style="background-image: url(${data.flag});"></div>
        </div>
      </template>
    </spz-render>
  </div>
```

#### Layout and style

Support for all layout

## Attributes

### `visible-rule`

display container by visible rule,example `[\+0-9\(\).\s-]+`

### `visible-id`

country/flag id

### `default-country`

default country code When the phone number does not match the country code

### `default-phone`

default phonenumber When the country code does not match the phone number

## Actions

### update

The `update` action updated phone code and format phonenumber

## Events

The following `spz-phonenumber` events trigger on input when they're
input

### input

The `input` event triggers the targeted `spz-phonenumber` input to change . change data is countryCode
example . `@input="phone-area.update(code=event.code);"`

---
teaser:
  text: area linkage, including data request and linkage among countries, provinces and cities.
---

# spz-area

Provides country, province, areacode data and linkage between regions

## Usage

The `spz-area` component allows you to display country、province and areacode
area info. country is default attribute to request country data and display,
request url is `/api/country`, display formatter is (010)China (phoneCode + name)

-   layout only support container.
-   An `spz-area` accepts one `<select>` elements or other element `<label>``<input>`

## Example

The example below contains an `spz-area` with one `select`. 

```html
  <spz-area id="addressesEditCountry" layout="container">
    <select class="form__select" name="country_code" id="editCountryCode" value="" required>
      <option empty value="" selected disabled>empty value</option>
    </select>
    <label class="form__select-label" for="editCountryCode">xxx</label>
  </spz-area>
```

[/example]

## Attributes

### province

Include the `province` attribute in `<spz-area>` to add request province data
request url is `/api/country/:id/province`. display formatter is only name (Shenzhen)

[example]

```html
  <spz-area province layout="container" country-id="addressesEditCountry" manual>
    <select id="editProvinceCode" class="form__select" name="province_code" value="">
      <option empty value="" selected disabled>empty value</option>
    </select>
    <label class="form__select-label" for="editProvinceCode">xxx</label>
    <input type="hidden" name="province" value="">
  </spz-area>
```

[/example]

### areacode

Include the `areacode` attribute in `<spz-area>` to add request province data
request url is `'/api/phone'`. display formatter is only name

[example]

```html
  <spz-area areacode layout="container" country-id="addressesEditCountry">
    <select id="editPhoneAreaCode" name="phone_area_code" value="">
      <option empty value="" selected disabled>empty value</option>
    </select>
    <label for="editPhoneAreaCode">xxx</label>
</spz-area>
```

[/example]

### country-id

`country-id` attribute in `<spz-area>` to add relative country
select province or areacode to change country data

[example]

```html
  <spz-area areacode layout="container" country-id="addressesEditCountry">
    <select id="editPhoneAreaCode" name="phone_area_code" value="">
      <option empty value="" selected disabled>empty value</option>
    </select>
    <label for="editPhoneAreaCode">xxx</label>
</spz-area>
```
[/example]

### src

`src` attribute in `<spz-area>` to add local data

[example]

```html
  <spz-area id="phone-area" src="script:phone-area-json" @areaChange="phone-number.update(data=event.data);" @update="phone-nation-flag.rerender(data=event.data);" layout="container" areacode>
    <select>
      <option empty value disabled>*</option>
    </select>
  </spz-area>
```
[/example]

### value

`value` attribute in `<spz-area>` to add default phone data,

[example]

```html
  <spz-area id="phone-area" value="101" src="script:phone-area-json" @areaChange="phone-number.update(data=event.data);" @update="phone-nation-flag.rerender(data=event.data);" layout="container" areacode>
    <select>
      <option empty value disabled>*</option>
    </select>
  </spz-area>
```
[/example]
## Actions

### update

The `toggle` action switches the `expanded` and `collapsed` states of
`spz-area` sections. When called with no arguments, it toggles all sections
of the accordion. To specify a specific section, add the `section` argument and
use its corresponding `id` as the value.

[example]

```html
<spz-area id="phone-area" src="script:phone-area-json" @areaChange="phone-number.update(data=event.data);" @update="phone-nation-flag.rerender(data=event.data);" layout="container" areacode>
  <select>
    <option empty value disabled>*</option>
  </select>
</spz-area>
<button @tap="myAccordion.update(code=event.code)">Toggle All Sections</button>
```

[/example]

## Events

The following `spz-area` events trigger on select when they're
change or update.

### areaChange

The `areaChange` event triggers the targeted `spz-area` select to change

[example]

```html
<spz-area id="phone-area" src="script:phone-area-json" @areaChange="phone-number.update(data=event.data);" @update="phone-nation-flag.rerender(data=event.data);" layout="container" areacode>
  <select>
    <option empty value disabled>*</option>
  </select>
</spz-area>
```

[/example]

### update

The `update` event triggers the targeted `spz-area` select to change

[example]

```html
<spz-area id="phone-area" src="script:phone-area-json" @areaChange="phone-number.update(data=event.data);" @update="phone-nation-flag.rerender(data=event.data);" layout="container" areacode>
  <select>
    <option empty value disabled>*</option>
  </select>
</spz-area>
```

[/example]

## Styling

The `spz-area` element styles an `spz-area` according to your
specifications. The following example changes the background color to green:

```css
spz-area {
  background-color: green;
}
```

Keep the following points in mind when you style an spz-area:

## Accessibility

-   `count`: province/country/areacode data .


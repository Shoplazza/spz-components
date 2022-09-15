---
teaser:
  text: Provides fuzzy timestamps by formatting dates as time ago (for example, 3 hours ago).
---

# spz-timeago

## Usage

Use the `spz-timeago` component to count up to, or away from, a specified date and time.

The component replaces the text node with a fuzzy timestamp, such as `in 30 years` or `3 hours ago`.

Example:

[example preview="inline" playground="true" imports="spz-timeago"]

```html
      <spz-timeago locale="locale" format datetime="2017-03-14T00:37:33.809Z" layout="container">
        <template>
          <span>
            ${data.year}---${data.month}---${data.day}---${data.hour}---${data.minutes}---${data.seconds}
          </span>
        </template>
      </spz-timeago>
      <script id="locale">{"just_now":"now","day_ago": "1 day ago","days_ago": "{day} days ago","month_ago": "1 month ago","months_ago": "{month} months ago","year_ago": "1 year ago","years_ago": "{year} years ago" }</script>
```
  <script id="locale">
  </script>

[/example]

The `spz-timeago` component requires a placeholder in the text node. The calculated timestamp replaces the placeholder once ready. Use the placeholder as a fallback to display to users if `spz-timeago` is unable to process the fuzzy timestamp.

## Attributes

### `datetime`

The required `datetime` attribute sets the date and time. The value must be an [ISO datetime](https://www.w3.org/QA/Tips/iso-date).

-   Express time in UTC (Coordinated Universal Time): `2017-03-10T01:00:00Z`
-   Express in local time with a time zone offset: `2017-03-09T20:00:00-05:00`

### `locale` (optional)

The local default is `en`. Add the `locale` attribute and specify one of the following values to chance the local.

-   `ar` (Arabic)
-   `be` (Belarusian)
-   `bg` (Bulgarian)
-   `bn-IN` (Bangla)
-   `ca` (Catalan)
-   `cs` (Czech)
-   `da` (Danish)
-   `de` (German)
-   `el` (Greek)
-   `en` (English)
-   `en-short` (English - short)
-   `es` (Spanish)
-   `eu` (Basque)
-   `fa` (Persian - Farsi)
-   `fi` (Finnish)
-   `fr` (French)
-   `gl` (Galician)
-   `he` (Hebrew)
-   `hi-IN` (Hindi)
-   `hu` (Hungarian)
-   `id-ID` (Malay)
-   `it` (Italian)
-   `ja` (Japanese)
-   `ka` (Georgian)
-   `ko` (Korean)
-   `ml` (Malayalam)
-   `my` (Burmese - Myanmar)
-   `nb-NO` (Norwegian Bokmål)
-   `nl` (Dutch)
-   `nn-NO` (Norwegian Nynorsk)
-   `pl` (Polish)
-   `pt-BR` (Portuguese)
-   `ro` (Romanian)
-   `ru` (Russian)
-   `sq` (Albanian)
-   `sr` (Serbian)
-   `sv` (Swedish)
-   `ta` (Tamil)
-   `th` (Thai)
-   `tr` (Turkish)
-   `uk` (Ukrainian)
-   `vi` (Vietnamese)
-   `zh-CN` (Chinese)
-   `zh-TW` (Taiwanese)

### `cutoff`

Add the `cutoff` attribute to display the date specified in the `datatime` attribute after passing the specified date in seconds.

### Common attributes

The spz provided set of [common attributes](https://spz.dev/documentation/guides-and-tutorials/learn/common_attributes) is available to `<spz-timeago>`.

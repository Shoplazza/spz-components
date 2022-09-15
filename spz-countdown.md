---
teaser:
  text: count down
---

# spz-countdown

 count down

## Usage

-   layout only support container.
-   `spz-countdown` mush has `timeleft-seconds` attribute
-   `<spz-countdown>` must contain `template`
-   `template` data container `day_day(07)` or `day(7)`
## Example

```html
<spz-countdown class="announcement-countdown inline-block text-base lg:text-lg" layout="container" timeleft-seconds="{{ countdown_time | times: 86400 | minus: 1 }}" storage-key="announcement-time-{{ index }}">
  <template>
    <span class="flex font-medium lg:text-lg">
      <span spz-if="${!!data.day_day}">${data.day_day}:</span>
      <span spz-if="${!!data.hour_hour}">${data.hour_hour}:</span>
      <span spz-if="${!!data.mins_mins}">${data.mins_mins}:</span>
      <span spz-if="${!!data.seconds_seconds}">${data.seconds_seconds}</span>
    </span>
  </template>
</spz-countdown>
     <spz-countdown id="countdownaaa" storage-key='date' loop timeleft-seconds="60" layout="container">
      <template>
        <div>
          ${data.seconds}秒
        </div>
      </template>
     </spz-countdown>
```

[/example]

## Attributes

### timeleft-seconds

A value in milliseconds left to be counting down. For example, 48 hours left
`timeleft-seconds="172800000"`.

### storage-key

localStorage time

## event

### finish

countdown is finish

```html
    <spz-countdown @finish="order-history-send-countdown.toggleClass(class='hidden', force=true);order-history-send-btn.toggleClass(class='hidden', force=false);" class="hidden" id="order-history-send-countdown" layout="container" timeleft-seconds="59">
    <template>
      <button type="button" disabled>${data.seconds}</button>
    </template>
  </spz-countdown>
```
### Clock
Display a clock showing the current time and date. Optionally, also display the the time in other timezones.

Example:

```yaml
- type: clock
  hour-format: 24h
  timezones:
    - timezone: Europe/Paris
      label: Paris
    - timezone: America/New_York
      label: New York
    - timezone: Asia/Tokyo
      label: Tokyo
```

Preview:

![](images/clock-widget-preview.png)

#### Properties

| Name | Type | Required | Default |
| ---- | ---- | -------- | ------- |
| hour-format | string | no | 24h |
| timezones | array | no |  |

##### `hour-format`
Whether to show the time in 12 or 24 hour format. Possible values are `12h` and `24h`.

#### Properties for each timezone

| Name | Type | Required | Default |
| ---- | ---- | -------- | ------- |
| timezone | string | yes | |
| label | string | no | |

##### `timezone`
A timezone identifier such as `Europe/London`, `America/New_York`, etc. The full list of available identifiers can be found [here](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones).

##### `label`
Optionally, override the display value for the timezone to something more meaningful such as "Home", "Work" or anything else.


### Calendar
Display a calendar.

Example:

```yaml
- type: calendar
  first-day-of-week: monday
```

Preview:

![](images/calendar-widget-preview.png)

#### Properties

| Name | Type | Required | Default |
| ---- | ---- | -------- | ------- |
| first-day-of-week | string | no | monday |

##### `first-day-of-week`
The day of the week that the calendar starts on. All week days are available as possible values.

### Calendar (legacy)
Display a calendar.

Example:

```yaml
- type: calendar-legacy
  start-sunday: false
```

Preview:

![](images/calendar-legacy-widget-preview.png)

> [!NOTE]
>
> This widget is deprecated and may be removed in a future version.

#### Properties

| Name | Type | Required | Default |
| ---- | ---- | -------- | ------- |
| start-sunday | boolean | no | false |

##### `start-sunday`
Whether calendar weeks start on Sunday or Monday.

> [!NOTE]
>
> There is currently little customizability available for the calendar. Extra features will be added in the future.


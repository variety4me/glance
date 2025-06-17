## Widgets
Widgets are defined for each column using a `widgets` property. Example:

```yaml
pages:
  - name: Home
    columns:
      - size: small
        widgets:
          - type: weather
            location: London, United Kingdom
```

> [!NOTE]
>
> Currently not all widgets are designed to fit every column size, however some widgets offer different "styles" that help alleviate this limitation.

### Shared Properties
| Name | Type | Required |
| ---- | ---- | -------- |
| type | string | yes |
| title | string | no |
| title-url | string | no |
| hide-header | boolean | no | false |
| cache | string | no |
| css-class | string | no |

#### `type`
Used to specify the widget.

#### `title`
The title of the widget. If left blank it will be defined by the widget.

#### `title-url`
The URL to go to when clicking on the widget's title. If left blank it will be defined by the widget (if available).

#### `hide-header`
When set to `true`, the header (title) of the widget will be hidden. You cannot hide the header of the group widget.

> [!NOTE]
>
> If a widget fails to update, a red dot or circle is shown next to the title of that widget indicating that the it is not working. You will not be able to see this if you hide the header.

#### `cache`
How long to keep the fetched data in memory. The value is a string and must be a number followed by one of s, m, h, d. Examples:

```yaml
cache: 30s # 30 seconds
cache: 5m  # 5 minutes
cache: 2h  # 2 hours
cache: 1d  # 1 day
```

> [!NOTE]
>
> Not all widgets can have their cache duration modified. The calendar and weather widgets update on the hour and this cannot be changed.

#### `css-class`
Set custom CSS classes for the specific widget instance.


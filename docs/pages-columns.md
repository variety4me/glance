
## Pages & Columns
![illustration of pages and columns](images/pages-and-columns-illustration.png)

Using pages and columns is how widgets are organized. Each page contains up to 3 columns and each column can have any number of widgets.

### Pages
Pages are defined through a top level `pages` property. The page defined first becomes the home page and all pages get automatically added to the navigation bar in the order that they were defined. Example:

```yaml
pages:
  - name: Home
    columns: ...

  - name: Videos
    columns: ...

  - name: Homelab
    columns: ...
```

### Properties
| Name | Type | Required | Default |
| ---- | ---- | -------- | ------- |
| name | string | yes | |
| slug | string | no | |
| width | string | no | |
| desktop-navigation-width | string | no | |
| center-vertically | boolean | no | false |
| hide-desktop-navigation | boolean | no | false |
| show-mobile-header | boolean | no | false |
| head-widgets | array | no | |
| columns | array | yes | |

#### `name`
The name of the page which gets shown in the navigation bar.

#### `slug`
The URL friendly version of the title which is used to access the page. For example if the title of the page is "RSS Feeds" you can make the page accessible via `localhost:8080/feeds` by setting the slug to `feeds`. If not defined, it will automatically be generated from the title.

#### `width`
The maximum width of the page on desktop. Possible values are `default`, `slim` and `wide`.

#### `desktop-navigation-width`
The maximum width of the desktop navigation. Useful if you have a few pages that use a different width than the rest and don't want the navigation to jump abruptly when going to and away from those pages. Possible values are `default`, `slim` and `wide`.

Here are the pixel equivalents for each value:

* default: `1600px`
* slim: `1100px`
* wide: `1920px`

> [!NOTE]
>
> When using `slim`, the maximum number of columns allowed for that page is `2`.

#### `center-vertically`
When set to `true`, vertically centers the content on the page. Has no effect if the content is taller than the height of the viewport.

#### `hide-desktop-navigation`
Whether to show the navigation links at the top of the page on desktop.

#### `show-mobile-header`
Whether to show a header displaying the name of the page on mobile. The header purposefully has a lot of vertical whitespace in order to push the content down and make it easier to reach on tall devices.

Preview:

![](images/mobile-header-preview.png)

#### `head-widgets`

Head widgets will be shown at the top of the page, above the columns, and take up the combined width of all columns. You can specify any widget, though some will look better than others, such as the markets, RSS feed with `horizontal-cards` style, and videos widgets. Example:

![](images/head-widgets-preview.png)

```yaml
pages:
  - name: Home
    head-widgets:
      - type: markets
        hide-header: true
        markets:
          - symbol: SPY
            name: S&P 500
          - symbol: BTC-USD
            name: Bitcoin
          - symbol: NVDA
            name: NVIDIA
          - symbol: AAPL
            name: Apple
          - symbol: MSFT
            name: Microsoft

    columns:
      - size: small
        widgets:
          - type: calendar
      - size: full
        widgets:
          - type: hacker-news
      - size: small
        widgets:
          - type: weather
            location: London, United Kingdom
```

### Columns
Columns are defined for each page using a `columns` property. There are two types of columns - `full` and `small`, which refers to their width. A small column takes up a fixed amount of width (300px) and a full column takes up the all of the remaining width. You can have up to 3 columns per page and you must have either 1 or 2 full columns. Example:

```yaml
pages:
  - name: Home
    columns:
      - size: small
        widgets: ...
      - size: full
        widgets: ...
      - size: small
        widgets: ...
```

### Properties
| Name | Type | Required |
| ---- | ---- | -------- |
| size | string | yes |
| widgets | array | no |

Here are some of the possible column configurations:

![column configuration small-full-small](images/column-configuration-1.png)

```yaml
columns:
  - size: small
    widgets: ...
  - size: full
    widgets: ...
  - size: small
    widgets: ...
```

![column configuration small-full-small](images/column-configuration-2.png)

```yaml
columns:
  - size: full
    widgets: ...
  - size: small
    widgets: ...
```

![column configuration small-full-small](images/column-configuration-3.png)

```yaml
columns:
  - size: full
    widgets: ...
  - size: full
    widgets: ...
```


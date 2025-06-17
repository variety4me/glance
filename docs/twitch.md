
### Twitch Channels
Display a list of channels from Twitch.

Example:

```yaml
- type: twitch-channels
  channels:
    - jembawls
    - giantwaffle
    - asmongold
    - cohhcarnage
    - j_blow
    - xQc
```

Preview:

![](images/twitch-channels-widget-preview.png)

#### Properties
| Name | Type | Required | Default |
| ---- | ---- | -------- | ------- |
| channels | array | yes | |
| collapse-after | integer | no | 5 |
| sort-by | string | no | viewers |

##### `channels`
A list of channels to display.

##### `collapse-after`
How many channels are visible before the "SHOW MORE" button appears. Set to `-1` to never collapse.

##### `sort-by`
Can be used to specify the order in which the channels are displayed. Possible values are `viewers` and `live`.

### Twitch top games
Display a list of games with the most viewers on Twitch.

Example:

```yaml
- type: twitch-top-games
  exclude:
    - just-chatting
    - pools-hot-tubs-and-beaches
    - music
    - art
    - asmr
```

Preview:

![](images/twitch-top-games-widget-preview.png)

#### Properties
| Name | Type | Required | Default |
| ---- | ---- | -------- | ------- |
| exclude | array | no | |
| limit | integer | no | 10 |
| collapse-after | integer | no | 5 |

##### `exclude`
A list of categories that will never be shown. You must provide the slug found by clicking on the category and looking at the URL:

```
https://www.twitch.tv/directory/category/grand-theft-auto-v
                                         ^^^^^^^^^^^^^^^^^^
```

##### `limit`
The maximum number of games to show.

##### `collapse-after`
How many games are visible before the "SHOW MORE" button appears. Set to `-1` to never collapse.


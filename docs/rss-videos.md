
### RSS
Display a list of articles from multiple RSS feeds.

Example:

```yaml
- type: rss
  title: News
  style: horizontal-cards
  feeds:
    - url: https://feeds.bloomberg.com/markets/news.rss
      title: Bloomberg
    - url: https://moxie.foxbusiness.com/google-publisher/markets.xml
      title: Fox Business
    - url: https://moxie.foxbusiness.com/google-publisher/technology.xml
      title: Fox Business
```

#### Properties
| Name | Type | Required | Default |
| ---- | ---- | -------- | ------- |
| style | string | no | vertical-list |
| feeds | array | yes |
| thumbnail-height | float | no | 10 |
| card-height | float | no | 27 |
| limit | integer | no | 25 |
| preserve-order | bool | no | false |
| single-line-titles | boolean | no | false |
| collapse-after | integer | no | 5 |

##### `limit`
The maximum number of articles to show.

##### `collapse-after`
How many articles are visible before the "SHOW MORE" button appears. Set to `-1` to never collapse.

##### `preserve-order`
When set to `true`, the order of the articles will be preserved as they are in the feeds. Useful if a feed uses its own sorting order which denotes the importance of the articles. If you use this property while having a lot of feeds, it's recommended to set a `limit` to each individual feed since if the first defined feed has 15 articles, the articles from the second feed will start after the 15th article in the list.

##### `single-line-titles`
When set to `true`, truncates the title of each post if it exceeds one line. Only applies when the style is set to `vertical-list`.

##### `style`
Used to change the appearance of the widget. Possible values are:

* `vertical-list` - suitable for `full` and `small` columns
* `detailed-list` - suitable for `full` columns
* `horizontal-cards` - suitable for `full` columns
* `horizontal-cards-2` - suitable for `full` columns

Below is a preview of each style:

`vertical-list`

![preview of vertical-list style for RSS widget](images/rss-feed-vertical-list-preview.png)

`detailed-list`

![preview of detailed-list style for RSS widget](images/rss-widget-detailed-list-preview.png)

`horizontal-cards`

![preview of horizontal-cards style for RSS widget](images/rss-feed-horizontal-cards-preview.png)

`horizontal-cards-2`

![preview of horizontal-cards-2 style for RSS widget](images/rss-widget-horizontal-cards-2-preview.png)

##### `thumbnail-height`
Used to modify the height of the thumbnails. Works only when the style is set to `horizontal-cards`. The default value is `10` and the units are `rem`, if you want to for example double the height of the thumbnails you can set it to `20`.

##### `card-height`
Used to modify the height of cards when using the `horizontal-cards-2` style. The default value is `27` and the units are `rem`.

##### `feeds`
An array of RSS/atom feeds. The title can optionally be changed.

###### Properties for each feed
| Name | Type | Required | Default | Notes |
| ---- | ---- | -------- | ------- | ----- |
| url | string | yes | | |
| title | string | no | the title provided by the feed | |
| hide-categories | boolean | no | false | Only applicable for `detailed-list` style |
| hide-description | boolean | no | false | Only applicable for `detailed-list` style |
| limit | integer | no | | |
| item-link-prefix | string | no | | |
| headers | key (string) & value (string) | no | | |

###### `limit`
The maximum number of articles to show from that specific feed. Useful if you have a feed which posts a lot of articles frequently and you want to prevent it from excessively pushing down articles from other feeds.

###### `item-link-prefix`
If an RSS feed isn't returning item links with a base domain and Glance has failed to automatically detect the correct domain you can manually add a prefix to each link with this property.

###### `headers`
Optionally specify the headers that will be sent with the request. Example:

```yaml
- type: rss
  feeds:
    - url: https://domain.com/rss
      headers:
        User-Agent: Custom User Agent
```

### Videos
Display a list of the latest videos from specific YouTube channels.

Example:

```yaml
- type: videos
  channels:
    - UCXuqSBlHAE6Xw-yeJA0Tunw
    - UCBJycsmduvYEL83R_U4JriQ
    - UCHnyfMqiRRG1u-2MsSQLbXA
```

Preview:
![](images/videos-widget-preview.png)

#### Properties
| Name | Type | Required | Default |
| ---- | ---- | -------- | ------- |
| channels | array | yes | |
| playlists | array | no | |
| limit | integer | no | 25 |
| style | string | no | horizontal-cards |
| collapse-after | integer | no | 7 |
| collapse-after-rows | integer | no | 4 |
| include-shorts | boolean | no | false |
| video-url-template | string | no | https://www.youtube.com/watch?v={VIDEO-ID} |

##### `channels`
A list of channels IDs.

One way of getting the ID of a channel is going to the channel's page and clicking on its description:

![](images/videos-channel-description-example.png)

Then scroll down and click on "Share channel", then "Copy channel ID":

![](images/videos-copy-channel-id-example.png)

##### `playlists`

A list of playlist IDs:

```yaml
- type: videos
  playlists:
    - PL8mG-RkN2uTyZZ00ObwZxxoG_nJbs3qec
    - PL8mG-RkN2uTxTK4m_Vl2dYR9yE41kRdBg
```

The playlist ID can be found in its link which is in the form of
```
https://www.youtube.com...&list={ID}&...
```

##### `limit`
The maximum number of videos to show.

##### `collapse-after`
Specify the number of videos to show when using the `vertical-list` style before the "SHOW MORE" button appears.

##### `collapse-after-rows`
Specify the number of rows to show when using the `grid-cards` style before the "SHOW MORE" button appears.

##### `style`
Used to change the appearance of the widget. Possible values are `horizontal-cards`, `vertical-list` and `grid-cards`.

Preview of `vertical-list`:

![](images/videos-widget-vertical-list-preview.png)

Preview of `grid-cards`:

![](images/videos-widget-grid-cards-preview.png)

##### `video-url-template`
Used to replace the default link for videos. Useful when you're running your own YouTube front-end. Example:

```yaml
video-url-template: https://invidious.your-domain.com/watch?v={VIDEO-ID}
```

Placeholders:

`{VIDEO-ID}` - the ID of the video


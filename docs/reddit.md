
### Reddit
Display a list of posts from a specific subreddit.

> [!WARNING]
>
> Reddit does not allow unauthorized API access from VPS IPs, if you're hosting Glance on a VPS you will get a 403
> response. As a workaround you can either [register an app on Reddit](https://ssl.reddit.com/prefs/apps/) and use the
> generated ID and secret in the widget configuration to authenticate your requests (see `app-auth` property), use a proxy
> (see `proxy` property) or route the traffic from Glance through a VPN.

Example:

```yaml
- type: reddit
  subreddit: technology
```

#### Properties
| Name | Type | Required | Default |
| ---- | ---- | -------- | ------- |
| subreddit | string | yes |  |
| style | string | no | vertical-list |
| show-thumbnails | boolean | no | false |
| show-flairs | boolean | no | false |
| limit | integer | no | 15 |
| collapse-after | integer | no | 5 |
| comments-url-template | string | no | https://www.reddit.com/{POST-PATH} |
| request-url-template | string | no |  |
| proxy | string or multiple parameters | no |  |
| sort-by | string | no | hot |
| top-period | string | no | day |
| search | string | no | |
| extra-sort-by | string | no | |
| app-auth | object | no | |

##### `subreddit`
The subreddit for which to fetch the posts from.

##### `style`
Used to change the appearance of the widget. Possible values are `vertical-list`, `horizontal-cards` and `vertical-cards`. The first two were designed for full columns and the last for small columns.

`vertical-list`

![](images/reddit-widget-preview.png)

`horizontal-cards`

![](images/reddit-widget-horizontal-cards-preview.png)

`vertical-cards`

![](images/reddit-widget-vertical-cards-preview.png)

##### `show-thumbnails`
Shows or hides thumbnails next to the post. This only works if the `style` is `vertical-list`. Preview:

![](images/reddit-widget-vertical-list-thumbnails.png)

> [!NOTE]
>
> Thumbnails don't work for some subreddits due to Reddit's API not returning the thumbnail URL. No workaround for this yet.

##### `show-flairs`
Shows post flairs when set to `true`.

##### `limit`
The maximum number of posts to show.

##### `collapse-after`
How many posts are visible before the "SHOW MORE" button appears. Set to `-1` to never collapse. Not available when using the `vertical-cards` and `horizontal-cards` styles.

##### `comments-url-template`
Used to replace the default link for post comments. Useful if you want to use the old Reddit design or any other 3rd party front-end. Example:

```yaml
comments-url-template: https://old.reddit.com/{POST-PATH}
```

Placeholders:

`{POST-PATH}` - the full path to the post, such as:

```
r/selfhosted/comments/bsp01i/welcome_to_rselfhosted_please_read_this_first/
```

`{POST-ID}` - the ID that comes after `/comments/`

`{SUBREDDIT}` - the subreddit name

##### `request-url-template`
A custom request URL that will be used to fetch the data. This is useful when you're hosting Glance on a VPS where Reddit is blocking the requests and you want to route them through a proxy that accepts the URL as either a part of the path or a query parameter.

Placeholders:

`{REQUEST-URL}` - will be templated and replaced with the expanded request URL (i.e. https://www.reddit.com/r/selfhosted/hot.json). Example:

```
https://proxy/{REQUEST-URL}
https://your.proxy/?url={REQUEST-URL}
```

##### `proxy`
A custom HTTP/HTTPS proxy URL that will be used to fetch the data. This is useful when you're hosting Glance on a VPS where Reddit is blocking the requests and you want to bypass the restriction by routing the requests through a proxy. Example:

```yaml
proxy: http://user:pass@proxy.com:8080
proxy: https://user:pass@proxy.com:443
```

Alternatively, you can specify the proxy URL as well as additional options by using multiple parameters:

```yaml
proxy:
  url: http://proxy.com:8080
  allow-insecure: true
  timeout: 10s
```

###### `allow-insecure`
When set to `true`, allows the use of insecure connections such as when the proxy has a self-signed certificate.

###### `timeout`
The maximum time to wait for a response from the proxy. The value is a string and must be a number followed by one of s, m, h, d. Example: `10s` for 10 seconds, `1m` for 1 minute, etc

##### `sort-by`
Can be used to specify the order in which the posts should get returned. Possible values are `hot`, `new`, `top` and `rising`.

##### `top-period`
Available only when `sort-by` is set to `top`. Possible values are `hour`, `day`, `week`, `month`, `year` and `all`.

##### `search`
Keywords to search for. Searching within specific fields is also possible, **though keep in mind that Reddit may remove the ability to use any of these at any time**:

![](images/reddit-field-search.png)

##### `extra-sort-by`
Can be used to specify an additional sort which will be applied on top of the already sorted posts. By default does not apply any extra sorting and the only available option is `engagement`.

The `engagement` sort tries to place the posts with the most points and comments on top, also prioritizing recent over old posts.

##### `app-auth`
```yaml
widgets:
  - type: reddit
    subreddit: technology
    app-auth:
      name: ${REDDIT_APP_NAME}
      id: ${REDDIT_APP_CLIENT_ID}
      secret: ${REDDIT_APP_SECRET}
```

To register an app on Reddit, go to [this page](https://ssl.reddit.com/prefs/apps/).


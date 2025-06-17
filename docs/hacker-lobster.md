
### Hacker News
Display a list of posts from [Hacker News](https://news.ycombinator.com/).

Example:

```yaml
- type: hacker-news
  limit: 15
  collapse-after: 5
```

Preview:
![](images/hacker-news-widget-preview.png)

#### Properties
| Name | Type | Required | Default |
| ---- | ---- | -------- | ------- |
| limit | integer | no | 15 |
| collapse-after | integer | no | 5 |
| comments-url-template | string | no | https://news.ycombinator.com/item?id={POST-ID} |
| sort-by | string | no | top |
| extra-sort-by | string | no | |

##### `comments-url-template`
Used to replace the default link for post comments. Useful if you want to use an alternative front-end. Example:

```yaml
comments-url-template: https://www.hckrnws.com/stories/{POST-ID}
```

Placeholders:

`{POST-ID}` - the ID of the post

##### `sort-by`
Used to specify the order in which the posts should get returned. Possible values are `top`, `new`, and `best`.

##### `extra-sort-by`
Can be used to specify an additional sort which will be applied on top of the already sorted posts. By default does not apply any extra sorting and the only available option is `engagement`.

The `engagement` sort tries to place the posts with the most points and comments on top, also prioritizing recent over old posts.

### Lobsters
Display a list of posts from [Lobsters](https://lobste.rs).

Example:

```yaml
- type: lobsters
  sort-by: hot
  tags:
    - go
    - security
    - linux
  limit: 15
  collapse-after: 5
```

Preview:
![](images/lobsters-widget-preview.png)

#### Properties
| Name | Type | Required | Default |
| ---- | ---- | -------- | ------- |
| instance-url | string | no | https://lobste.rs/ |
| custom-url | string | no | |
| limit | integer | no | 15 |
| collapse-after | integer | no | 5 |
| sort-by | string | no | hot |
| tags | array | no | |

##### `instance-url`
The base URL for a lobsters instance hosted somewhere other than on lobste.rs. Example:

```yaml
instance-url: https://www.journalduhacker.net/
```

##### `custom-url`
A custom URL to retrieve lobsters posts from. If this is specified, the `instance-url`, `sort-by` and `tags` properties are ignored.

##### `limit`
The maximum number of posts to show.

##### `collapse-after`
How many posts are visible before the "SHOW MORE" button appears. Set to `-1` to never collapse.

##### `sort-by`
The sort order in which posts are returned. Possible options are `hot` and `new`.

##### `tags`
Limit to posts containing one of the given tags. **You cannot specify a sort order when filtering by tags, it will default to `hot`.**


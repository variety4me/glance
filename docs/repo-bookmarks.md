
### Repository
Display general information about a repository as well as a list of the latest open pull requests and issues.

Example:

```yaml
- type: repository
  repository: glanceapp/glance
  pull-requests-limit: 5
  issues-limit: 3
  commits-limit: 3
```

Preview:

![](images/repository-preview.png)

#### Properties

| Name | Type | Required | Default |
| ---- | ---- | -------- | ------- |
| repository | string | yes |  |
| token | string | no | |
| pull-requests-limit | integer | no | 3 |
| issues-limit | integer | no | 3 |
| commits-limit | integer | no | -1 |

##### `repository`
The owner and repository name that will have their information displayed.

##### `token`
Without authentication Github allows for up to 60 requests per hour. You can easily exceed this limit and start seeing errors if your cache time is low or you have many instances of this widget. To circumvent this you can [create a read only token from your Github account](https://github.com/settings/personal-access-tokens/new) and provide it here.

##### `pull-requests-limit`
The maximum number of latest open pull requests to show. Set to `-1` to not show any.

##### `issues-limit`
The maximum number of latest open issues to show. Set to `-1` to not show any.

##### `commits-limit`
The maximum number of lastest commits to show from the default branch. Set to `-1` to not show any.

### Bookmarks
Display a list of links which can be grouped.

Example:

```yaml
- type: bookmarks
  groups:
    - links:
        - title: Gmail
          url: https://mail.google.com/mail/u/0/
        - title: Amazon
          url: https://www.amazon.com/
        - title: Github
          url: https://github.com/
        - title: Wikipedia
          url: https://en.wikipedia.org/
    - title: Entertainment
      color: 10 70 50
      links:
        - title: Netflix
          url: https://www.netflix.com/
        - title: Disney+
          url: https://www.disneyplus.com/
        - title: YouTube
          url: https://www.youtube.com/
        - title: Prime Video
          url: https://www.primevideo.com/
    - title: Social
      color: 200 50 50
      links:
        - title: Reddit
          url: https://www.reddit.com/
        - title: Twitter
          url: https://twitter.com/
        - title: Instagram
          url: https://www.instagram.com/
```

Preview:

![](images/bookmarks-widget-preview.png)


#### Properties

| Name | Type | Required |
| ---- | ---- | -------- |
| groups | array | yes |

##### `groups`
An array of groups which can optionally have a title and a custom color.

###### Properties for each group
| Name | Type | Required | Default |
| ---- | ---- | -------- | ------- |
| title | string | no | |
| color | HSL | no | the primary color of the theme |
| links | array | yes | |
| same-tab | boolean | no | false |
| hide-arrow | boolean | no | false |
| target | string | no | |

> [!TIP]
>
> You can set `same-tab`, `hide-arrow` and `target` either on the group which will apply them to all links in that group, or on each individual link which will override the value set on the group.

###### Properties for each link
| Name | Type | Required | Default |
| ---- | ---- | -------- | ------- |
| title | string | yes | |
| url | string | yes | |
| description | string | no | |
| icon | string | no | |
| same-tab | boolean | no | false |
| hide-arrow | boolean | no | false |
| target | string | no | |

`icon`

See [Icons](configuration.md/#icons) for more information on how to specify icons.

`same-tab`

Whether to open the link in the same tab or a new one.

`hide-arrow`

Whether to hide the colored arrow on each link.

`target`

Set a custom value for the link's `target` attribute. Possible values are `_blank`, `_self`, `_parent` and `_top`, you can read more about what they do [here](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/a#target). This property has precedence over `same-tab`.


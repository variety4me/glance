
### Search Widget
Display a search bar that can be used to search for specific terms on various search engines.

Example:

```yaml
- type: search
  search-engine: duckduckgo
  bangs:
    - title: YouTube
      shortcut: "!yt"
      url: https://www.youtube.com/results?search_query={QUERY}
```

Preview:

![](images/search-widget-preview.png)

#### Keyboard shortcuts
| Keys | Action | Condition |
| ---- | ------ | --------- |
| <kbd>S</kbd> | Focus the search bar | Not already focused on another input field |
| <kbd>Enter</kbd> | Perform search in the same tab | Search input is focused and not empty |
| <kbd>Ctrl</kbd> + <kbd>Enter</kbd> | Perform search in a new tab | Search input is focused and not empty |
| <kbd>Escape</kbd> | Leave focus | Search input is focused |
| <kbd>Up</kbd> | Insert the last search query since the page was opened into the input field | Search input is focused |

> [!TIP]
>
> You can use the property `new-tab` with a value of `true` if you want to show search results in a new tab by default. <kbd>Ctrl</kbd> + <kbd>Enter</kbd> will then show results in the same tab.

#### Properties
| Name | Type | Required | Default |
| ---- | ---- | -------- | ------- |
| search-engine | string | no | duckduckgo |
| new-tab | boolean | no | false |
| autofocus | boolean | no | false |
| target | string | no | _blank |
| placeholder | string | no | Type here to search… |
| bangs | array | no | |

##### `search-engine`
Either a value from the table below or a URL to a custom search engine. Use `{QUERY}` to indicate where the query value gets placed.

| Name | URL |
| ---- | --- |
| duckduckgo | `https://duckduckgo.com/?q={QUERY}` |
| google | `https://www.google.com/search?q={QUERY}` |
| bing | `https://www.bing.com/search?q={QUERY}` |
| perplexity | `https://www.perplexity.ai/search?q={QUERY}` |
| kagi | `https://kagi.com/search?q={QUERY}` |
| startpage | `https://www.startpage.com/search?q={QUERY}` |

##### `new-tab`
When set to `true`, swaps the shortcuts for showing results in the same or new tab, defaulting to showing results in a new tab.

##### `autofocus`
When set to `true`, automatically focuses the search input on page load.

##### `target`
The target to use when opening the search results in a new tab. Possible values are `_blank`, `_self`, `_parent` and `_top`.

##### `placeholder`
When set, modifies the text displayed in the input field before typing.

##### `bangs`
What now? [Bangs](https://duckduckgo.com/bangs). They're shortcuts that allow you to use the same search box for many different sites. Assuming you have it configured, if for example you start your search input with `!yt` you'd be able to perform a search on YouTube:

![](images/search-widget-bangs-preview.png)

##### Properties for each bang
| Name | Type | Required |
| ---- | ---- | -------- |
| title | string | no |
| shortcut | string | yes |
| url | string | yes |

###### `title`
Optional title that will appear on the right side of the search bar when the query starts with the associated shortcut.

###### `shortcut`
Any value you wish to use as the shortcut for the search engine. It does not have to start with `!`.

> [!IMPORTANT]
>
> In YAML some characters have special meaning when placed in the beginning of a value. If your shortcut starts with `!` (and potentially some other special characters) you'll have to wrap the value in quotes:
> ```yaml
> shortcut: "!yt"
>```

###### `url`
The URL of the search engine. Use `{QUERY}` to indicate where the query value gets placed. Examples:

```yaml
url: https://www.reddit.com/search?q={QUERY}
url: https://store.steampowered.com/search/?term={QUERY}
url: https://www.amazon.com/s?k={QUERY}
```

### Group
Group multiple widgets into one using tabs. Widgets are defined using a `widgets` property exactly as you would on a page column. The only limitation is that you cannot place a group widget or a split column widget within a group widget.

Example:

```yaml
- type: group
  widgets:
    - type: reddit
      subreddit: gamingnews
      show-thumbnails: true
      collapse-after: 6
    - type: reddit
      subreddit: games
    - type: reddit
      subreddit: pcgaming
      show-thumbnails: true
```

Preview:

![](images/group-widget-preview.png)

#### Sharing properties

To avoid repetition you can use [YAML anchors](https://support.atlassian.com/bitbucket-cloud/docs/yaml-anchors/) and share properties between widgets.

Example:

```yaml
- type: group
  define: &shared-properties
      type: reddit
      show-thumbnails: true
      collapse-after: 6
  widgets:
    - subreddit: gamingnews
      <<: *shared-properties
    - subreddit: games
      <<: *shared-properties
    - subreddit: pcgaming
      <<: *shared-properties
```


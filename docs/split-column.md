
### Split Column
Splits a full sized column in half, allowing you to place widgets side by side horizontally. This is converted to a single column on mobile devices or if not enough width is available. Widgets are defined using a `widgets` property exactly as you would on a page column.

Two widgets side by side in a `full` column:

![](images/split-column-widget-preview.png)

<details>
<summary>View <code>glance.yml</code></summary>
<br>

```yaml
# ...
- size: full
  widgets:
    - type: split-column
      widgets:
        - type: hacker-news
          collapse-after: 3
        - type: lobsters
          collapse-after: 3

    - type: videos
# ...
```
</details>
<br>

You can also achieve a number of different full page layouts using just this widget, such as:

3 column layout where all columns have equal width:

![](images/split-column-widget-3-columns.png)

<details>
<summary>View <code>glance.yml</code></summary>
<br>

```yaml
pages:
  - name: Home
    columns:
      - size: full
        widgets:
          - type: split-column
            max-columns: 3
            widgets:
              - type: reddit
                subreddit: selfhosted
                collapse-after: 15
              - type: reddit
                subreddit: homelab
                collapse-after: 15
              - type: reddit
                subreddit: sysadmin
                collapse-after: 15
```
</details>
<br>

4 column layout where all columns have equal width (and the page is set to `width: wide`):

![](images/split-column-widget-4-columns.png)

<details>
<summary>View <code>glance.yml</code></summary>
<br>

```yaml
pages:
  - name: Home
    width: wide
    columns:
      - size: full
        widgets:
          - type: split-column
            max-columns: 4
            widgets:
              - type: reddit
                subreddit: selfhosted
                collapse-after: 15
              - type: reddit
                subreddit: homelab
                collapse-after: 15
              - type: reddit
                subreddit: linux
                collapse-after: 15
              - type: reddit
                subreddit: sysadmin
                collapse-after: 15
```
</details>
<br>

Masonry layout with up to 5 columns where all columns have equal width (and the page is set to `width: wide`):

![](images/split-column-widget-masonry.png)

<details>
<summary>View <code>glance.yml</code></summary>
<br>

```yaml
define:
  - &subreddit-settings
    type: reddit
    collapse-after: 5

pages:
  - name: Home
    width: wide
    columns:
      - size: full
        widgets:
          - type: split-column
            max-columns: 5
            widgets:
              - subreddit: selfhosted
                <<: *subreddit-settings
              - subreddit: homelab
                <<: *subreddit-settings
              - subreddit: linux
                <<: *subreddit-settings
              - subreddit: sysadmin
                <<: *subreddit-settings
              - subreddit: DevOps
                <<: *subreddit-settings
              - subreddit: Networking
                <<: *subreddit-settings
              - subreddit: DataHoarding
                <<: *subreddit-settings
              - subreddit: OpenSource
                <<: *subreddit-settings
              - subreddit: Privacy
                <<: *subreddit-settings
              - subreddit: FreeSoftware
                <<: *subreddit-settings
```
</details>
<br>

Just like the `group` widget, you can insert any widget type, you can even insert a `group` widget inside of a `split-column` widget, but you can't insert a `split-column` widget inside of a `group` widget.


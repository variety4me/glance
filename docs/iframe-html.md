
### iframe
Embed an iframe as a widget.

Example:

```yaml
- type: iframe
  source: <url>
  height: 400
```

#### Properties
| Name | Type | Required | Default |
| ---- | ---- | -------- | ------- |
| source | string | yes | |
| height | integer | no | 300 |

##### `source`
The source of the iframe.

##### `height`
The height of the iframe. The minimum allowed height is 50.

### HTML
Embed any HTML.

Example:

```yaml
- type: html
  source: |
    <p>Hello, <span class="color-primary">World</span>!</p>
```

Note the use of `|` after `source:`, this allows you to insert a multi-line string.


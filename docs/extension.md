
### Extension
Display a widget provided by an external source (3rd party). If you want to learn more about developing extensions, checkout the [extensions documentation](extensions.md) (WIP).

```yaml
- type: extension
  url: https://domain.com/widget/display-a-message
  allow-potentially-dangerous-html: true
  parameters:
    message: Hello, world!
```

#### Properties
| Name | Type | Required | Default |
| ---- | ---- | -------- | ------- |
| url | string | yes | |
| fallback-content-type | string | no | |
| allow-potentially-dangerous-html | boolean | no | false |
| headers | key & value | no | |
| parameters | key & value | no | |

##### `url`
The URL of the extension. **Note that the query gets stripped from this URL and the one defined by `parameters` gets used instead.**

##### `fallback-content-type`
Optionally specify the fallback content type of the extension if the URL does not return a valid `Widget-Content-Type` header. Currently the only supported value for this property is `html`.

##### `headers`
Optionally specify the headers that will be sent with the request. Example:

```yaml
headers:
  x-api-key: ${SECRET_KEY}
```

##### `allow-potentially-dangerous-html`
Whether to allow the extension to display HTML.

> [!WARNING]
>
> There's a reason this property is scary-sounding. It's intended to be used by developers who are comfortable with developing and using their own extensions. Do not enable it if you have no idea what it means or if you're not **absolutely sure** that the extension URL you're using is safe.

##### `parameters`
A list of keys and values that will be sent to the extension as query paramters.


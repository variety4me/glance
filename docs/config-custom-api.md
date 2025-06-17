
### Custom API

Display data from a JSON API using a custom template.

> [!NOTE]
>
> The configuration of this widget requires some basic knowledge of programming, HTML, CSS, the Go template language and Glance-specific concepts.

Examples:

![](images/custom-api-preview-1.png)

<details>
<summary>View <code>glance.yml</code></summary>
<br>

```yaml
- type: custom-api
  title: Random Fact
  cache: 6h
  url: https://uselessfacts.jsph.pl/api/v2/facts/random
  template: |
    <p class="size-h4 color-paragraph">{{ .JSON.String "text" }}</p>
```
</details>
<br>

![](images/custom-api-preview-2.png)

<details>
<summary>View <code>glance.yml</code></summary>
<br>

```yaml
- type: custom-api
  title: Immich stats
  cache: 1d
  url: https://${IMMICH_URL}/api/server/statistics
  headers:
    x-api-key: ${IMMICH_API_KEY}
    Accept: application/json
  template: |
    <div class="flex justify-between text-center">
      <div>
          <div class="color-highlight size-h3">{{ .JSON.Int "photos" | formatNumber }}</div>
          <div class="size-h6">PHOTOS</div>
      </div>
      <div>
          <div class="color-highlight size-h3">{{ .JSON.Int "videos" | formatNumber }}</div>
          <div class="size-h6">VIDEOS</div>
      </div>
      <div>
          <div class="color-highlight size-h3">{{ div (.JSON.Int "usage" | toFloat) 1073741824 | toInt | formatNumber }}GB</div>
          <div class="size-h6">USAGE</div>
      </div>
    </div>
```
</details>
<br>

![](images/custom-api-preview-3.png)

<details>
<summary>View <code>glance.yml</code></summary>
<br>

```yaml
- type: custom-api
  title: Steam Specials
  cache: 12h
  url: https://store.steampowered.com/api/featuredcategories?cc=us
  template: |
    <ul class="list list-gap-10 collapsible-container" data-collapse-after="5">
    {{ range .JSON.Array "specials.items" }}
      <li>
        <a class="size-h4 color-highlight block text-truncate" href="https://store.steampowered.com/app/{{ .Int "id" }}/">{{ .String "name" }}</a>
        <ul class="list-horizontal-text">
          <li>{{ div (.Int "final_price" | toFloat) 100 | printf "$%.2f" }}</li>
          {{ $discount := .Int "discount_percent" }}
          <li{{ if ge $discount 40 }} class="color-positive"{{ end }}>{{ $discount }}% off</li>
        </ul>
      </li>
    {{ end }}
    </ul>
```
</details>

#### Properties
| Name | Type | Required | Default |
| ---- | ---- | -------- | ------- |
| url | string | no | |
| headers | key (string) & value (string) | no | |
| method | string | no | GET |
| body-type | string | no | json |
| body | any | no | |
| frameless | boolean | no | false |
| allow-insecure | boolean | no | false |
| skip-json-validation | boolean | no | false |
| template | string | yes | |
| options | map | no | |
| parameters | key (string) & value (string|array) | no | |
| subrequests | map of requests | no | |

##### `url`
The URL to fetch the data from. It must be accessible from the server that Glance is running on.

##### `headers`
Optionally specify the headers that will be sent with the request. Example:

```yaml
headers:
  x-api-key: your-api-key
  Accept: application/json
```

##### `method`
The HTTP method to use when making the request. Possible values are `GET`, `POST`, `PUT`, `PATCH`, `DELETE`, `OPTIONS` and `HEAD`.

##### `body-type`
The type of the body that will be sent with the request. Possible values are `json`, and `string`.

##### `body`
The body that will be sent with the request. It can be a string or a map. Example:

```yaml
body-type: json
body:
  key1: value1
  key2: value2
  multiple-items:
    - item1
    - item2
```

```yaml
body-type: string
body: |
  key1=value1&key2=value2
```

##### `frameless`
When set to `true`, removes the border and padding around the widget.

##### `allow-insecure`
Whether to ignore invalid/self-signed certificates.

##### `skip-json-validation`
When set to `true`, skips the JSON validation step. This is useful when the API returns JSON Lines/newline-delimited JSON, which is a format that consists of several JSON objects separated by newlines.

##### `template`
The template that will be used to display the data. It relies on Go's `html/template` package so it's recommended to go through [its documentation](https://pkg.go.dev/text/template) to understand how to do basic things such as conditionals, loops, etc. In addition, it also uses [tidwall's gjson](https://github.com/tidwall/gjson) package to parse the JSON data so it's worth going through its documentation if you want to use more advanced JSON selectors. You can view additional examples with explanations and function definitions [here](custom-api.md).

##### `options`
A map of options that will be passed to the template and can be used to modify the behavior of the widget.

<details>
<summary>View examples</summary>

<br>

Instead of defining options within the template and having to modify the template itself like such:

```yaml
- type: custom-api
  template: |
    {{ /* User configurable options */ }}
    {{ $collapseAfter := 5 }}
    {{ $showThumbnails := true }}
    {{ $showFlairs := false }}

     <ul class="list list-gap-10 collapsible-container" data-collapse-after="{{ $collapseAfter }}">
      {{ if $showThumbnails }}
        <li>
          <img src="{{ .JSON.String "thumbnail" }}" alt="thumbnail" />
        </li>
      {{ end }}
      {{ if $showFlairs }}
        <li>
          <span class="flair">{{ .JSON.String "flair" }}</span>
        </li>
      {{ end }}
     </ul>
```

You can use the `options` property to retrieve and define default values for these variables:

```yaml
- type: custom-api
  template: |
    <ul class="list list-gap-10 collapsible-container" data-collapse-after="{{ .Options.IntOr "collapse-after" 5 }}">
      {{ if (.Options.BoolOr "show-thumbnails" true) }}
        <li>
          <img src="{{ .JSON.String "thumbnail" }}" alt="thumbnail" />
        </li>
      {{ end }}
      {{ if (.Options.BoolOr "show-flairs" false) }}
        <li>
          <span class="flair">{{ .JSON.String "flair" }}</span>
        </li>
      {{ end }}
    </ul>
```

This way, you can optionally specify the `collapse-after`, `show-thumbnails` and `show-flairs` properties in the widget configuration:

```yaml
- type: custom-api
  options:
    collapse-after: 5
    show-thumbnails: true
    show-flairs: false
```

Which means you can reuse the same template for multiple widgets with different options:

```yaml
# Note that `custom-widgets` isn't a special property, it's just used to define the reusable "anchor", see https://support.atlassian.com/bitbucket-cloud/docs/yaml-anchors/
custom-widgets:
  - &example-widget
    type: custom-api
    template: |
      {{ .Options.StringOr "custom-option" "not defined" }}

pages:
  - name: Home
    columns:
      - size: full
        widgets:
          - <<: *example-widget
            options:
              custom-option: "Value 1"

          - <<: *example-widget
            options:
              custom-option: "Value 2"
```

Currently, the available methods on the `.Options` object are: `StringOr`, `IntOr`, `BoolOr` and `FloatOr`.

</details>

##### `parameters`
A list of keys and values that will be sent to the custom-api as query paramters.

##### `subrequests`
A map of additional requests that will be executed concurrently and then made available in the template via the `.Subrequest` property. Example:

```yaml
- type: custom-api
  cache: 2h
  subrequests:
    another-one:
      url: https://uselessfacts.jsph.pl/api/v2/facts/random
  title: Random Fact
  url: https://uselessfacts.jsph.pl/api/v2/facts/random
  template: |
    <p class="size-h4 color-paragraph">{{ .JSON.String "text" }}</p>
    <p class="size-h4 color-paragraph margin-top-15">{{ (.Subrequest "another-one").JSON.String "text" }}</p>
```

The subrequests support all the same properties as the main request, except for `subrequests` itself, so you can use `headers`, `parameters`, etc.

`(.Subrequest "key")` can be a little cumbersome to write, so you can define a variable to make it easier:

```yaml
  template: |
    {{ $anotherOne := .Subrequest "another-one" }}
    <p>{{ $anotherOne.JSON.String "text" }}</p>
```

You can also access the `.Response` property of a subrequest as you would with the main request:

```yaml
  template: |
    {{ $anotherOne := .Subrequest "another-one" }}
    <p>{{ $anotherOne.Response.StatusCode }}</p>
```

> [!NOTE]
>
> Setting this property will override any query parameters that are already in the URL.

```yaml
parameters:
  param1: value1
  param2:
    - item1
    - item2
```


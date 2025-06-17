
### ChangeDetection.io
Display a list watches from changedetection.io.

Example

```yaml
- type: change-detection
  instance-url: https://changedetection.mydomain.com/
  token: ${CHANGE_DETECTION_TOKEN}
```

Preview:

![](images/change-detection-widget-preview.png)

#### Properties

| Name | Type | Required | Default |
| ---- | ---- | -------- | ------- |
| instance-url | string | no | `https://www.changedetection.io` |
| token | string | no |  |
| limit | integer | no | 10 |
| collapse-after | integer | no | 5 |
| watches | array of strings | no |  |

##### `instance-url`
The URL pointing to your instance of `changedetection.io`.

##### `token`
The API access token which can be found in `SETTINGS > API`. Optionally, you can specify this using an environment variable with the syntax `${VARIABLE_NAME}`.

##### `limit`
The maximum number of watches to show.

##### `collapse-after`
How many watches are visible before the "SHOW MORE" button appears. Set to `-1` to never collapse.

##### `watches`
By default all of the configured watches will be shown. Optionally, you can specify a list of UUIDs for the specific watches you want to have listed:

```yaml
  - type: change-detection
    watches:
      - 1abca041-6d4f-4554-aa19-809147f538d3
      - 705ed3e4-ea86-4d25-a064-822a6425be2c
```


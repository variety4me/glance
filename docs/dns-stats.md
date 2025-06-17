
### DNS Stats
Display statistics from a self-hosted ad-blocking DNS resolver such as AdGuard Home, Pi-hole, or Technitium.

Example:

```yaml
- type: dns-stats
  service: adguard
  url: https://adguard.domain.com/
  username: admin
  password: ${ADGUARD_PASSWORD}
```

Preview:

![](images/dns-stats-widget-preview.png)

> [!NOTE]
>
> When using AdGuard Home the 3rd statistic on top will be the average latency and when using Pi-hole or Technitium it will be the total number of blocked domains from all adlists.

#### Properties

| Name | Type | Required | Default |
| ---- | ---- | -------- | ------- |
| service | string | no | pihole |
| allow-insecure | bool | no | false |
| url | string | yes |  |
| username | string | when service is `adguard` |  |
| password | string | when service is `adguard` or `pihole-v6` |  |
| token | string | when service is `pihole` |  |
| hide-graph | bool | no | false |
| hide-top-domains | bool | no | false |
| hour-format | string | no | 12h |

##### `service`
Either `adguard`, `technitium`, or `pihole` (major version 5 and below) or `pihole-v6` (major version 6 and above).

##### `allow-insecure`
Whether to allow invalid/self-signed certificates when making the request to the service.

##### `url`
The base URL of the service.

##### `username`
Only required when using AdGuard Home. The username used to log into the admin dashboard.

##### `password`
Required when using AdGuard Home, where the password is the one used to log into the admin dashboard.

Also required when using Pi-hole major version 6 and above, where the password is the one used to log into the admin dashboard or the application password, which can be found in `Settings -> Web Interface / API -> Configure app password`.

##### `token`
Required when using Pi-hole major version 5 or earlier. The API token which can be found in `Settings -> API -> Show API token`.

Also required when using Technitium, an API token can be generated at `Administration -> Sessions -> Create Token`.

##### `hide-graph`
Whether to hide the graph showing the number of queries over time.

##### `hide-top-domains`
Whether to hide the list of top blocked domains.

##### `hour-format`
Whether to display the relative time in the graph in `12h` or `24h` format.



## Server
Server configuration is done through a top level `server` property. Example:

```yaml
server:
  port: 8080
  assets-path: /home/user/glance-assets
```

### Properties

| Name | Type | Required | Default |
| ---- | ---- | -------- | ------- |
| host | string | no |  |
| port | number | no | 8080 |
| proxied | boolean | no | false |
| base-url | string | no | |
| assets-path | string | no |  |

#### `host`
The address which the server will listen on. Setting it to `localhost` means that only the machine that the server is running on will be able to access the dashboard. By default it will listen on all interfaces.

#### `port`
A number between 1 and 65,535, so long as that port isn't already used by anything else.

#### `proxied`
Set to `true` if you're using a reverse proxy in front of Glance. This will make Glance use the `X-Forwarded-*` headers to determine the original request details.

#### `base-url`
The base URL that Glance is hosted under. No need to specify this unless you're using a reverse proxy and are hosting Glance under a directory. If that's the case then you can set this value to `/glance` or whatever the directory is called. Note that the forward slash (`/`) in the beginning is required unless you specify the full domain and path.

> [!IMPORTANT]
> You need to strip the `base-url` prefix before forwarding the request to the Glance server.
> In Caddy you can do this using [`handle_path`](https://caddyserver.com/docs/caddyfile/directives/handle_path) or [`uri strip_prefix`](https://caddyserver.com/docs/caddyfile/directives/uri).

#### `assets-path`
The path to a directory that will be served by the server under the `/assets/` path. This is handy for widgets like the Monitor where you have to specify an icon URL and you want to self host all the icons rather than pointing to an external source.

> [!IMPORTANT]
>
> When installing through docker the path will point to the files inside the container. Don't forget to mount your assets path to the same path inside the container.
> Example:
>
> If your assets are in:
> ```
> /home/user/glance-assets
> ```
>
> You should mount:
> ```
> /home/user/glance-assets:/app/assets
> ```
>
> And your config should contain:
> ```
> assets-path: /app/assets
> ```

##### Examples

Say you have a directory `glance-assets` with a file `gitea-icon.png` in it and you specify your assets path like:

```yaml
assets-path: /home/user/glance-assets
```

To be able to point to an asset from your assets path, use the `/assets/` path like such:

```yaml
icon: /assets/gitea-icon.png
```


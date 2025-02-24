# Configuration and environment variables parser

The `config` plugin parses the configurations of other plugins and uses flags to locate the YAML/JSON config. Each configuration should contain a version. The currently supported version is version 3. The version should be at the top of the configuration and should be a string:

```yaml
version: '3'

# ... other config values
```

## Compatibility matrix

⚠️ Keep in mind that the `yaml` configuration version is not the same as the RR version. They have independent versions.

| RR version     | Configuration version                                                          |
|----------------|--------------------------------------------------------------------------------|
| **>=2023.x.x** | **3**                                                                          |
| **>=2.8**      | **2.7**                                                                        |
| **2.7.x**      | **2.7** `OR` Unversioned (treated as `v2.6.0`, will be auto-updated to `v2.7`) |
| **<=2.6.x**    | Doesn't support versions                                                       |

*non-versioned: configuration used in the 2.0.x-2.6.x releases.

## v3.0 Configuration

#### CHANGES:

**OpenTelemetry Middleware Update:**

As of version `v2023.1.0`, the OpenTelemetry (OTEL) middleware has been separated from the HTTP plugin. It is now
configured using a top-level YAML key.

- **`v2.x`**

```yaml
# HTTP plugin settings.
http:
  ...
  middleware: [ "otel" ]
  otel:
    insecure: true
    compress: false
    client: http
    exporter: otlp
    custom_url: ""
    service_name: "rr_test"
    service_version: "1.0.0"
    endpoint: "127.0.0.1:4318"
```

- **`v2023.x.x`**

```yaml
http:
  ...
  middleware: [ "otel" ]

otel:
  insecure: true
  compress: false
  client: http
  exporter: otlp
  custom_url: ""
  service_name: "rr_test"
  service_version: "1.0.0"
  endpoint: "127.0.0.1:4318"
```

## Updating from `version: 2.7` to `version: 3`:

To update your configuration from version 2.7 to version 3, follow these steps:

1. **Update the version number:** Change the `version` value from `2.7` to `3`.
2. **Relocate the `otel` middleware configuration:** If your configuration uses the `otel` middleware configuration
   within the `http` plugin, move it to the configuration root by cutting it from the `http` plugin and pasting it at
   the root level.

## Tips:

1. By default, `.rr.yaml` used as the configuration, located in the same directory with RR binary.


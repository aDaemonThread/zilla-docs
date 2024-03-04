---
shortTitle: openapi
description: Zilla runtime openapi binding
category:
  - Binding
tag:
  - Server
  - Client
---

# openapi Binding

Zilla runtime openapi binding.

```yaml {2}
openapi_server:
  type: openapi
  kind: server
  options:
    specs:
      openapi-id: spec/openapi.yaml
  exit: openapi_client
openapi_client:
  type: openapi
  kind: client
  options:
    tcp:
      host: localhost
      port: 8080
    specs:
      openapi-id: spec/petstore.yaml

```

## Summary

Defines a binding with `openapi` spec, with `server` or `client` behavior.

The `server` kind `openapi` binding creates composite of `tcp`, `tls`, and `http` bindings with server kind and adapts HTTP request-response streams to OpenAPI request-response streams.

The `client` kind `openapi` binding creates composite of `http`, `tls`, and `tcp` bindings with client kind and adapts OpenAPI request-response streams to HTTP request-response streams.

## Configuration

:::: note Properties
π
- [kind\*](#kind)
- [options](#options)
- [options.tcp](#options-tcp)
- [tpc.host](#tpc-host)
- [tcp.port](#tcp-port)
- [options.tls](#options-tls)
- [tls.version](#tls-version)
- [tls.keys](#tls-keys)
- [tls.trust](#tls-trust)
- [tls.signers](#tls-signers)
- [tls.trustcacerts](#tls-trustcacerts)
- [tls.sni\*](#tls-sni)
- [tls.alpn](#tls-alpn)
- [tls.mutual](#tls-mutual)
- [options.http](#options-http)
- [http.authorization](#http-authorization)
  - [authorization.credentials](#authorization-credentials)
    - [credentials.cookies](#credentials-cookies)
    - [credentials.headers](#credentials-headers)
    - [credentials.query](#credentials-query)
  - [options.spec](#options-spec)
- [exit](#exit)

::: right
\* required
:::

::::

### kind\*

> `enum` [ "client", "server" ]

Behave as a `openapi` `client` or `server`.

```yaml
kind: server
```

### options

> `object`

`openapi`-specific options.

```yaml
options:
  spec:
    openapi-id: spec/openapi.yaml
```

### options.tcp

> `object`

`client` specific `tcp` options.

### tpc.host

> `string`

Hostname or IP address.

### tcp.port

> `integer` | `string` | `array` of  `integer` | `array` of `string`

Port number(s), including port number ranges.

### options.tls

> `object`

`tls` specific options.

### tls.version

> `string`

Protocol version.

### tls.keys

> `array` of `string`

A list of reference names for the Vault key.

### tls.trust

> `array` of `string`

A list of reference names for the Vault certificate.

### tls.signers

> `array` of `string`

A list of reference names for the Vault signer certificate.

### tls.trustcacerts

> `boolean` | Default: `true` when trust is `null`

Trust CA certificates.

### tls.sni\*

> `array` of `string`

A list of the Server Name Indications.

### tls.alpn

> `array` of `string`

Application protocols.

### tls.mutual

> `enum` [ "required", "requested", "none" ] | Default: `"none"`

Mutual authentication.

### options.http

> `object`

`http` specific options.

### http.authorization

> `object` as map of named properties

Authorization by guard for the `HTTP/1.1` and `HTTP/2` protocols.

```yaml
authorization:
  jwt:
    credentials:
      headers:
        authorization: Bearer {credentials}
```

#### authorization.credentials

> `object`

Defines how to extract credentials from the HTTP request.

##### credentials.cookies

> `map` of `name: value` properties

Named cookie value pattern with `{credentials}`.

##### credentials.headers

> `map` of `name: value` properties

Named header value pattern with `{credentials}`, e.g. `"Bearer` `{credentials}"`.

##### credentials.query

> `map` of `name: value` properties

Named query parameter value pattern with `{credentials}`.

#### options.spec

> `object`

OpenAPI spec definition filenames and its unique id.

### exit

> `string`

Default exit binding.

```yaml
exit: echo_server
```

  ---
::: right
\* required
:::
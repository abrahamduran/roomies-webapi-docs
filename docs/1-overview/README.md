---
title: Overview
---

<Block>

# Overview

The Roomies RESTful API is exposed as a HTTP/2 service over SSL. All endpoints live under the URL `https://api.roomies.do` and then generally follow the REST architecture.

</Block>

<Block>

## Environments

We provide two environments you can use, `PROD` and `DEV`.

The production environment offers **rollover backups** every `4h`, but please try to avoid breaking something, or using it as a development environment.

The development environment offers a **sandboxed** environment that **resets itself** daily.

<Example>

```
PROD: https://api.roomies.do
DEV:  https://dev.roomies.do
```

</Example>

</Block>

<Block>

## Current Version

By default, all requests to `https://api.roomies.do` uses the latest version of the REST API.

We try to avoid breaking backwards-compatibility as much as possible. So, in a future release we
to allow the version specification through a header.

<Example>
```
X-API-Version: latest
```
</Example>

</Block>

<Block>

## Content Type

All requests must be encoded as JSON with the `Content-Type: application/json` header. Most responses, including errors, are encoded exclusively as JSON as well.

<Example>

```
Content-Type: application/json
```

</Example>

</Block>

<Block>

## HTTP Verbs

Where possible, API strives to use appropriate HTTP verbs for each action.

|  Verb  | Description |
| :----: | :---------: |
|  GET   | Used for retrieving resources. |
|  POST  | Used for creating resources. |
| DELETE | Used for deleting resources. |

</Block>

<Block>

## Errors

Errors happen, we know. We inform you of error with a structure that tells what
`field` causes it, and any `message` that explains the situation.

<Example>

```json
Status: 400
{
  "someField": [
    "A descriptive message about the error",
    "If multiple errors, another message here"
  ]
}
```

</Example>

</Block>
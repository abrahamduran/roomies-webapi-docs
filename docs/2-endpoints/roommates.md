<Block>

# Roommates

</Block>

<Block>

## Create Roommate

You can use this API to create a new roommate in the app.

### Endpoint

```
POST /api/roommates
```

### Body

|   Name   |  Type  |     Description     |      Required      |
| :------: | :----: | :-----------------: | :----------------: |
|   name   | string | First and last name | :heavy_check_mark: |
|   email  | string |    Email address    | :heavy_check_mark: |
| username | string |       Username      | :heavy_minus_sign: |

### Response

```json
Status: 200
{
  "id": "string",
  "name": "Johnny Appleseed",
  "email": "user@example.com",
  "username": "jhonny",
  "balance": 0,
  "notificationsEnabled": true
}
```

<Example>

<CURL>
```bash
curl -X POST https://dev.roomies.do/api/roommates \
  --data '{
    "name": "Johnny Appleseed",
    "email": "user@example.com"
  }'
```
</CURL>

> Something to keep in mind, the **email** must be unique.
> **Username** will be set using the first name lowercased.
> This means, that you might get an error in those cases.

</Example>

</Block>

<Block>

## List Roommates

You can use this API to list all the roommates registered in the app.

### Endpoint

```
GET /api/roommates
```

### Response

```json
Status: 200
[
  {
    "id": "string",
    "name": "Johnny Appleseed",
    "email": "user@example.com",
    "username": "jhonny",
    "balance": 0,
    "notificationsEnabled": true
  }
]
```

<Example>

<CURL>

```bash
curl -X GET https://dev.roomies.do/api/roommates
```

</CURL>

</Example>

</Block>

<Block>

## Get Roommate

You can use this API to get a roommate's information.

### Endpoint

```
GET /api/roommates/{id}
```

### Parameters

|   Name   |  Type  | Description |      Required      |
| :------: | :----: | :---------: | :----------------: |
|    id    | string |  Roommate's identifier   | :heavy_check_mark: |

### Response

```json
Status: 200
{
  "id": "string",
  "name": "Johnny Appleseed",
  "email": "user@example.com",
  "username": "jhonny",
  "balance": 0,
  "notificationsEnabled": true
}
```

<Example>

<CURL>

```bash
curl -X GET https://dev.roomies.do/api/roommates/{id}
```

> It will return 404 if the roommate cannot be located.

</CURL>

</Example>

</Block>

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

<Block>

## List Expenses

You can use this API to list all the expenses for a given roommate.

### Endpoint

```
GET /api/roommates/{id}/expenses
```

### Parameters

|   Name   |  Type  | Description |      Required      |
| :------: | :----: | :---------: | :----------------: |
|    id    | string |  Roommate's identifier | :heavy_check_mark: |

### Response

```json
Status: 200
[
  {
    "id": "someIdentifier",
    "total": 200,
    "businessName": "Business Name",
    "description": "A beautiful description",
    "date": "2020-08-31",
    "status": "unpaid",
    "id": "string",
    "payee": {
      "id": "someIdentifier",
      "name": "Johnny Appleseed"
    }
  }
]
```

<Example>

<CURL>

```bash
curl -X GET https://dev.roomies.do/api/roommates/{id}/expenses
```

> It will return 404 if the roommate cannot be located.

</CURL>

</Example>

</Block>

<Block>

## Get Expense

You can use this API to get a given expense for a given roommate.
For a **Detailed expense** only the items assigned to the given roommate will be returned.

### Endpoint

```
GET /api/roommates/{roommateId}/expenses/{expenseId}
```

### Parameters

|   Name   |  Type  | Description |      Required      |
| :------: | :----: | :---------: | :----------------: |
| roommateId | string |  Roommate's identifier | :heavy_check_mark: |
| expenseId | string |  Expense's identifier | :heavy_check_mark: |

### Response


```json
Status: 200
[
  {
    "id": "someIdentifier",
    "businessName": "Business Name",
    "payee": {
      "id": "someIdentifier",
      "name": "Charles Chapman"
    },
    "status": "unpaid",
    "date": "2020-08-26",
    "total": 900,
    "description": "A descriptive text",
    "distribution": "even",
    "payers": [
      {
        "id": "someIdentifier",
        "name": "John Doe",
        "amount": 900
      }
    ]
  }
]
```

<small>Keep in mind this is a _Simple Expense_, if you request a _Detailed Expense_ expect a response accordingly.</small>

<Example>

<CURL>

```bash
curl -X GET https://dev.roomies.do/api/roommates/{roommateId}/payments/{expenseId}
```

> It will return 404 if the roommate cannot be located.

</CURL>

</Example>

</Block>

<Block>

## List Payments

You can use this API to list all the payments for a given roommate.

### Endpoint

```
GET /api/roommates/{id}/payments
```

### Parameters

|   Name   |  Type  | Description |      Required      |
| :------: | :----: | :---------: | :----------------: |
|    id    | string |  Roommate's identifier | :heavy_check_mark: |

### Response

```json
Status: 200
[
  {
    "id": "string",
    "total": 500,
    "date": "2020-08-31",
    "description": "A beautiful description",
    "by": {
      "id": "someIdentifier",
      "name": "Johnny Appleseed"
    },
    "to": {
      "id": "someIdentifier",
      "name": "Charles Chapman"
    },
    "expenses": [
      {
        "id": "someIdentifier",
        "date": "2020-08-31",
        "total": 500
      }
    ]
  }
]
```

<Example>

<CURL>

```bash
curl -X GET https://dev.roomies.do/api/roommates/{id}/payments
```

> It will return 404 if the roommate cannot be located.

</CURL>

</Example>

</Block>
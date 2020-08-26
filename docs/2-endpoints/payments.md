<Block>

# Payments

</Block>

<Block>

## Create

You can use this API to register a new payment in the app.

### Endpoint

```
POST /api/payments
```

### Body

|   Name   |  Type  |     Description     |      Required      |
| :------: | :----: | :-----------------: | :----------------: |
|  amount  | decimal | Amount to pay or be paid | :heavy_check_mark: |
|  paidBy  | string | Identifier for the person making the payment | :heavy_check_mark: |
|  paidTo  | string | Identifier for the person the payment is due | :heavy_check_mark: |
| expenseIds | array | Array that contains the identifiers for expenses to be paid | :heavy_check_mark: |
| description | string | A breif decription about the payment | :heavy_minus_sign: |

### Response

```json
Status: 200
{
  "id": "string",
  "total": 0,
  "date": "2020-08-26",
  "description": "string",
  "by": {
    "id": "string",
    "name": "string"
  },
  "to": {
    "id": "string",
    "name": "string"
  },
  "expenses": [
    {
      "id": "string",
      "date": "2020-08-26",
      "total": 0
    }
  ]
}
```

<Example>

<CURL>
```bash
curl -X POST https://dev.roomies.do/api/roommates \
  --data '{
    "expenseIds": [
      "{expenseIdentifier}"
    ],
    "paidTo": "{identifier1}",
    "paidBy": "{identifier2}",
    "amount": 200,
    "description": "A descriptive text"
  }'
```
</CURL>

</Example>

</Block>

<Block>

## List Payments

You can use this API to list all the payments registered in the app.
It will return the payments sorted from newest to oldest.

### Endpoint

```
GET /api/payments
```

### Response

```json
Status: 200
[
  {
    "id": "string",
    "total": 0,
    "date": "2020-08-26",
    "description": "string",
    "by": {
      "id": "string",
      "name": "string"
    },
    "to": {
      "id": "string",
      "name": "string"
    },
    "expenses": [
      {
        "id": "string",
        "date": "2020-08-26",
        "total": 0
      }
    ]
  }
]

```

<Example>

<CURL>

```bash
curl -X GET https://dev.roomies.do/api/payments
```

</CURL>

</Example>

</Block>

<Block>

## Get Payment

You can use this API to get a roommate's information.

### Endpoint

```
GET /api/payments/{id}
```

### Parameters

|   Name   |  Type  | Description |      Required      |
| :------: | :----: | :---------: | :----------------: |
|    id    | string |  Payments's identifier   | :heavy_check_mark: |

### Response

```json
Status: 200
{
  "id": "string",
  "total": 0,
  "date": "2020-08-26",
  "description": "string",
  "by": {
    "id": "string",
    "name": "string"
  },
  "to": {
    "id": "string",
    "name": "string"
  },
  "expenses": [
    {
      "id": "string",
      "date": "2020-08-26",
      "total": 0
    }
  ]
}
```

<Example>

<CURL>

```bash
curl -X GET https://dev.roomies.do/api/payments/{id}
```

> It will return 404 if the payment cannot be located.

</CURL>

</Example>

</Block>

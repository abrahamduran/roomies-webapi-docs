<Block>

# Transactions

This represents expenses and payments as a single unit.
It is only intended to read operations.

</Block>

<Block>

## List Transactions

You can use this API to list all the transactions registered in the app.

### Endpoint

```
GET /api/transactions
```

### Response

```json
Status: 200
[
  {
    "id": "someIdentifier",
    "businessName": "Business Name",
    "payee": {
      "id": "someIdentifier",
      "name": "Samuel Brown"
    },
    "status": "unpaid",
    "date": "2020-08-26",
    "total": 1800,
    "description": "A descriptive text",
    "distribution": "even",
    "payers": [
      {
        "id": "someIdentifier",
        "name": "John Doe",
        "amount": 900
      }
    ],
    "type": "expense"
  },
  {
    "id": "someIdentifier",
    "total": 300,
    "date": "2020-08-26",
    "description": "A descriptive text",
    "by": {
      "id": "someIdentifier",
      "name": "Samuel Brown"
    },
    "to": {
      "id": "someIdentifier",
      "name": "John Doe"
    },
    "expenses": [
      {
        "id": "someIdentifier",
        "date": "2020-08-26",
        "total": 300
      }
    ],
    "type": "payment"
  }
]
```

<small>Keep in mind this is a _Simple Expense_, if you request a _Detailed Expense_ expect a response accordingly.</small>

<Example>

<CURL>

```bash
curl -X GET https://dev.roomies.do/api/transactions
```

</CURL>

</Example>

</Block>

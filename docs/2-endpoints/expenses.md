<Block>

# Expenses

This API supports two types of expenses:

- Simple Expense
- Detailed Expense


A **simple expense** allows you to register a expense which information is minimum:
"I paid _this_ much at _this_ place, and the cost is distributed among _these_ people".

On the other hand, a **detailed expense** would expand the information provided by a
simple expense. It will allow you to detail what _items_ did the person paid for, and among
whom to divide their costs.

</Block>

<Block>

## Register

You can use this API to register a new expense. This, besides saving
the expense, will also update the balences of the selected roommates.

### Endpoint

```
POST /api/expenses
```

### Body

As you can guess, a **simple expense** have a slightly different body from a **detailed expense**.

#### Simple Expense

|      Name    |   Type  |     Description     |      Required      |
|    :------:  | :-----: | :-----------------: | :----------------: |
| businessName | string  | Name of the business or person the expense was made against to | :heavy_check_mark: |
|     total    | decimal | Total cost of the expense | :heavy_check_mark: |
|     date     |  date   | Date the expense was made | :heavy_check_mark: |
| description  | string | A description about what the expense | :heavy_minus_sign: |
| distribution | even<br>proportional<br>custom | Specifies the type of distribution to be used | :heavy_check_mark: |
| payeeId | string | Identifier for the person that's paying for the expense | :heavy_check_mark: |
| payers | array | Array containing the id of those that have to pay for the expense (included the person registering, if applicable) | :heavy_check_mark: |
| payers.amount | decimal | When using custom distribution, the amount that corresponds to the payer | :heavy_minus_sign: |
| payers.multiplier | float | A value between 0 and 1 that indicates the percentage that corresponds to the payer | :heavy_minus_sign: |

::: tip Note
For **distribution**:

- **even** will divide the cost evenly among the selected members
- **proportional** will devide the cost proportionally based on the indicated percentage
- **custom** will allow you to specify a custom amount to be charged against someone

Both, **proportional** and custom **distribution** should be used in conjunction with `payers.multiplier`
and `payers.amount` respectively. If **even** distribution is used, both fields can be omitted.
:::

```json
{
  "businessName": "PriceSmart", // max length: 30
  "date": "2020-08-26",
  "total": 8000,
  "payeeId": "someIdentifier", // id of the roommate that paid it
  "description": "A descriptive text", // max length: 100
  "distribution": "even",
  "payers": [
    {
      "id": "someIdentifier",
      "multiplier": 0, // required if proportional distribution is used
      "amount": 0 // required if custom distribution is used
    }
  ]
}
```

#### Detailed Expense

Most of the field used previously are their definition remain valid for the detailed expense.

|      Name    |   Type  |     Description     |      Required      |
|    :------:  | :-----: | :-----------------: | :----------------: |
| items | array | Array that indicates the items, their distribution and their payers | :heavy_check_mark: |
| items.price | decimal | Price for the item | :heavy_check_mark: |
| items.quantity | float | Indicates the amount of a particular item | :heavy_check_mark: |

```json
{
  "businessName": "PriceSmart", // max length: 30
  "date": "2020-08-26",
  "total": 2000,
  "payeeId": "someIdentifier", // id of the roommate that paid it
  "description": "A descriptive text", // max length: 100
  "items": [
    {
      "name": "Some item", // max length: 30
      "price": 500,
      "quantity": 4,
      "payers": [
        { "id": "someIdentifier1", "multiplier": 0.6 },
        { "id": "someIdentifier2", "multiplier": 0.4 },
      ],
      "distribution": "proportional"
    }
  ]
}
```

### Response

#### Simple Expense

```json
Status: 200
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
    },
    {
      "id": "someIdentifier",
      "name": "Eric White",
      "amount": 900
    }
  ]
}
```

#### Detailed Expense

```json
Status: 200
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
  "items": [
    {
      "id": 1,
      "price": 700,
      "quantity": 1,
      "total": 700,
      "name": "Some item",
      "distribution": "even",
      "payers": [
        {
          "id": "someIdentifier",
          "name": "John Doe",
          "amount": 700
        }
      ]
    },
    {
      "id": 2,
      "price": 550,
      "quantity": 2,
      "total": 1100,
      "name": "Another item",
      "distribution": "even",
      "payers": [
        {
          "id": "someIdentifier",
          "name": "John Doe",
          "amount": 550
        },
        {
          "id": "someIdentifier",
          "name": "Eric White",
          "amount": 550
        }
      ]
    }
  ]
}
```

<Example>

<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>
<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>
<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>

<CURL>

> Simple

```bash
curl -X POST https://dev.roomies.do/api/expenses \
  --data '{
  "businessName": "PriceSmart",
  "date": "2020-08-26",
  "total": 8000,
  "payeeId": "{identifier}",
  "description": "A descriptive text",
  "distribution": "even",
  "payers": [
    { "id": "{identifier}" }
  ]
}'
```

</CURL>

<br><br><br><br><br><br><br><br><br><br>

<CURL>

> Detailed
```bash
curl -X POST https://dev.roomies.do/api/expenses \
  --data '{
  "businessName": "Viverde",
  "date": "2020-08-26",
  "total": 2000,
  "payeeId": "{identifier}",
  "description": "A descriptive text",
  "items": [
    {
      "name": "Some item",
      "price": 500,
      "quantity": 4,
      "payers": [
        { "id": "{identifier}", "multiplier": 0.6 },
        { "id": "{identifier}", "multiplier": 0.4 },
      ],
      "distribution": "proportional"
    }
  ]
}'
```

</CURL>

</Example>

</Block>

<Block>

## List Expenses

You can use this API to list all the expenses registered in the app.
It will return the expenses sorted from newest to oldest.

### Endpoint

```
GET /api/expenses
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
    ]
  }
]
```

<small>Keep in mind this is a _Simple Expense_, if you request a _Detailed Expense_ expect a response accordingly.</small>

<Example>

<CURL>

```bash
curl -X GET https://dev.roomies.do/api/expenses
```

</CURL>

</Example>

</Block>

<Block>

## Get Expense

You can use this API to get a expenses's information.

### Endpoint

```
GET /api/expenses/{id}
```

### Parameters

|   Name   |  Type  | Description |      Required      |
| :------: | :----: | :---------: | :----------------: |
|    id    | string |  Expenses's identifier   | :heavy_check_mark: |

### Response

```json
Status: 200
{
    "id": "someIdentifier",
    "businessName": "Business Name",
    "payee": {
      "id": "someIdentifier",
      "name": "Samuel Brown"
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
```

<small>Keep in mind this is a _Simple Expense_, if you request a _Detailed Expense_ expect a response accordingly.</small>

<Example>

<CURL>

```bash
curl -X GET https://dev.roomies.do/api/expenses/{id}
```

> It will return 404 if the expense cannot be located.

</CURL>

</Example>

</Block>

<Block>

## List Items

You can use this API to list all the items for a particular expense.

### Endpoint

```
GET /api/expenses/{id}/items
```

### Parameters

|   Name   |  Type  | Description |      Required      |
| :------: | :----: | :---------: | :----------------: |
|    id    | string |  Expenses's identifier   | :heavy_check_mark: |

### Response

```json
Status: 200
[
  {
    "id": 1,
    "price": 120,
    "quantity": 1,
    "total": 120,
    "name": "Some item",
    "distribution": "even",
    "payers": [
      {
        "id": "someIdentifier",
        "name": "John Doe",
        "amount": 120
      }
    ]
  }
]
```

<Example>

<CURL>

```bash
curl -X GET https://dev.roomies.do/api/expenses/{id}/items
```

</CURL>

</Example>

</Block>

<Block>

## Get Item

You can use this API to get the item for a particular expense.

### Endpoint

```
GET /api/expenses/{expenseId}/items/{itemId}
```

### Parameters

|   Name   |  Type  | Description |      Required      |
| :------: | :----: | :---------: | :----------------: |
| expenseId | string |  Expenses's identifier   | :heavy_check_mark: |
| itemId | integer |  Item's identifier   | :heavy_check_mark: |

### Response

```json
Status: 200
{
  "id": 1,
  "price": 120,
  "quantity": 1,
  "total": 120,
  "name": "Some item",
  "distribution": "even",
  "payers": [
    {
      "id": "someIdentifier",
      "name": "John Doe",
      "amount": 120
    }
  ]
}
```

<Example>

<CURL>

```bash
curl -X GET https://dev.roomies.do/api/expenses/{expenseId}/items/{itemId}
```

</CURL>

</Example>

</Block>

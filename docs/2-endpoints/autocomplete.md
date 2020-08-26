<Block>

# Autocomple

</Block>

<Block>

## Create

You can use this API to index new resources in the autocomplete records.

### Endpoint

```
POST /api/autocomplete
```

### Body

|   Name   |  Type  |     Description     |      Required      |
| :------: | :----: | :-----------------: | :----------------: |
|   text   | string | The text to be indexed | :heavy_check_mark: |
|   field  | itemName<br>businessName | The field that represents the context for the text | :heavy_check_mark: |

### Response

```json
Status: 200
{
  "id": "someIndentifier",
  "text": "Rubber duck",
  "type": "itemName"
}
```

<Example>

<CURL>
```bash
curl -X POST https://dev.roomies.do/api/autocomplete \
  --data '{
    "text": "Rubber duck",
    "field": "itemName"
  }'
```
</CURL>

</Example>

</Block>

<Block>

## Search

You can use this API to search the autocomplete index for an approximation to your text.

### Endpoint

```
GET /api/autocomplete
```

### Parameters

|   Name   |  Type  |     Description     |      Required      |
| :------: | :----: | :-----------------: | :----------------: |
|   text   | string | The text to be searched | :heavy_check_mark: |
|   field  | all<br>itemName<br>businessName | The field that represents the context for the search | :heavy_minus_sign: |


### Response

```json
Status: 200
[
  "Rubber",
  "Rubber duck"
]
```

<Example>

<CURL>

```bash
curl -X GET https://dev.roomies.do/api/roommates?text={text}&field=all
```

</CURL>

</Example>

</Block>

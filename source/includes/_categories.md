# Categories

## GET /categories

```shell
curl -u adam:password https://localhost:8000/categories
```

> Status code 200 with response as follows:

```json
[
    {
        "id": "5547ad95d4c6285588f4b23c",
        "title": "Cheese"
    },
    {
        "id": "9090ad95d4c6285588f4b23c",
        "title": "Whiz"
    }
]
```

This endpoint retrieves a list of categories available to put streams into

### Request

`GET https://api.attensa.com/categories`

### Response

Status code `200`

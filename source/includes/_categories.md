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
        "title": "Wiz"
    }
]
```

This endpoint retrieves a list of categories available to categorize streams into

### Request

`GET https://api.attensa.com/categories`

### Response

Status code `200`

## PUT /categories

```shell
curl -u username:password \
     -H "Content-Type: application/json" \
     -X POST \
     -d '[
       {
         "id": "5547ad95d4c6285588f4b23c",
         "title": "Cheese",
       },
       {
         "title": "Wiz",
       }
     ]' \
     https://api.attensa.net/streams/{streamId}/items
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
        "title": "Wiz"
    }
]
```

### Request

`PUT https://api.attensa.net/categories`

This updates the list of categories available to put streams into.

### JSON request body parameters
An array of category objects should be provided. Each category takes the following form:

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
id | Id of existing category to update title | No | String | `null`
title | Title of the category. | Yes | String | n/a

<aside class="notice">Any category without an id is considered to be new, and will be assigned an id in the response. If an existing category (with id) is included with a different title, the category's title will be updated.</aside>
<aside class="warning">Be careful! If an existing category is not included, it is removed and any associated streams will be disassociate from the removed category.</aside>
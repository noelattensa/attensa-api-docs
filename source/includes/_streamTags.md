# Stream Tags

## GET /streamTags

```shell
curl -u username:password https://api.attensa.net/streamTags
```
> Status code 200 with response as follows:

```json
[
  {
    "id": "5547ad95d4c6285588f4b23c",
    "label": "Cheese"
  },
  {
    "id": "9090ad95d4c6285588f4b23c",
    "label": "Wiz"
  }
]
```

Get a list of all stream tags.

### Request

`GET https://api.attensa.net/streamTags`

### Response

Status code `200`

## GET /streamTags/{tagId}/streams

```shell
curl -u username:password \
     -X GET \
     -d page=0 \
     -d published=firstName
     -d rows=20 \
     -d term=test \
     -d type=COLLECTION
     https://api.attensa.net/streamTags/{tagId}/streams
```

> Status code 200 with response as follows:

```json
{
  "_paging": {
    "totalElementCount": 1,
    "pageCount": 1,
    "requestedPageSize": 20,
    "elementCount": 1,
    "page": 0
  },
  "_links": {
    "first": "https://api.attensa.net/streamTags/{tagId}/streams?rows=20&page=0&term=test&published=true&type=COLLECTION",
    "last": "https://api.attensa.net/streamTags/{tagId}/streams?rows=20&page=0&term=test&published=true&type=COLLECTION"
  },
  "streams": [{
    "title": "Test Stream 01",
    "groupIsSubscribed": true,
    "description": "Description 01",
    "ownerId": "55414a36e4b0436b6280e668",
    "type": "COLLECTION",
    "emailPostingEnabled": true,
    "openForReading": true,
    "openForPosting": true,
    "published": true,
    "streamEmailAddress": "test.stream.01@email.attensa.net",
    "substreams":[
      {
        "id": "559c1972e4b008b9a5329478",
        "title": "Hi, I am a substream!",
        "type": "RSS"
      }
    ],
    "rssEnabled": false,
    "categoryIds" : ["55414a36e4b0436b6280e668", "823hg4asf34b0436b6280e668"],
    "tagIds": ["55414a36e9878136b6280e668"]
  }]
}
```

Retrieve a paged list of streams that are tagged with a certain stream tag.

### Request

`GET https://api.attensa.com/streamTags/{tagId}/streams`

### Request query parameters

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
page | The page number to retrieve | No | Integer | 0
published | Filter stream list to published or unpublished streams. Omit for all streams. | No | Boolean | `null`
rows | Number of users in each page | No | Integer | 20
term | A search term to narrow the list of streams returned | No | String | `null`
type | Filter results to a specific stream type | No | [searchable stream type](#stream-types) | `null`

### Response

Status code `201`

See the [paging metadata specification](#paging-format) for more information on the `_paging` and `_links` properties

## POST /streamTags

```shell
curl -u username:password \
     -H "Content-Type: application/json" \
     -X POST \
     -d '{
       "label": "Cheese"
     }' \
     https://api.attensa.net/streamTags
```
> Status code 201 with response as follows:

```json
{
  "id": "56161che546097aa51621b47",
  "label": "Cheese"
}
```

Create a new stream tag.

### Request

`POST https://api.attensa.net/streamTags`

### JSON request body

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
label | The tag label | Yes | String | n/a

### Response

Status code `201`

## PUT /streamTags/{tagId}

```shell
curl -u username:password \
     -H "Content-Type: application/json" \
     -X PUT \
     -d '{
       "label": "Wiz"
     }' \
     https://api.attensa.net/streamTags/{tagId}
```
> Status code 200 with response as follows:

```json
{
  "id": "56161che546097aa51621b47",
  "label": "Wiz"
}
```

Edit the label of an existing stream tag

### Request

`PUT https://api.attensa.net/streamTags/{tagId}`

### JSON request body

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
label | The tag label | Yes | String | n/a

### Response

Status code `200`

## DELETE /streamTags/{tagId}

```shell
curl -u username:password \
     -X DELETE \
     https://api.attensa.net/streamTags/{tagId}
```
> 204 empty body returned on success

Delete an existing stream tag from the system.  All streams tagged with that tag will have that tag removed.

### Request

`DELETE https://api.attensa.net/streamTags/{tagId}`

### Response

Status code `204` with empty body
# Briefings

## GET /briefings

```shell
curl -u username:password \
     -X GET \
     -d page=0 \
     -d rows=20 \
     https://api.attensa.net/briefings
```

> Status code 200 with response as follows:

```json
{
  "_paging": {
    "elementCount": 1,
    "page": 0,
    "pageCount": 1,
    "requestedPageSize": 20,
    "totalElementCount": 1
  },
  "_links": {
    "first": "https://api.attensa.net/briefings?rows=20&page=0",
    "last": "https://api.attensa.net/briefings?rows=20&page=0"
  },
  "briefings": [
    {
      "description": "javascript news",
      "templateId": "54eba226e4b050dd8b9c1099",
      "subject": "DailyJS",
      "schedule": {
        "frequency": "DAILY",
        "interval": 2,
        "sendHour": 10,
        "sendMinute": 40,
        "startDate": "2015-08-08",
        "timeZone": "US/Pacific"
      },
      "stream": {
        "categoryIds": ["54eba224e4b050dd8b9c1096"],
        "emailPostingEnabled": false,
        "id": "5519ae56e4b0c0419a88bae1",
        "followersCount": 0,
        "itemsCount": 111,
        "openForPosting": false,
        "openForReading": true,
        "ownerId": "54da7849e4b02386a4658e5d",
        "rssEnabled": true,
        "source": {
            "uri": "http://feeds.feedburner.com/dailyjs"
        },
        "title": "DailyJS",
        "type": "RSS",
        "_links": {
            "self": "https://api.attensa.net/streams/5519ae56e4b0c0419a88bae1",
            "owner": "https://api.attensa.net/users/54da7849e4b02386a4658e5d"
        }
      }
    }
  ]
}
```

Get a paged list of all enabled briefings

### Request

`GET /briefings`

### Request query parameters

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
page | The page number to retrieve | No | Integer | 0
rows | Number of briefings in each page | No | Integer | 20

### Response

Status code `200`

See the [paging metadata specification](#paging-format) for more information on the `_paging` property
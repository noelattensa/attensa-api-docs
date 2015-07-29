# Streams

## Get a specific stream

```shell
curl -u username:password https://api.attensa.net/streams/{streamId}
```

> The above command returns JSON structured like this:

```json
{
  "id": "546e17fcd4c67da2547f5b61",
  "title": "Test Stream 01",
  "ownerId": "55414a36e4b0436b6280e668",
  "description" : "Description 01",
  "type": "COLLECTION",
  "source": {
      "search": "search term",
      "uri": "http://slashdot.org/rss",
      "username": "myUserNameForSecuredRSSFeed"
  },
  "emailPostingEnabled": false,
  "openForReading": true,
  "openForPosting": true,
  "streamEmailAddress": "test.stream.01@email.attensa.net",
  "rssEnabled": false,
  "catgoryIds" : ["55414a36e4b0436b6280e668", "823hg4asf34b0436b6280e668"],
  "numberOfItems": 0,
  "numberOfFollowers": 0,
  "_links": {
        "self": "https://api.attensa.net/streams/546e17fcd4c67da2547f5b61"
    }
}
```

This endpoint retrieves a specific stream

### Request

`GET https://api.attensa.net/streams/{streamId}`

### Response

Status code `200`

## Create a new stream

```shell
curl -u username:password \
     -H "Content-Type: application/json" \
     -X POST \
     -d '{
       "title": "Test Stream 01",
       "description": "Description 01",
       "ownerId": "55414a36e4b0436b6280e668",
       "type": "RSS",
       "source": {
           "uri": "http://slashdot.org/rss",
           "username": "myUserNameForSecuredRSSFeed",
           "password": "myPasswordForSecuredRSSFeed",
       },
       "emailPostingEnabled": false,
       "streamEmailAddress": "test.stream.01@email.attensa.net",
       "openForReading": true,
       "openForPosting": true,
       "rssEnabled": false,
       "categoryIds" : ["55414a36e4b0436b6280e668"]
     }' \
     https://api.attensa.net/users
```

> The above command returns JSON structured like this:

```json
{
  "id": "546e17fcd4c67da2547f5b61",
  "title": "Test Stream 01",
  "ownerId": "55414a36e4b0436b6280e668",
  "description" : "Description 01",
  "type": "COLLECTION",
  "source": {
      "uri": "http://slashdot.org/rss",
      "username": "myUserNameForSecuredRSSFeed"
  },
  "emailPostingEnabled": false,
  "streamEmailAddress": "test.stream.01@email.attensa.net",
  "openForReading": true,
  "openForPosting": true,
  "rssEnabled": false,
  "catgoryIds" : ["55414a36e4b0436b6280e668"],
  "numberOfItems": 0,
  "numberOfFollowers": 0,
  "_links": {
        "self": "https://api.attensa.net/streams/546e17fcd4c67da2547f5b61"
    }
}
```

### Request

`POST https://api.attensa.net/streams`

### JSON request properties

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
title | Stream Title | Yes | String | n/a
description | Stream description | No | String | `null`
ownerId | User id of stream owner | Yes | String of valid user id | n/a
type | Stream type | Yes | COLLECTION, RSS | n/a
source:uri | Uri of rss feed. Only supply for type RSS streams | For type RSS | String | `null`
source:username | Basic auth username for secured rss feed. Only supply for type RSS streams. | For secured RSS streams | String | `null`
source:password | Basic auth password for secured rss feed. Only supply for type RSS streams. | For secured RSS streams | String | `null`
emailPostingEnabled | Allow posting to COLLECTION stream via email. | No | Boolean | false
streamEmailAddress | Email address to for stream if emailPosting is enabled. Only set for collection streams | No | Valid email string | `null`
openForReading | Allow all users to read this stream | No | boolean | false
openForPosting | Allow all users to post content to a COLLECTION stream | No | boolean | false
rssEnabled | Allow public access to an RSS feed of this stream | No | boolean | false
categoryIds | Categories to put the stream in | Yes (empy array for no categories) | [String] | []


### Response

Status code `201`

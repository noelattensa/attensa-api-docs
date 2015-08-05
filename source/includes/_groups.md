# Groups

## GET /groups/{groupId}

```shell
curl -u username:password https://api.attensa.net/groups/{groupId}
```
> Status code 200 with response as follows:

```json
{
  "creatorId": "56161che546097aa51621b47",
  "description": "foo",
  "id": "55161cf7e4b097aa51621b47",
  "name": "test",
  "streamCount": 5,
  "userCount": 2,
  "_links": {
    "self": "http://localhost/groups/55161cf7e4b097aa51621b47"
  }
}
```

This endpoint retrieves information about a specific group

### Request

`GET https://api.attensa.net/groups/{groupsId}`

### Response

Status code `200`

## POST /groups

```shell
curl -u username:password \
     -H "Content-Type: application/json" \
     -X POST \
     -d '{
       "creatorId": "56161che546097aa51621b47"
       "description": "just a test group",
       "name": "test"
     }' \
     https://api.attensa.net/groups
```
> Status code 201 with response as follows:

```json
{
  "creatorId": "56161che546097aa51621b47",
  "description": "just a test group",
  "id": "55161cf7e4b097aa51621b47",
  "name": "test",
  "streamCount": 0,
  "userCount": 0,
  "_links": {
    "self": "http://localhost/groups/55161cf7e4b097aa51621b47"
  }
}
```

Create a new group.

### Request

`POST https://api.attensa.net/groups`

### JSON request body

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
creatorId | Id of the user that should be marked as creator | Yes | String | n/a
description | Description of the group | Yes | String | n/a
name | Name of the group | Yes | String | n/a

### Response

Status code `201`

## PUT /groups/{groupId}

```shell
curl -u username:password \
     -H "Content-Type: application/json" \
     -X PUT \
     -d '{
       "creatorId": "56161che546097aa51621b47"
       "description": "just a test group",
       "name": "test"
     }' \
     https://api.attensa.net/groups/{groupId}
```
> Status code 200 with response as follows:

```json
{
  "creatorId": "56161che546097aa51621b47",
  "description": "just a test group",
  "id": "55161cf7e4b097aa51621b47",
  "name": "test",
  "streamCount": 0,
  "userCount": 0,
  "_links": {
    "self": "http://localhost/groups/55161cf7e4b097aa51621b47"
  }
}
```

Update an existing group.  Updates are applied in a incremental PATCH-like manner, so the entire group resource does not need to be supplied, only the properties that are changing.

### Request

`PUT https://api.attensa.net/groups`

### JSON request body

Parameter | Description | Required | Format | Default
--------- | ----------- | -------- | ------ | -------
creatorId | Id of the user that should be marked as creator | No | String | n/a
description | Description of the group | No | String | n/a
name | Name of the group | No | String | n/a

### Response

Status code `200`
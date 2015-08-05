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
---
title: CubeYou API Docs

language_tabs: # must be one of https://git.io/vQNgJ
 [//]: # - shell
 [//]: # - ruby 
 [//]: # - python -->
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the CubeYou API! You can use our API to access our endpoints, which can get the same info available on out website [www.cubeyou.com](www.cubeyou.com).

## Authentication

> To authorize, use this code:

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
```

> Make sure to replace `meowmeowmeow` with your API key.

CubeYou uses API keys to allow access to the API. You can ask a new CubeYou API key at our website support page.

CubeYou expects for the API key to be included in all API requests to the server in a header that looks like the following:

`cy-auth-token: your-token`

<aside class="notice">
You must replace <code>your-token</code> with your personal API key.
</aside>

## Pagination
All `GET` endpoints which return an object list support skip & limit based pagination. This means that to get all objects, you need to paginate through the results by always using the index of the last resource in the list as a `skip` parameter for the next call.

Default `limit` is set to 50, values up to 50 are permitted, `limit > 50` will cause a `400 Bad Request`. The response list might in some cases return less objects than specified by the limit parameter. This is normal behaviour and should be expected when approaching the end of the list.


Query parameter | Default | Description
--------- | ------- | -----------
skip | 0 | Number of elements skipped.
limit | 50 | Maximum number of elements returned.

<aside class="success">
Use of a negative <code>skip</code> is permitted, it will return last <code>n</code> elements. <br />
Ie: <code>skip=-7</code> will return last 7 elements
</aside>

## HTTP Client

```javascript
const axiosClient = axios.create({
  baseURL: 'https://api.cubeyou.com/v1/',
  timeout: 30000,
  headers: {'cy-auth-token': 'your-token'}
});
```

In our Javascript examples we will use `axios` as http library. It's only for demo purpose, feel free to use whichever library you like.

In all our example we will consider that this type of initialization has been done. It avoids you to specify the `base path` and the `api Key` at each request.


# Demographics
This group of endpoints will handle anything related to targets demographics

Base URL:
`https://api.cubeyou.com/v1/:targetId/demographics`

## Get Gender data


```javascript
axiosClient.get('/:targetId/demographics/gender').then(response => {
  console.log(response.data);
})
```

> The above command, using `5a61d4edb36e685b14458ba4` as targetId, returns JSON structured like this:

```json
[
    {
        "label": "Male",
        "category": "Gender",
        "targets": {
            "5a61d4edb36e685b14458ba4": {
                "targetId": "5a61d4edb36e685b14458ba4",
                "reach": 0.507488580370948,
                "affinity": 1.0139216419891337,
                "average": 0.5005205129810089,
                "penetration": 0.3495,
                "show": "full",
                "interClusterAffinity": 1
            }
        }
    },
    {
        "label": "Female",
        "category": "Gender",
        "targets": {
            "5a61d4edb36e685b14458ba4": {
                "targetId": "5a61d4edb36e685b14458ba4",
                "reach": 0.492511419629052,
                "affinity": 0.9860493422231887,
                "average": 0.4994794870189912,
                "penetration": 0.3399,
                "show": "full",
                "interClusterAffinity": 1
            }
        }
    }
]
```

This endpoint retrieves data for `Male` and `Female`.

### HTTP Request

`GET https://api.cubeyou.com/v1/:targetId/demographics/gender`


## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete



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

## Get *gender* data


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


## Get *age* data


```javascript
axiosClient.get('/:targetId/demographics/age').then(response => {
  console.log(response.data);
})
```

> The above command, using `5a7847fef35cdca8a9c3e2a3` as targetId, returns JSON structured like this:

```json
[{
	"label": "18-24",
	"category": "Age",
	"targets": {
		"5a7847fef35cdca8a9c3e2a3": {
			"targetId": "5a7847fef35cdca8a9c3e2a3",
			"reach": 0.15306229191758672,
			"affinity": 1.0133412901081114,
			"average": 0.15104712835816334,
			"penetration": 0.5051,
			"show": "full",
			"interClusterAffinity": 1
		}
	}
}, {
	"label": "25-34",
	"category": "Age",
	"targets": {
		"5a7847fef35cdca8a9c3e2a3": {
			"targetId": "5a7847fef35cdca8a9c3e2a3",
			"reach": 0.20571491891998397,
			"affinity": 1.0201920728472431,
			"average": 0.20164332226759654,
			"penetration": 0.5085,
			"show": "full",
			"interClusterAffinity": 1
		}
	}
}, {
	"label": "35-44",
	"category": "Age",
	"targets": {
		"5a7847fef35cdca8a9c3e2a3": {
			"targetId": "5a7847fef35cdca8a9c3e2a3",
			"reach": 0.20556984562468633,
			"affinity": 1.0150633381251923,
			"average": 0.20251922998654542,
			"penetration": 0.5059,
			"show": "full",
			"interClusterAffinity": 1
		}
	}
}, {
	"label": "45-54",
	"category": "Age",
	"targets": {
		"5a7847fef35cdca8a9c3e2a3": {
			"targetId": "5a7847fef35cdca8a9c3e2a3",
			"reach": 0.21669869747591908,
			"affinity": 0.9898555062720561,
			"average": 0.2189195252265038,
			"penetration": 0.4934,
			"show": "full",
			"interClusterAffinity": 1
		}
	}
}, {
	"label": "55-69",
	"category": "Age",
	"targets": {
		"5a7847fef35cdca8a9c3e2a3": {
			"targetId": "5a7847fef35cdca8a9c3e2a3",
			"reach": 0.21895424606182376,
			"affinity": 0.9693782982211006,
			"average": 0.22587079416119094,
			"penetration": 0.4831,
			"show": "full",
			"interClusterAffinity": 1
		}
	}
}]
```

This endpoint retrieves *age* data for the specified target.

### HTTP Request

`GET https://api.cubeyou.com/v1/:targetId/demographics/age`




## Get *city* data


```javascript
axiosClient.get('/:targetId/demographics/city?limit=2').then(response => {
  console.log(response.data);
})
```
> In this example has been used `limit=2` in order to limit the result size <br>
> The above command, using `5a7847fef35cdca8a9c3e2a3` as targetId, returns JSON structured like this:

```json
[{
	"label": "New York-Northern New Jersey-Long Island, NY-NJ-PA",
	"category": "Metro Area",
	"targets": {
		"5a7847fef35cdca8a9c3e2a3": {
			"targetId": "5a7847fef35cdca8a9c3e2a3",
			"reach": 0.059326771016627144,
			"affinity": 1.010113094317938,
			"average": 0.058732800663955906,
			"penetration": 0.5034,
			"show": "full",
			"interClusterAffinity": 1
		}
	}
}, {
	"label": "Los Angeles-Long Beach-Santa Ana, CA",
	"category": "Metro Area",
	"targets": {
		"5a7847fef35cdca8a9c3e2a3": {
			"targetId": "5a7847fef35cdca8a9c3e2a3",
			"reach": 0.04605819679170036,
			"affinity": 1.1425406257149961,
			"average": 0.04031208672591172,
			"penetration": 0.5695,
			"show": "full",
			"interClusterAffinity": 1
		}
	}
}]
```
 
This endpoint retrieves *city* data for the specified target.

### HTTP Request

`GET https://api.cubeyou.com/v1/:targetId/demographics/city`


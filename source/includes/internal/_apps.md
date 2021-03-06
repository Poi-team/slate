# Applications

<div class="public-endpoint"></div>
## List applications

Get a list of all applications registered on the Poi Network.

### HTTP Request

`GET /v1/applications`

### Query Parameters

<div class="params-table"></div>
name         | type      | required | default     | description |
-------------| --------- | -------- | ----------- | ----------- |
page         | `integer` |          | 1           | Page number |
per_page     | `integer` |          | 10          | Number of events per page |
category     | `category` |         |             | A filter by [category](#categories) (`mobility`, `health`, ...)

>  JSON Response

```json
  {
    "count": 3,
    "data": {
      "spotlight": [
        <Application>,
        <Application>
      ],
      "applications": [
        <Application>,
        <Application>,
        <Application>
      ]
    }
  }
```

<div class="public-endpoint"></div>
## Fetch application

Get an application's information.

```shell
  curl "/v1/applications/1"
```

### HTTP Request

`GET /v1/applications/:id`

### URL Arguments

<div class="params-table"></div>
name         | type      | required | default     | description |
-------------| --------- | -------- | ----------- | ----------- |
id           | `integer` | true     | 1           | The application's id |

>  JSON Response

```json
  {
    "data": <Application>
  }
```

<div class="private-endpoint"></div>
## Application's connected users

Get the list of all users that have the given application connected.

```shell
  curl "/v1/applications/1/users"
```

### HTTP Request

`GET /v1/applications/:id/users`

### URL Arguments

<div class="params-table"></div>
name         | type      | required | default     | description |
-------------| --------- | -------- | ----------- | ----------- |
id           | `integer` | true     | 1           | The application's id |

>  JSON Response

```json
  {
    "count": 2,
    "data": [
      <User>,
      <User>
    ]
  }
```

<div class="public-endpoint"></div>
## List categories

Get a list of all [categories](#categories) that have applications.

### HTTP Request

`GET /v1/applications/categories`

>  JSON Response

```json
  {
    "data": {
      "mobility": {
        "title": "Mobilité",
        "description": "Poi détermine ton épargne carbone par km selon les moyens de transport que tu choisis. (Base de référence : émission de CO2 pour une personne seule dans sa voiture à essence)"
      },
      "recycling": {
        "title": "Recyclage",
        "description": "Poiem ipsum dolor es sit amet non secitur."
      },
      "consumption": {
        "title": "Consommation",
        "description": "Poiem ipsum dolor es sit amet non secitur."
      }
    }
  }
```

<div class="public-endpoint"></div>
## My Connected Apps

List of all apps the user has connected.

### HTTP Request

`GET /v1/me/apps`

### Query Parameters

<div class="params-table"></div>
name         | type      | required | default     | description |
-------------| --------- | -------- | ----------- | ----------- |
page         | `integer` |          | 1           | Page number |
per_page     | `integer` |          | 20          | Number of events per page |

>  JSON Response

```json
{
  "data": {
    "apps_to_connect": [
      {
        "id": 2,
        "name": "Yoyo",
        "icon": "https://poi-api.s3.amazonaws.com/application/icon/logo_yoyo_189ed5d21e.png",
        "category": "recycling"
      }
    ],
    "connected_apps": [
      {
        "id": 1,
        "name": "Lime",
        "icon": "https://poi-api.s3.amazonaws.com/application/icon/logo_lime_baafc20747.png",
        "email": "toto@gmail.com",
        "category": "mobility",
        "status": "connected"
      },
      {
        "id": 3,
        "name": "Phenix",
        "icon": "https://poi-api.s3.amazonaws.com/application/icon/logo_phenix_ba5b6fa137.png",
        "email": "tech@poi.app",
        "category": "consumption",
        "status": "connected"
      }
    ]
  }
}
```

<div class="public-endpoint"></div>
## Connect an app

Allows a user to connect their account to a new application. To do so, you will need to send the user's credentials encrypted using **RSA**.
Here are some libraries that you can use: 

- [uRSA](https://github.com/JoshKaufman/ursa) [JS]
- [JSencrypt](https://github.com/travist/jsencrypt) [JS]
- [OpenSSL::PKey::RSA](https://ruby-doc.org/stdlib-2.5.1/libdoc/openssl/rdoc/OpenSSL/PKey/RSA.html) [Ruby]

The public key used for encryption is the following

<div class="rsa-pkey-container">
<pre class="rsa-pkey">-----BEGIN PUBLIC KEY-----
MIICIjANBgkqhkiG9w0BAQEFAAOCAg8AMIICCgKCAgEAnJafV/BLkTOVPst3v1A1
7NpM4lpT8yYiVzjwkDpT4RYPiSqvGV+fLImwT7Whi+UPsfmzwA8toZIxeTgdm3rO
xW8Oa9bHv5VVWi8Bxvz77u5I2EmdbxI6Q3aGBd7dQodl3Pr6ULC0j+Vl4qQHYsb2
W1qlsUBZaVN7fdwal2yTp+qErnBIilFOC2jVex7gNxXso2HDjHR4ou/w8pChByR1
duvIga8XF6QavotOiPaalVnY2P60RmjIXSzyqVhgCBTT90DWZUzpH8+3dFLMSbSh
0q9Bb9wNUi0bzFkQwKwwGY8v1wqi23nh9pfqhGBlIpUkH77qe7HBCjKGzXPNs6gx
JhRglNRpl9/ufMSCiq7Pt7j4gFOI1BJbNezoQ2fKtC0FPlC0sjtTOHkoA2DINEMG
VYfrrCo3cNscV0zfdNp859VAmTvYqJS5WzbzCDPi0tbaO/OK7ztUUOLU7SzClpGd
RRos6yCYOHPeV2hEdN7CzVSEpX+7TdTX1GeqpXy/I7ysKaAHwjJ/1wG4Suic0iam
44zMyN8F2ZOhIqAq5F7OGqyjFrPtc43tzBaAxK1a3Br749YUnfBQCsc8B7AqNW4m
x7UFwoQFbmPaUqkBN0O+6jQq91ygo8B/RkXbz1r/pcGdhJJ6xLT+tYucsE456/LS
d5Wd1kV4SfAc1s0QEtpkXYkCAwEAAQ==
-----END PUBLIC KEY-----
</pre>
</div>

> Request Body

```json
  {
      "email": "george@gmail.com",
      "encrypted_password": "WJKZHcAzH9Ee8iavMUvYSKGkSXCcaTthalXTIrUKmjnV1gXgHoPg9/mXR4/fyP/pG87Z1EGPXyM1rUzRWYIlvBSHsLa+EQnFimNGr8NhFNs52AfzsHRM1/BQumTK6Q/ThsMIqbsKnnfYO8NQKbjPprT9NkzWqgpAzuH9XvXGyg0=",
  }
```

### HTTP Request

`POST /v1/me/apps/:id`

### URL Arguments

<div class="params-table"></div>
name          | type      | required | default     | description |
--------------| --------- | -------- | ----------- | ----------- |
id            | `integer`  | true         |             | The application id |

### Parameters

<div class="params-table"></div>
name          | type      | required | default     | description |
--------------| --------- | -------- | ----------- | ----------- |
email         | `string`  | true     |             | The user's email for this app |
encrypted_password      | `string`  | true     |             | The user's password encrypted with RSA and the given public key |


>  JSON Response

```json
{
  "data": {
    "apps_to_connect": [
      {
        "id": 2,
        "name": "Yoyo",
        "icon": "https://poi-api.s3.amazonaws.com/application/icon/logo_yoyo_189ed5d21e.png",
        "category": "recycling"
      }
    ],
    "connected_apps": [
      {
        "id": 1,
        "name": "Lime",
        "icon": "https://poi-api.s3.amazonaws.com/application/icon/logo_lime_baafc20747.png",
        "email": "toto@gmail.com",
        "category": "mobility",
        "status": "connected"
      },
      {
        "id": 3,
        "name": "Phenix",
        "icon": "https://poi-api.s3.amazonaws.com/application/icon/logo_phenix_ba5b6fa137.png",
        "email": "tech@poi.app",
        "category": "consumption",
        "status": "connected"
      }
    ]
  }
}
```
<div class="public-endpoint"></div>
## Disconnect an app

### HTTP Request

`DELETE /v1/me/apps/:id`

### URL Arguments

<div class="params-table"></div>
name                 | type      | required | default     | description |
---------------------| --------- | -------- | ----------- | ----------- |
id                   | `integer` | true     |         | Application's id |

>  JSON Response

```json
{
  "data": {
    "apps_to_connect": [
      {
        "id": 2,
        "name": "Yoyo",
        "icon": "https://poi-api.s3.amazonaws.com/application/icon/logo_yoyo_189ed5d21e.png",
        "category": "recycling"
      }
    ],
    "connected_apps": [
      {
        "id": 1,
        "name": "Lime",
        "icon": "https://poi-api.s3.amazonaws.com/application/icon/logo_lime_baafc20747.png",
        "email": "toto@gmail.com",
        "category": "mobility",
        "status": "connected"
      },
      {
        "id": 3,
        "name": "Phenix",
        "icon": "https://poi-api.s3.amazonaws.com/application/icon/logo_phenix_ba5b6fa137.png",
        "email": "tech@poi.app",
        "category": "consumption",
        "status": "connected"
      }
    ]
  }
}
```

<div class="public-endpoint"></div>
## List potential applications

### HTTP Request

`GET /v1/potential_applications`

### URL Arguments

<div class="params-table"></div>
name         | type      | required | default     | description |
-------------| --------- | -------- | ----------- | ----------- |
page         | `integer` |          | 1           | Page number |
per_page     | `integer` |          | 20          | Number of events per page |

>  Response

```json
 {
    "count": 3,
    "data": [
        {
            "id": 7,
            "name": "Cityscoot",
            "icon": "https://poi-api.s3.amazonaws.com/potential_application/icon/logo_cityscoot_3d68de5a52.png",
            "has_voted": false
        },
        {
            "id": 8,
            "name": "Fitbit",
            "icon": "https://poi-api.s3.amazonaws.com/potential_application/icon/logo_fitbit_6badc369fd.png",
            "has_voted": false
        },
        {
            "id": 9,
            "name": "Lilo",
            "icon": "https://poi-api.s3.amazonaws.com/potential_application/icon/logo_lilo_792e5ae998.png",
            "has_voted": true
        }
    ]
}
```


<div class="public-endpoint"></div>
## Suggest a potential application

Allows an user to suggest a new application to be integrated on the Poi Network. The user will also automaticaly vote for this application.

> Request Body

```json
  {
    "name": "Lime",
    "category": "mobility",
    "url": "https://www.lime.com"
  }
```

### HTTP Request

`POST /v1/potential_applications`

### Parameters

<div class="params-table"></div>
name          | type      | required | default     | description |
--------------| --------- | -------- | ----------- | ----------- |
name          | `string`  | true     |             | The potential app's name |
category      | `string`  | true     |             | The potential app's [category](#categories) |
url           | `string`  | true     |             | The potential app's website URL |


>  JSON Response

```json
  {
    "data": {
      "id": 2,
      "name": "Lime",
      "category": "mobility",
      "description": null,
      "icon": null, 
      "url": "https://lime.com",
      "status": "pending"
    }
  }
```


<div class="public-endpoint"></div>
## Vote for a potential application

Votes for a potential application in stead of the current user. An application can only be voted once.

### HTTP Request

`POST /v1/potential_applications/:id/vote`

### URL Arguments

<div class="params-table"></div>
name          | type      | required | default     | description |
--------------| --------- | -------- | ----------- | ----------- |
id            | `integer`  | true         |             | The potential application's id |

>  JSON Response

```json
  {
    "success": true,
    "data": {
      "voter_id": 1,
      "potential_application_id": 1,
      "name": "Lime"
    }
  }
```

<div class="public-endpoint"></div>
## Remove vote on a potential application

Removes the previous vote by the current user on a potential application.

### HTTP Request

`DELETE /v1/potential_applications/:id/vote`

### URL Arguments

<div class="params-table"></div>
name          | type      | required | default     | description |
--------------| --------- | -------- | ----------- | ----------- |
id            | `integer`  | true         |             | The potential application's id |

>  Response

```
  HTTP 204 No Content
```


<div class="public-endpoint"></div>
## Batch vote (wishlist)

Votes for a list of potential applications in stead of the current user. Any application missing from the parameters will be considered removed from the votes of the user.

> Request Body

```json
  {
     	"apps_wishlist": [7, 9]
  }
```

### HTTP Request

`PUT /v1/me/wishlist`

### URL Arguments

<div class="params-table"></div>
name          | type      | required | default     | description |
--------------| --------- | -------- | ----------- | ----------- |
apps_wishlist | `array`   | true         |         | An array of ids as `Integer`. |

>  JSON Response

```json
{
  "count": 3,
  "data": [
    {
      "id": 7,
      "name": "Cityscoot",
      "icon": "https://poi-api.s3.amazonaws.com/potential_application/icon/logo_cityscoot_3d68de5a52.png",
      "has_voted": false
    },
    {
      "id": 8,
      "name": "Fitbit",
      "icon": "https://poi-api.s3.amazonaws.com/potential_application/icon/logo_fitbit_6badc369fd.png",
      "has_voted": false
    },
    {
      "id": 9,
      "name": "Lilo",
      "icon": "https://poi-api.s3.amazonaws.com/potential_application/icon/logo_lilo_792e5ae998.png",
      "has_voted": true
    }
  ]
}
```
---
title: API Reference

language_tabs: # must be one of https://github.com/rouge-ruby/rouge/wiki/List-of-supported-languages-and-lexers
  - shell
  - ruby
  - python
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the Kittn API
---

# Introduction

Welcome to the Kittn API! You can use our API to access Kittn API endpoints, which can get information on various cats, kittens, and breeds in our database.

We have language bindings in Shell, Ruby, Python, and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

This example API documentation page was created with [Slate](https://github.com/slatedocs/slate). Feel free to edit it and use it as a base for your own API's documentation.

# Authentication

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
curl "api_endpoint_here" \
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
```

> Make sure to replace `meowmeowmeow` with your API key.

Kittn uses API keys to allow access to the API. You can register a new Kittn API key at our [developer portal](http://example.com/developers).

Kittn expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>

# Kittens

## Get All Kittens

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://example.com/api/kittens" \
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let kittens = api.kittens.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/api/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

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
curl "http://example.com/api/kittens/2" \
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
curl "http://example.com/api/kittens/2" \
  -X DELETE \
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

---
title: express-typescript-skeleton v2.7.1
language_tabs:
  - python: Python
  - javascript: javascript
  - go: Go
language_clients:
  - python: ""
  - javascript: ""
  - go: ""
toc_footers: []
includes: []
search: false
highlight_theme: darkula
headingLevel: 2

---

<!-- Generator: Widdershins v4.0.1 -->

<h1 id="express-typescript-skeleton">express-typescript-skeleton v2.7.1</h1>

> Scroll down for code samples, example requests and responses. Select a language for code samples from the tabs above or the mobile navigation menu.

🔰🦸 Template to start developing a REST API with Node.js (Express), TypeScript, ESLint, Prettier, Husky, Prisma, etc.

Email: <a href="mailto:borjapazr@gmail.com">Borja Paz Rodríguez</a> Web: <a href="https://bpaz.dev">Borja Paz Rodríguez</a> 
License: <a href="https://spdx.org/licenses/MIT.html">Licensed Under MIT</a>

# Authentication

- HTTP Authentication, scheme: bearer A valid *Access Token* is required to access protected resources. To obtain one, simply authenticate to the API through the authentication endpoint. If the authentication is successful, an Access Token and a Refresh Token will be returned.

The *Access Token* can be attached to requests using one of the headers `Authorization: Bearer <access_token>` and `access-token: <access-token>` or a cookie called `access-token`.

The *Refresh Token* can be sent using the header `refresh-token: <refresh-token>` or the cookie `refresh-token`.

🧐 *The headers override the cookies, so if both are sent, the value of the headers will be used. In the case of the Access Token, the header with the highest priority is the one corresponding to the Authorization Bearer scheme.*

**Sample username and password to use on `/api/auth/login` endpoint**: `janedoe` / `123456`

<h1 id="express-typescript-skeleton-authentication">Authentication</h1>

Login and register users

## User login

<a id="opIdauthenticationControllerAuthenticateUser"></a>

> Code samples

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json'
}

r = requests.post('/api/auth/login', headers = headers)

print(r.json())

```

```javascript
const inputBody = '{
  "username": "janedoe",
  "password": "123456"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('/api/auth/login',
{
  method: 'POST',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Accept": []string{"application/json"},
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("POST", "/api/auth/login", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`POST /api/auth/login`

Endpoint to perform a user login to obtain access token and refresh token

> Body parameter

```json
{
  "username": "janedoe",
  "password": "123456"
}
```

<h3 id="user-login-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|none|
|» username|body|string|false|none|
|» password|body|string|false|none|

> Example responses

> 200 Response

```json
{
  "uuid": "string",
  "username": "string",
  "email": "user@example.com",
  "roles": [
    "string"
  ],
  "accessToken": "string",
  "refreshToken": "string"
}
```

<h3 id="user-login-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|[UserSuccessfullyAuthenticatedApiResponse](#schemausersuccessfullyauthenticatedapiresponse)|

<aside class="success">
This operation does not require authentication
</aside>

## Refresh access token

<a id="opIdauthenticationControllerRefreshAccessToken"></a>

> Code samples

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.post('/api/auth/refresh', headers = headers)

print(r.json())

```

```javascript

const headers = {
  'Accept':'application/json'
};

fetch('/api/auth/refresh',
{
  method: 'POST',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("POST", "/api/auth/refresh", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`POST /api/auth/refresh`

Endpoint to update the access token and the refresh token

> Example responses

> 200 Response

```json
{
  "uuid": "string",
  "username": "string",
  "email": "user@example.com",
  "roles": [
    "string"
  ],
  "accessToken": "string",
  "refreshToken": "string"
}
```

<h3 id="refresh-access-token-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|[UserSuccessfullyAuthenticatedApiResponse](#schemausersuccessfullyauthenticatedapiresponse)|

<aside class="success">
This operation does not require authentication
</aside>

## User logout

<a id="opIdauthenticationControllerRevokeSession"></a>

> Code samples

```python
import requests

r = requests.delete('/api/auth/logout')

print(r.json())

```

```javascript

fetch('/api/auth/logout',
{
  method: 'DELETE'

})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("DELETE", "/api/auth/logout", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`DELETE /api/auth/logout`

Endpoint to perform a user logout and revoke a valid session

<h3 id="user-logout-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|204|[No Content](https://tools.ietf.org/html/rfc7231#section-6.3.5)|No Content|None|

<aside class="success">
This operation does not require authentication
</aside>

## Authenticated user information

<a id="opIdauthenticationControllerMe"></a>

> Code samples

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'Bearer {access-token}'
}

r = requests.get('/api/auth/me', headers = headers)

print(r.json())

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'Bearer {access-token}'
};

fetch('/api/auth/me',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authorization": []string{"Bearer {access-token}"},
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "/api/auth/me", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /api/auth/me`

Endpoint to obtain the authenticated user's details

> Example responses

> 200 Response

```json
{
  "uuid": "string",
  "gender": "undefined",
  "firstName": "string",
  "lastName": "string",
  "birthDate": "2019-08-24",
  "username": "string",
  "email": "user@example.com",
  "phoneNumber": "string",
  "address": "string",
  "profilePicUrl": "string",
  "roles": [
    "admin"
  ]
}
```

<h3 id="authenticated-user-information-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|[AuthenticatedUserApiResponse](#schemaauthenticateduserapiresponse)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Unauthorized|[ExceptionApiResponse](#schemaexceptionapiresponse)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Forbidden|[ExceptionApiResponse](#schemaexceptionapiresponse)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
Bearer
</aside>

<h1 id="express-typescript-skeleton-health">Health</h1>

Status and health check

## Health check

<a id="opIdhealthControllerCheckHealthStatus"></a>

> Code samples

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('/api/healthz', headers = headers)

print(r.json())

```

```javascript

const headers = {
  'Accept':'application/json'
};

fetch('/api/healthz',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "/api/healthz", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /api/healthz`

Endpoint to check whether the application is healthy or unhealthy

> Example responses

> 200 Response

```json
{
  "status": "string",
  "message": "string",
  "appVersion": "2.7.1"
}
```

<h3 id="health-check-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|[HealthStatusApiResponse](#schemahealthstatusapiresponse)|

<aside class="success">
This operation does not require authentication
</aside>

<h1 id="express-typescript-skeleton-user">User</h1>

User management

## Obtain all users

<a id="opIduserControllerSearchAllUsers"></a>

> Code samples

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'Bearer {access-token}'
}

r = requests.get('/api/users', headers = headers)

print(r.json())

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'Bearer {access-token}'
};

fetch('/api/users',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authorization": []string{"Bearer {access-token}"},
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "/api/users", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /api/users`

Endpoint to obtain all users

> Example responses

> 200 Response

```json
[
  {
    "uuid": "string",
    "gender": "undefined",
    "firstName": "string",
    "lastName": "string",
    "birthDate": "2019-08-24",
    "username": "string",
    "email": "user@example.com",
    "phoneNumber": "string",
    "address": "string",
    "profilePicUrl": "string",
    "passwordHash": "string",
    "roles": [
      "admin"
    ],
    "verified": true,
    "enabled": true
  }
]
```

<h3 id="obtain-all-users-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|Inline|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Unauthorized|[ExceptionApiResponse](#schemaexceptionapiresponse)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Forbidden|[ExceptionApiResponse](#schemaexceptionapiresponse)|

<h3 id="obtain-all-users-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[[UserApiResponse](#schemauserapiresponse)]|false|none|none|
|» uuid|string|false|none|none|
|» gender|string|false|none|none|
|» firstName|string|false|none|none|
|» lastName|string|false|none|none|
|» birthDate|string(date)|false|none|none|
|» username|string|false|none|none|
|» email|string(email)|false|none|none|
|» phoneNumber|string|false|none|none|
|» address|string|false|none|none|
|» profilePicUrl|string|false|none|none|
|» passwordHash|string|false|none|none|
|» roles|[string]|false|none|none|
|» verified|boolean|false|none|none|
|» enabled|boolean|false|none|none|

#### Enumerated Values

|Property|Value|
|---|---|
|gender|undefined|
|gender|male|
|gender|female|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
Bearer
</aside>

## Obtain user by UUID

<a id="opIduserControllerFindUser"></a>

> Code samples

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'Bearer {access-token}'
}

r = requests.get('/api/users/{uuid}', headers = headers)

print(r.json())

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'Bearer {access-token}'
};

fetch('/api/users/{uuid}',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authorization": []string{"Bearer {access-token}"},
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "/api/users/{uuid}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /api/users/{uuid}`

Endpoint to obtain a user by UUID

<h3 id="obtain-user-by-uuid-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|uuid|path|string|true|none|

> Example responses

> 200 Response

```json
{
  "uuid": "string",
  "gender": "undefined",
  "firstName": "string",
  "lastName": "string",
  "birthDate": "2019-08-24",
  "username": "string",
  "email": "user@example.com",
  "phoneNumber": "string",
  "address": "string",
  "profilePicUrl": "string",
  "passwordHash": "string",
  "roles": [
    "admin"
  ],
  "verified": true,
  "enabled": true
}
```

<h3 id="obtain-user-by-uuid-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|[UserApiResponse](#schemauserapiresponse)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Unauthorized|[ExceptionApiResponse](#schemaexceptionapiresponse)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Forbidden|[ExceptionApiResponse](#schemaexceptionapiresponse)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
Bearer
</aside>

# Schemas

<h2 id="tocS_UserSuccessfullyAuthenticatedApiResponse">UserSuccessfullyAuthenticatedApiResponse</h2>
<!-- backwards compatibility -->
<a id="schemausersuccessfullyauthenticatedapiresponse"></a>
<a id="schema_UserSuccessfullyAuthenticatedApiResponse"></a>
<a id="tocSusersuccessfullyauthenticatedapiresponse"></a>
<a id="tocsusersuccessfullyauthenticatedapiresponse"></a>

```json
{
  "uuid": "string",
  "username": "string",
  "email": "user@example.com",
  "roles": [
    "string"
  ],
  "accessToken": "string",
  "refreshToken": "string"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|uuid|string|false|none|none|
|username|string|false|none|none|
|email|string(email)|false|none|none|
|roles|[string]|false|none|none|
|accessToken|string|false|none|none|
|refreshToken|string|false|none|none|

<h2 id="tocS_AuthenticatedUserApiResponse">AuthenticatedUserApiResponse</h2>
<!-- backwards compatibility -->
<a id="schemaauthenticateduserapiresponse"></a>
<a id="schema_AuthenticatedUserApiResponse"></a>
<a id="tocSauthenticateduserapiresponse"></a>
<a id="tocsauthenticateduserapiresponse"></a>

```json
{
  "uuid": "string",
  "gender": "undefined",
  "firstName": "string",
  "lastName": "string",
  "birthDate": "2019-08-24",
  "username": "string",
  "email": "user@example.com",
  "phoneNumber": "string",
  "address": "string",
  "profilePicUrl": "string",
  "roles": [
    "admin"
  ]
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|uuid|string|false|none|none|
|gender|string|false|none|none|
|firstName|string|false|none|none|
|lastName|string|false|none|none|
|birthDate|string(date)|false|none|none|
|username|string|false|none|none|
|email|string(email)|false|none|none|
|phoneNumber|string|false|none|none|
|address|string|false|none|none|
|profilePicUrl|string|false|none|none|
|roles|[string]|false|none|none|

#### Enumerated Values

|Property|Value|
|---|---|
|gender|undefined|
|gender|male|
|gender|female|

<h2 id="tocS_ExceptionApiResponse">ExceptionApiResponse</h2>
<!-- backwards compatibility -->
<a id="schemaexceptionapiresponse"></a>
<a id="schema_ExceptionApiResponse"></a>
<a id="tocSexceptionapiresponse"></a>
<a id="tocsexceptionapiresponse"></a>

```json
{
  "status": 202,
  "code": "im_a_teapot",
  "message": "I'm a teapot",
  "appVersion": "2.7.1"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|status|integer|false|none|none|
|code|string|false|none|none|
|message|string|false|none|none|
|appVersion|string|false|none|none|

#### Enumerated Values

|Property|Value|
|---|---|
|status|202|
|status|502|
|status|400|
|status|409|
|status|100|
|status|201|
|status|417|
|status|424|
|status|403|
|status|504|
|status|410|
|status|505|
|status|418|
|status|419|
|status|507|
|status|500|
|status|411|
|status|423|
|status|420|
|status|405|
|status|301|
|status|302|
|status|207|
|status|300|
|status|511|
|status|204|
|status|203|
|status|406|
|status|404|
|status|501|
|status|304|
|status|200|
|status|206|
|status|402|
|status|308|
|status|412|
|status|428|
|status|102|
|status|407|
|status|431|
|status|408|
|status|413|
|status|414|
|status|416|
|status|205|
|status|303|
|status|503|
|status|101|
|status|307|
|status|429|
|status|401|
|status|451|
|status|422|
|status|415|
|status|305|
|status|421|

<h2 id="tocS_HealthStatusApiResponse">HealthStatusApiResponse</h2>
<!-- backwards compatibility -->
<a id="schemahealthstatusapiresponse"></a>
<a id="schema_HealthStatusApiResponse"></a>
<a id="tocShealthstatusapiresponse"></a>
<a id="tocshealthstatusapiresponse"></a>

```json
{
  "status": "string",
  "message": "string",
  "appVersion": "2.7.1"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|status|string|false|none|none|
|message|string|false|none|none|
|appVersion|string|false|none|none|

<h2 id="tocS_UserApiResponse">UserApiResponse</h2>
<!-- backwards compatibility -->
<a id="schemauserapiresponse"></a>
<a id="schema_UserApiResponse"></a>
<a id="tocSuserapiresponse"></a>
<a id="tocsuserapiresponse"></a>

```json
{
  "uuid": "string",
  "gender": "undefined",
  "firstName": "string",
  "lastName": "string",
  "birthDate": "2019-08-24",
  "username": "string",
  "email": "user@example.com",
  "phoneNumber": "string",
  "address": "string",
  "profilePicUrl": "string",
  "passwordHash": "string",
  "roles": [
    "admin"
  ],
  "verified": true,
  "enabled": true
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|uuid|string|false|none|none|
|gender|string|false|none|none|
|firstName|string|false|none|none|
|lastName|string|false|none|none|
|birthDate|string(date)|false|none|none|
|username|string|false|none|none|
|email|string(email)|false|none|none|
|phoneNumber|string|false|none|none|
|address|string|false|none|none|
|profilePicUrl|string|false|none|none|
|passwordHash|string|false|none|none|
|roles|[string]|false|none|none|
|verified|boolean|false|none|none|
|enabled|boolean|false|none|none|

#### Enumerated Values

|Property|Value|
|---|---|
|gender|undefined|
|gender|male|
|gender|female|


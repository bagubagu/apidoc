## Authentication

Chynge API follows OAuth 2.0 specification for authentication. The API 
supports client credential grant to be used for developers created
middleware applications and authorization code grant for mobile and SPA
type applications.

In the past the API supported the use of resource owner credential grant.
It is now discouraged and will not be supported in the future. Applications
that have been using resource owner credential grant will continue to work.

### Authenticate through client credential grant

This section is intended as how to for developer's trusted middleware
application (middleware-app) to authenticate to Chynge API through client
credential grant.


To aquire an access_token middleware-appe sends a POST request to 
`api.chynge.com/v1/auth` with the following body parameters:
- `client_id`
- `client_secret`

{% method %}

{% sample lang="curl" %}
```bash
curl -X POST \
  --url 'https://api.chynge.com/v1/auth' \
  --header 'Content-Type: application/json' \
  --data '{"client_secret": "tUSfmzgzV0LMsuwgxxxxxxxxxxxxxxxxxxxxxxxxx", "client_id": "U3kTfxxxxxxxxxxxxxxx"}' 
``` 

{% sample lang="js" %}
```js
const headers = new Headers({
  'Content-type': 'application/json'
});

const body = JSON.stringify({
  client_id: 'U3kTfxxxxxxxxxxxxxxx',
  client_secret: 'tUSfmzgzV0LMsuwgxxxxxxxxxxxxxxxxxxxxxxxxx'
});

const options = {
  method: 'POST',
  headers: headers,
  body: body
};

fetch('https://api.chynge.com/v1/auth', options).then(response => {
  console.log('access_token:', response.access_token);
});
``` 

{% endmethod %}

The authorization server will respond with a JSON object containing
following properties:
- `token_type` with the value of 'Bearer'
- `expires_in` with an integer representing the TTL of the access token
- `access_token` is the access token itself

```bash
{
  "access_token": "eyJ0eXAxxxxxxxxxx.asdfasdfxxxxxxxxxx.uiokdfhksjdxxxxxx",
  "expires_in": 86400,
  "token_type": "Bearer"
}
```

Middleware-app can now use the returned `access_token` as the bearer token
to authenticate with Chynge API endpoints.

```bash
curl -X GET --header 'Authorization: eyJ0eXAiOiJKV1QiLCxxxxxxxxxxxxxxxxx' 'https://api.chynge.com/v1/country'
```

```bash
[
  {
    "country": "Indonesia",
    "countryCode": "ID"
  },
  {
    "country": "Malaysia",
    "countryCode": "MY"
  },
  {
    "country": "Singapore",
    "countryCode": "SG"
  }
]
```

When you're using our interactive API documentation, `access_token` is
the value that you want to copy to the api_key input in the 'Authorize'
before you do the 'try it out'.

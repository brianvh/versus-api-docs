# Game Session

## Request New Session Seed

```shell
curl -X GET http://versus.dev/api/v2/games/:game_uuid
  /session?developer_uuid=<developer_uuid>
```

> Returns a 401 with JSON following this structure:

```json
{ "session": { "seed": "a random genreated hash" } }
```

### HTTP Request

`GET /api/v2/games/:game_uuid/session/`

### Query Parameters

Parameter | Required? | Description
--------- | --------- | -----------
developer_uuid | Y | Versus ID of the Game Developer/Publisher.


### Error Responses

Reason | Code | Error Message
------ | ---- | -------------
:developer_uuid missing | 400 | developer_uuid is missing
:developer_uuid incorrect | 404 | Invalid Developer


## Generating the Token Value

> Compute the SHA1 hash of the following JSON-ish formatted string:

```ruby
'{"uuid":game_uuid,"secret_key":api_secret_key,"seed":seed}'
```

> NOTE: The order of the key/value pairs, and the lack of spaces, is significant.

Authentication requires a `token`, generated separately on the API client and server.

### Token Generation Parameter Values
Value Name | Provided By
---------- | -----------
game_uuid | The Versus identifier of the Game to which you want to authenticate.
api_secret_key | The Versus API Secret for the game's Provider.
seed | The `seed` value provided by the above GET endpoint.

## Verify Session Token

```shell
curl -X GET http://versus.dev/api/v2/games/:game_uuid
  /session?developer_uuid=<developer_uuid>&token=<token>
```

> Returns a 200 with JSON following this structure:

```json
{
  "session": {
    "expires": "expiration-timestamp",
    "state": "active"
  }
}
```

`GET /api/v2/games/:game_uuid/session/`

### Query Parameters

Parameter | Required? | Description
--------- | --------- | -----------
developer_uuid | Y | Versus ID of the Game Developer/Publisher.
token | N | Currently active token value.


### Error Responses

Reason | Code | Error Message
------ | ---- | -------------
:developer_uuid missing | 400 | developer_uuid is missing
:developer_uuid incorrect | 404 | Invalid Developer
:token incorrect, expired or missing | 401 | Same response as above GET request.

## Activate Session Token

```shell
curl -X PUT .../api/v2/games/:game_uuid/session \
  -d '{
    "developer_uuid": "<developer_uuid>",
    "token": "<token>"
  }'
```

> Returns a 200 with JSON following this structure:

```json
{
  "session": {
    "expires": "expiration-timestamp",
    "state": "active"
  }
}
```

`PUT /api/v2/games/:game_uuid/session/`

### Request Parameters

Parameter | Required? | Description
--------- | --------- | -----------
developer_uuid | Y | Versus ID of the Game Developer/Publisher.
token | Y | Just generated (aka. pending) token value.


### Error Responses

Reason | Code | Error Message
------ | ---- | -------------
:developer_uuid missing | 400 | developer_uuid is missing
:developer_uuid incorrect | 404 | Invalid Developer
:token missing | 400 | token is missing
:token not a pending token | 401 | Authentication Seed Required

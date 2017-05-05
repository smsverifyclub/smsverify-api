[![Docs](http://img.shields.io/badge/API-v1-00aced.svg?style=flat-square)](https://github.com/smsverifyclub/smsverify-api)

## API Documentation

>This API is useful for developers who want to consume the services of SMS Verify Club.

### Introduction

**Base URL:**

`https://api.smsverify.club`

**API Characteristics:**

- **JSON:** data back-and-forth is formatted in JSON
- **Status:** responses are sent back with sensible status codes and messages
- **Fully Authenticated:** API key is required on every request

### HTTP Statuses

```
200 - indicates that the request was fulfilled successfully and that no error was encountered.
4XX - indicates that either you did not authenticate correctly, you do not have authorization for the particular resource, that the object you are requesting does not exist, or that your request is malformed.
500 - indicates a serverside issue, contact support
```

### Response

Responses will be sent in the form:

```js
{
  "status": 200,
  message: "OK"
  ...
}
```

Where status is the HTTP response code, message is the response and addtional useful information denoted by the three dots.

### API Authentication

#### Getting Your API Key

Your API key can be found in your registration email.

#### Making Requests

All parameters must be sent as a query string.

You must follow the order of flow when making requests:

```

1. Check if balance is more than one credit.

2. Order a phone number.

3. Set a timeout of atleast 35 seconds (to be on the safe side)

4. Retrieve the sms code upon timeout.

```

### Endpoints

- `GET /balance`


Param | Description 
--- | --- 
**api_key** | Your API key


If successful, response is returned in the form:

```js
{
  "status": 200,
  "message": "OK",
  "credit": {YOUR_CREDIT_BALANCE}
}
```


- `GET /order`


Param | Description 
--- | --- 
**api_key** | Your API key
**service** | Service name as displayed on the table

_Do not forget to use a capital letter at the start of the service name, eg "Telegram"_


If successful, response is returned in the form:

```js
{
  "status": 200,
  "message": "Successfully acquired number",
  "number": {PHONE_NUMBER},
  "id": {ORDER_ID}
}
```


- `GET /smscode`

_Rememberto set a timeout of atleast 35 seconds in order to be 90%+ sure to receive the sms code, failure to do so will result in a null error. This is beacuse we use a GSM module which isn't as fast as receiving and trassmitting messages like VOIP. _


Param | Description 
--- | --- 
**api_key** | Your API key
**service** | Service name as displayed on the table
**id** | Unique identifier of order obtained in previous step

_Do not forget to use a capital letter at the start of the service name, eg "Telegram"_


If successful, response is returned in the form:

```js
{
  "status": 200,
  "message": "OK",
  "number": {PHONE_NUMBER},
  "sms": {SMS_VERIFICATION_CODE},
  "text": {COMPLETE_SMS_MESSAGE}
}
```

_if you receive an object whose values contain "null", it means that either the sms hasn't come through or id doesn't exist._


> Copyright © 2017 [SMS Verify Club](https://github.com/smsverifyclub)



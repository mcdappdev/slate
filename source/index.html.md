---
title: Vapor Template API Reference

language_tabs:
  - shell

toc_footers:
  - <a href='https://github.com/mcdappdev/Vapor-Template'>Template</a>
  - <a href='https://github.com/mcdappdev/Vaporize'>Vaporize</a>

search: true
---

# Introduction

Welcome to the docs for mcdappdev's Vapor Template! 

These docs will cover how to use the endpoints that are included with the template. 

**Note:** All endpoints are hosted at /api/v1/. Make sure to replace the url in the shell examples with localhost or your API URL.

# Authentication

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: Bearer API_TOKEN"
```

> Make sure to replace `API_TOKEN` with your API key.

To authorize, you must register or login. But once you're authenticated, make sure that you pass a `API_TOKEN` to the `Authorization` header, as well as the `Bearer` keyword.:

# User Functions

## Login

```shell
  curl -i \
    -H "Accept: application/json" \
    -X POST -d "email":"email@email.com","password":"password" \
    /login
```

> The above command returns JSON structured like this:

```json
{
  "admin": false,
  "email": "email@email.com",
  "id": 2,
  "name": "Person's name",
  "token": "53i8yqt8ap0pEJJ9E0FnPQ"
}
```

This endpoint logs in a user

### HTTP Request

`POST /login`

### Status Codes
Code | Meaning
---- | -------
200  | User Returned
403  | Invalid Credentials
500  | Internal Error

### Parameters

Parameter | Default | Description
--------- | ------- | -----------
email     |         | The user's email
password  |         | The user's unhashed password

## Register

```shell
  curl -i \
    -H "Accept: application/json" \
    -X POST -d "name":"name","email":"email@email.com","password":"password" \
    /register
```

> The above command returns JSON structured like this:

```json
{
  "admin": false,
  "email": "email@email.com",
  "id": 2,
  "name": "Person's name",
  "token": "53i8yqt8ap0pEJJ9E0FnPQ"
}
```

This endpoint registers a user

### HTTP Request

`POST /register`

### Status Codes
Code | Meaning
---- | -------
200  | User Returned and Saved
400  | Invalid Data
500  | Internal Error

### Parameters

Parameter | Default | Description
--------- | ------- | -----------
email     |         | The user's email
password  |         | The user's unhashed password
name      |         | The user's name

## Me

```shell
  curl -i \
    -H "Accept: application/json", "Authorization": "Bearer YOUR_TOKEN_HERE" \
    /me
```

> Make sure to replace `YOUR_TOKEN_HERE` with the user's token. The above command returns JSON structured like this:

```json
{
  "admin": false,
  "email": "email@email.com",
  "id": 2,
  "name": "Person's name",
  "token": "53i8yqt8ap0pEJJ9E0FnPQ"
}
```

This endpoint returns the current user

### HTTP Request

`GET /me`

### Status Codes
Code | Meaning
---- | -------
200  | User Returned
500  | Internal Error

## Update Me

> Any combination of parameters can be passed into this function and all of them will be validated and updated, with the exception of id, token and password. password can be updated using the /password endpoint documented below.

```shell
  curl -i \
    -H "Accept: application/json", "Authorization": "Bearer YOUR_TOKEN_HERE" \
    -X PATCH -d "name":"new name","email":"newemail@email.com" \
    /me
```

> The above command returns JSON structured like this:

```json
{
  "admin": false,
  "email": "newemail@email.com",
  "id": 2,
  "name": "new name",
  "token": "53i8yqt8ap0pEJJ9E0FnPQ"
}
```

This endpoint updates the current user

### HTTP Request

`PATCH /me`

### Status Codes
Code | Meaning
---- | -------
200  | User Updated, Returned
400  | Email Taken
500  | Internal Error

### Parameters

Parameter | Default | Description
--------- | ------- | -----------
email     |         | The user's email
name      |         | The user's name

## Update Password

```shell
  curl -i \
    -H "Accept: application/json", "Authorization": "Bearer YOUR_TOKEN_HERE" \
    -X PATCH -d "oldPassword":"oldpassword","newPassword":"newPassword" \
    /me
```

> The above command returns JSON structured like this:

```json
{
  "admin": false,
  "email": "newemail@email.com",
  "id": 2,
  "name": "new name",
  "token": "53i8yqt8ap0pEJJ9E0FnPQ"
}
```

This endpoint updates the current user's password

### HTTP Request

`PATCH /password`

### Status Codes
Code | Meaning
---- | -------
200  | User Updated, Returned
401  | Incorrect `oldPassword`
500  | Internal Error

### Parameters

Parameter   | Default | Description
----------  | ------- | -----------
oldPassword |         | The user's old, unhashed password
newPassword |         | The user's new, unhashed password
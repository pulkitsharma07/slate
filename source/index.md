---
title: Print-Square API reference

toc_footers:
  - <a href='http://github.com/tripit/slate'>Documentation Powered by Slate</a>

search: true
---

<!---

        INTRODUCTION

-->


# Introduction

Welcome to the Print-Square API reference


<!---

        USER SIGNUP

-->

# User Signup

## Signup with Facebook

> Make a `POST` request to `/api/v1/user/new ` :

```shell
curl -X POST --data "provider=fb&token=facebook_token" "http://someserver.com/api/v1/user/new"

```
> Make sure to replace `facebook_token` with the actual token value


> The above command (if successful) returns JSON structured like this:

```json
{
    "message": {
        "api_key": "38945b04ab19ae4088b06858468bb4fe",
        "created_at": "2015-08-19T06:51:57.367Z",
        "email": "avastpulkit@gmail.com",
        "first_name": "Pulkit",
        "id": 1,
        "last_name": "ShaRma",
        "mobile": null,
        "password_hash": null,
        "updated_at": "2015-08-19T06:51:57.367Z",
        "verified": true
    },
    "status": "successful"
}
```
>If the above command is unsuccessful:

```json
{
    "message": [
        "Invalid Token"
    ],
    "status": "failed"
}
```
`POST /api/v1/user/new`

### Query Parameters

Parameter | Description
--------- | -----------
provider | set to `fb` for facebook login/signup
token | `access_token` provided by facebook



## Signup with Email or Mobile

> Make a `POST` request to `/api/v1/user/new ` :

```shell
curl -X POST --data "provider=email&email=USER_EMAIL&password=USER_PASSWORD&first_name=FIRST_NAME&last_name=LAST_NAME" "http://localhost:3000/api/v1/user/new"
```
> Make sure to replace `USER_EMAIL` , `USER_PASSWORD` ,`FIRST_NAME` , `LAST_NAME` with actual values

> The above command returns JSON structured like this:

```json
{
    "message": {
        "api_key": "6e29d562691b4f20713d6465bfab09e9",
        "created_at": "2015-08-19T07:15:40.682Z",
        "email": "avastpulkit@gmail.com",
        "first_name": "Pulkit",
        "id": 2,
        "last_name": "Sharma",
        "mobile": null,
        "password_hash": "$2a$10$rBYpytFcKskPAzyEYnbRkeeiWBJ6ttqU.TVBe6VbhW.mFWa.O35ju",
        "updated_at": "2015-08-19T07:15:40.682Z",
        "verified": false
    },
    "status": "successful"
}
```

>If the command fails, the following object is returned:


```json
{
    "message": [
        "Email has already been taken"
    ],
    "status": "failed"
}
```
`POST /api/v1/user/new`

### Query Parameters

Parameter | Description
--------- | -----------
provider | set to `email` or `mobile` accordingly
email | the `email address` of the user , if present
mobile | the `mobile number` of the user , if present
password | the `password`
first_name | `first name` of the user
last_name | `last name` of the user

<aside class="warning">If the email/mobile is already registered (Even if by a facebook account) , then the above query will fail"</aside>




<!---

        USER LOGIN
-->


# User Login

## Login/Signup with Facebook

> Make a `POST` request to `/api/v1/user/login` :

```shell
curl -X POST --data "provider=fb&token=facebook_token" "http://someserver.com/api/v1/user/login"

```
> Make sure to replace `facebook_token` with the actual token value


> The above command (if successful) returns JSON structured like this:

```json
{
    "message": {
        "api_key": "b19b866f2ec776f14da8f24f7a13c286",
        "created_at": "2015-08-19T07:45:10.567Z",
        "email": "avastpulkit@gmail.com",
        "first_name": "Pulkit",
        "id": 4,
        "last_name": "ShaRma",
        "mobile": null,
        "password_hash": null,
        "updated_at": "2015-08-19T07:45:10.567Z",
        "verified": true
    },
    "status": "successful"
}
```
>If the above command is unsuccessful:

```json
{
    "message": [
        "Invalid Token"
    ],
    "status": "failed"
}
```
`POST /api/v1/user/login`


<aside class="notice">Login also creates a new `fb` user in the database (if one doesn't exist).<bold>So essentially, you can use login to signup as well as login a Facebook user</bold></aside>

### Query Parameters

Parameter | Description
--------- | -----------
provider | set to `fb` for facebook login/signup
token | `access_token` provided by facebook




## Login with Email or Mobile

> Make a `POST` request to `/api/v1/user/login ` :

```shell
curl -X POST --data "provider=email_mobile&email_mobile=USER_EMAIL_OR_MOBILE&password=USER_PASSWORD" 
"http://localhost:3000/api/v1/user/login"
```
> Make sure to replace `USER_EMAIL_OR_MOBILE` , `USER_PASSWORD` with actual values

> The above command returns JSON structured like this:

```json
{
    "message": {
        "api_key": "6e29d562691b4f20713d6465bfab09e9",
        "created_at": "2015-08-19T07:15:40.682Z",
        "email": "avastpulkit@gmail.com",
        "first_name": "Pulkit",
        "id": 2,
        "last_name": "Sharma",
        "mobile": null,
        "password_hash": "$2a$10$rBYpytFcKskPAzyEYnbRkeeiWBJ6ttqU.TVBe6VbhW.mFWa.O35ju",
        "updated_at": "2015-08-19T07:15:40.682Z",
        "verified": false
    },
    "status": "successful"
}
```


>If the command fails, the following object is returned:


```json
{
    "message": "Invalid credentials",
    "status": "failed"
}

```
`POST /api/v1/user/login`

<aside class="notice">Users registered with email or mobile can be logged in using this endpoint. Provider = email_mobile</aside>


Parameter | Description
--------- | -----------
provider | set to `email_mobile`
email_mobile | `email` or `mobile` of the user to login
password | the `password`



<!---

        AUTHENTICATION

-->

# Authentication

> Example Authorization:

```shell
curl --data "api_key=THE_API_KEY" "api_endpoint_here"  
```

> Make sure to replace `THE_API_KEY` with the API key.


Authentication is only required after a *User* is successfully logged in.

When a *User* is logged in , you will be provided with an hexadecimal `api_key`.
Once you have the `api_key` , you will need to send that `api_key` for each request concerned with that *User* to authorize.

<aside class="notice">
You must replace <code>THE_API_KEY</code> with the API key.
</aside>


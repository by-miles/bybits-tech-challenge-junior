## By Bits Code Challenge
By Bits have a Policy API which handles car insurance policies for customers. Don't worry, we don't expect you to know the in's and out's of car insurance. But here are some useful definitions which may be of some help.

**Useful definitions**

* A **policy** is an agreement or contract between the car insurance provider and the customer who has decided to purchase car insurance.
* A **policy holder** is the customer, owner of the car and the owner of the policy.

## Task

Using the [Policy API](#policy-api) endpoints described below, your task is create a simple web application with a login screen which takes a username and password. Once authorised, it will navigate the user to another page which will display policy details.

A wireframe and user story are provided below as a guide.

### Wireframe

<img src="tech-challange-wireframe.png" />

### User Story

As a policy holder

I can login successfully and view my current policy information

So that I can view my policy details

### Notes

* We use React, however, choose the technical stack that you are most comfortable with.
* You are free to use any 3rd party libraries to assist you in this task.
* You are not expected to develop anything outside of the wireframe and user story described above.
* You are free to design the user interface to your liking or what you think is best.
* If you have experience in testing, please do add any tests where you think are appropriate.


### Time

You are free to spend as little or as much time as you wish to complete this challenge to a level of your satisfaction. At the same time, we do not expect candidates to spend days and weeks on this task.

As a guide, this task can typically take anywhere from 2 to 6 hours, based on skill level.

If you go over that time, it does not mean you will be penalised. 
We appreciate that your time is valuable and therefore, to help us assess your code submission accordingly, it's important to include how long you spend as described in the [How to submit your application](#how-to-submit-your-application) section.


## How to submit your application

1. Create a GitHub repository and upload your code.
2. Provide a README.md in your repository which includes:
    * Any notes, assumptions and decisions you have made.
    * An estimate of how long you spent on this task.
    * If you ran out of time or wanted to spend more time, what would you have liked to have done?
3. Email us a link to this repository.

  

## Policy API 

This Policy API is a mock API and returns dummy data.

We are asking candidates to focus and use two API endpoints, [Login](#login) and [Policy details](#policy-details). 

### Login

This endpoint validates a username and password and returns an `access_token`. This can then be used for all other subsequent API requests such as [Policy details](#policy-details).

**Http Request**
```http
POST https://api.bybits.co.uk/auth/token
HTTP Headers:
environment: mock
Content-type: application/json
```

**Example POST Body**

```json
{
	"username":"testuser",
	"password":"EbpucVzUP5cvsYha0E9i",
	"type":"USER_PASSWORD_AUTH"
}
```

**Parameters**
* `username` - This is the username of a policy holder. As this is a Mock API, this can be any value.
* `password` - This is the password of a policy holder. As this is a Mock API, this can be any value.
* `type` - This must be set to `USER_PASSWORD_AUTH`.


**Example response**
```json
{
    "username": "Jacquelyn.Simonis",
    "session": "yJraWQiOiJweUs2RHhFak05SXhnU3",
    "type": "USER_PASSWORD_AUTH",
    "code": "116567",
    "access_token": "MuYW1hem9uYXdzLmNvbVwvZXUtd2VzdC0zX3JkdldSMGs",
    "refresh_token": "MuYW1hem9uYXdzLmNvbVwvZXUtd2VzdC0zX3JkdldSMGs"
}
```

As this is a Mock API, the response returned will be dummy data.
Take note of the `access_token` value from the response above. This will be needed in the Authorization header as described in the [Policy details](#policy-details) section.

**Example Curl Command**

```shell
curl --request POST --url https://api.bybits.co.uk/auth/token --header "environment: mock" --data "{"username":"testuser","password":"EbpucVzUP5cvsYha0E9i","type":"USER_PASSWORD_AUTH"}"
```

### Policy details

Returns a detailed policy object. 

**Important note:** This API endpoint must be accessed by providing an additional **Authorization** request header using the bearer authentication scheme. Like so:

```
Authorization: Bearer {access_token}
```

The `{access_token}` value can be found from the Login response as described earlier.

```
Authorization: Bearer MuYW1hem9uYXdzLmNvbVwvZXUtd2VzdC0zX3JkdldSMGs
```

**Http Request**
```http
GET https://api.bybits.co.uk/policys/details
HTTP Headers:
environment: mock
Authorization: Bearer MuYW1hem9uYXdzLmNvbVwvZXUtd2VzdC0zX3JkdldSMGs
Content-type: application/json
```

**Example response**
```json
{
  "policy": {
    "compulsory_excess": 100,
    "voluntary_excess": 100,
    "address": {
      "line_1": "Flat 1, 11 The Street",
      "line_2": "Little Hampton",
      "line_3": "Burton-on-the-water",
      "county": "Avon",
      "city": "Stroud",
      "country": "GB",
      "postcode": "W53TR"
    },
    "usage": "SDP",
    "cover": "Comprehensive",
    "auto_renew": true,
    "start_date": 1599567165,
    "end_date": 1599567165,
    "billing_day_date": 20,
    "underwriter": "Zurich",
    "underwriter_ref": "AXABM000001",
    "product_name": "PBMYD",
    "policy_year": 1,
    "created_at": 1599567165,
    "policy_ref": "apple-orange-pear"
  },
  "proposer": {
    "title": "003",
    "first_names": "Dave",
    "last_names": "Jones",
    "email": "dave@jones.com",
    "mobile_number": "+447999000011",
  ...
```


**Example Curl command**
```shell
curl --request GET --url https://api.bybits.co.uk/policys/details --header "environment: mock" --header "authorization beaer MuYW1hem9uYXdzLmNvbVwvZXUtd2VzdC0zX3JkdldSMGs"
```





Best of luck.



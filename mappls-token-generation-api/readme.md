[<img src="https://about.mappls.com/about/images/MAPPLS-MapmyIndia-logo.png" height="40"/> </p>](https://about.mappls.com/api/)

# Token Generation API

## Introduction

This API is required to generate tokens authorize the oAuth 2 based APIs. <br> Hence, the developer would need to send a request for access token using their client_id and client_secret to the Token Generation API. <br>Once validated from the OAuth API, the access_token and the token_type need to be sent as Authorization header with the value: `{token_type} {access_token}`
    ```
    Authorization: “token_type access_token”. 
    ```


## Input URL

```jsx
https://outpost.mappls.com/api/security/oauth/token
``` 

## Method

POST

## Request Type

`Content-Type: application/x-www-form-urlencoded`

## Response Type

`Content-Type: application/json`

## Request Body


### Mandatory Parameters


1.	**`grant_type`** (string) : 	The grant type applicable to the token. By default, it is set at "client_credentials".<br>
    Example:
    - `client_credentials` <br><br>

2.	**`client_id`** (string) : 	The client ID provided to thec client for accessing oAuth 2 based APIs. There is no fixed length for client id.<br>
    Example:
    - `33Okryxxxxxxxxxxxxxxx-yyyyyyyyyyyyyy-zzzzzzzzzzz` <br><br>

3.	**`client_secret`** (string) : 	The client secret provided to thec client for accessing oAuth 2 based APIs. There is no fixed length for client secret.<br>
    Example:
    - `lxxxxx-iyyyyyyyyyyyyyYYyyyy-ZzzZzzzz-3xyxyxyXYxyxy=` <br><br>


## Response Parameters

1.	`access_token`(string): The access token provided by the API for accessing OAuth 2 based APIs from Mappls. <br>
    Example: 
    - `0XXXXXXf-dXX0-4XX0-8XXa-eXXXXXXXXXX6`<br><br>
2. `token_type` (string): Type of the token returned by the API.<br>
    Example: 
    - `bearer`<br><br>
3. `expires_in` (number): period in seconds from generation after which the token generated will expire.<br>
    Example: 
    - `86499`<br><br>
4. `scope` (string): The scope of the token applicable. <br>
    Example: 
    - `READ`<br><br>
5. `project_code` (string): The project code/ID for which the token was generated. This is helpful in identifying if there are multiple projects in an account of Mappls API console. <br>
    Example: 
    - `prj1234567890987654321`<br><br>
6. `client_id` (string): client ID which was used in generation of the token. In case there are multiple pairs of client ID + Client secret within a project, this will help in identifying which pair was used for generation of token.<br>
    Example: 
    - `33Okryxxxxxxxxxxxxxxx-yyyyyyyyyyyyyy-zzzzzzzzzzz`<br><br>

 
## Sample cURL Request

```jsx
curl --location --request POST 'https://outpost.mappls.com/api/security/oauth/token' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--header 'User-Agent: iamdarkseid' \
--data-urlencode 'grant_type=client_credentials' \
--data-urlencode 'client_id=33Okryxxxxxxxxxxxxxxx-yyyyyyyyyyyyyy-zzzzzzzzzzz' \
--data-urlencode 'client_secret=lxxxxx-iyyyyyyyyyyyyyYYyyyy-ZzzZzzzz-3xyxyxyXYxyxy='
```

## Sample Response
```json
{
  "access_token": "0XXXXXXf-dXX0-4XX0-8XXa-eXXXXXXXXXX6",
  "token_type": "bearer",
  "expires_in": 86499,
  "scope": "READ",
  "project_code": "prj1234567890987654321",
  "client_id": "33Okryxxxxxxxxxxxxxxx-yyyyyyyyyyyyyy-zzzzzzzzzzz"
}
```


## Response Codes (as HTTP response codes)

#### Success
1. 200: To denote a successful API call. 
2. 204: To denote the API was a success but no results were found. 

#### Client-Side Issues 

3. 400: Bad Request, User made an error while creating a valid request. 
4. 401: Unauthorized, Some extra invalid authorization object is being used to send a request.
5. 403: Forbidden.

#### Server-Side Issues

6. 500: Internal Server Error, the request caused an error in our systems.
7. 503: Service Unavailable, during our maintenance break or server downtimes.


## Response Messages (as HTTP response messages)

1.	200: Success.
2.	201: Created. 
3.	204: No matches were found for the provided query. 
4.	400: Something’s just not right with the request. 
5.	401: Unauthorized. 
6.	403: Forbidden. 
7.	500: Something went wrong. 
8.	503: Maintenance Break. 
9.	410 : Deleted
10.	422 : Unprocessable entity
11.	412 : Precondition Failed
12.	428 : Precondition Required.


<br>

For any queries and support, please contact: 

[<img src="https://about.mappls.com/images/mappls-logo.svg" height="40"/> </p>](https://about.mappls.com/api/)
Email us at [apisupport@mappls.com](mailto:apisupport@mappls.com)


![](https://www.mapmyindia.com/api/img/icons/support.png)
[Support](https://about.mappls.com/contact/)
Need support? contact us!

<br></br>
<br></br>

[<p align="center"> <img src="https://www.mapmyindia.com/api/img/icons/stack-overflow.png"/> ](https://stackoverflow.com/questions/tagged/mappls-api)[![](https://www.mapmyindia.com/api/img/icons/blog.png)](https://about.mappls.com/blog/)[![](https://www.mapmyindia.com/api/img/icons/gethub.png)](https://github.com/Mappls-api)[<img src="https://mmi-api-team.s3.ap-south-1.amazonaws.com/API-Team/npm-logo.one-third%5B1%5D.png" height="40"/> </p>](https://www.npmjs.com/org/mapmyindia) 



[<p align="center"> <img src="https://www.mapmyindia.com/june-newsletter/icon4.png"/> ](https://www.facebook.com/Mapplsofficial)[![](https://www.mapmyindia.com/june-newsletter/icon2.png)](https://twitter.com/mappls)[![](https://www.mapmyindia.com/newsletter/2017/aug/llinkedin.png)](https://www.linkedin.com/company/mappls/)[![](https://www.mapmyindia.com/june-newsletter/icon3.png)](https://www.youtube.com/channel/UCAWvWsh-dZLLeUU7_J9HiOA)




<div align="center">@ Copyright 2022 CE Info Systems Ltd. All Rights Reserved.</div>

<div align="center"> <a href="https://about.mappls.com/api/terms-&-conditions">Terms & Conditions</a> | <a href="https://about.mappls.com/about/privacy-policy">Privacy Policy</a> | <a href="https://about.mappls.com/pdf/mapmyIndia-sustainability-policy-healt-labour-rules-supplir-sustainability.pdf">Supplier Sustainability Policy</a> | <a href="https://about.mappls.com/pdf/Health-Safety-Management.pdf">Health & Safety Policy</a> | <a href="https://about.mappls.com/pdf/Environment-Sustainability-Policy-CSR-Report.pdf">Environmental Policy & CSR Report</a>

<div align="center">Customer Care: +91-9999333223</div>
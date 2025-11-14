[<img src="https://about.mappls.com/images/mappls-logo.svg" height="40"/> </p>](https://about.mappls.com/api/)

# Custom Search - List Record API


## Introduction

Get all records API returns the list of all the live records added by the user with pagination. User can apply various filters like to get the expired records, modified date, create date etc. 

## URL

```html
https://search.mappls.com/search/byod/list?
```

## HTTPS Method

GET

## Getting Access

Before using the API in the your solution, please ensure that the related access is enabled in the [Mappls Console](https://auth.mappls.com/console/), within your app - be it for Mobile OR Web or Cloud integration.

1. Copy and paste the key from your `credentials` section from your API [keys](https://auth.mappls.com/console/) into the `access_token` query parameter.
    - Your static key can be secured by whitelisting its usage for particular IPs (in case of cloud app usage) OR a set of domains (in case of a web app)
    - Your static key obtained from your Console is to be passed as a query parameter: `access_token`.

## Authentication Object - `access_token` mandatory query parameter.

-  `access_token`: "hklmgbwzrxncdyavtsuojqpiefrbhqplnm".

## Response Type

`application/json`


## Response Codes

### Success

1. 200: To denote a successful API call. 
2. 204: To denote the API was a success but no results we’re found. 

### Client-Side Issues

3.	400: Bad Request, User made an error while creating a valid request.
4.	401: Unauthorized, Developer’s key is not allowed to send a request.
5.	403: Forbidden, Developer’s key has hit its daily/hourly limit.

### Server-Side Issues

6.	500: Internal Server Error, the request caused an error in our systems.
7.	503: Service Unavailable, during our maintenance break or server downtimes.

## Response Messages

1. 200: Success. 
2. 204: No matches we’re found for the provided query. 
3. 400: Something’s just not right with the request. 
4. 401: Access Denied. 
5. 403: Forbidden, Services for this key has been suspended due to daily/hourly transactions limit. 
6. 500: Something went wrong. 
7. 503: Maintenance Break. 

## Request Parameters


### Mandatory Parameters

There is no Mandatory parameter to get the list of records.
<br><br>

### Optional Parameters

1. *`recordType (string)`* : This parameter will ensure that only records with a certain record type are listed. A user can be used multiple recordType and there is no limit on the number of record types to be given in the pa rameter. Multiple record types can be provided using a semicolon (;) as a separator. e.g. recordType=chariotTest13;chariotTest12;chariotTest15 
2. *`createdTime (number)`* : This is an epoch value in seconds. The filter acts as follows: All records whose creation time is ‘greater than’ the provided input time here are responded back in results. Example: createdTime=1628855941 
3. *`modifiedTime (number)`* : This is an epoch value in seconds. The fil ter acts as follows: All records whose modified time is ‘greater than’ the provided input time here are responded back in results. Example: modifiedTime=1628855941 
4. *`page (integer)`*: Provides the number of the page to provide results from. 
5. *`includeExpired (valueless)`*: By default, only the active recordIds are returned in the response. This parameter includes the expired record ids as well. 

## Response Parameters
1. *`records (array)`* : Array of records each containing: 
    - *`recordId`* : The uniquely identifier ID of the record. 
2. *`pageInfo (object)`* : A page info object containing: 
   - pageCount: Count of the page. 
   - totalHits : Total number of the hits. 
   - totalPages: Total number of the pages. 
   - pageSize : Size of the page.

## Sample cURL Request

### Sample
Record added with geographical coordinate values.
```curl
curl --location 'https://search.mappls.com/search/byod/list?access_token=hklmgbwzrxncdyavtsuojqpiefrbhqplnm'

```
<br> <br>


## Sample Response

```
{
    "recordIds": [
        {
            "recordId": "CT0076"
        },
        {
            "recordId": "CT0059"
        },
        {
            "recordId": "CT0074"
        },
        {
            "recordId": "CT0078"
        },
        {
            "recordId": "CT0075"
        },
        {
            "recordId": "CT0077"
        },
        {
            "recordId": "CT0060"
        },
        {
            "recordId": "CT0056"
        },
        {
            "recordId": "CT0057"
        },
        {
            "recordId": "CT0058"
        }
    ],
    "pageInfo": {
        "pageCount": 1,
        "totalHits": 12,
        "totalPages": 2,
        "pageSize": 10
    }
}
```


<br><br>

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




<div align="center">@ Copyright 2025 CE Info Systems Ltd. All Rights Reserved.</div>

<div align="center"> <a href="https://about.mappls.com/api/terms-&-conditions">Terms & Conditions</a> | <a href="https://about.mappls.com/about/privacy-policy">Privacy Policy</a> | <a href="https://about.mappls.com/pdf/mapmyIndia-sustainability-policy-healt-labour-rules-supplir-sustainability.pdf">Supplier Sustainability Policy</a> | <a href="https://about.mappls.com/pdf/Health-Safety-Management.pdf">Health & Safety Policy</a> | <a href="https://about.mappls.com/pdf/Environment-Sustainability-Policy-CSR-Report.pdf">Environmental Policy & CSR Report</a>

<div align="center">Customer Care: +91-9999333223</div>
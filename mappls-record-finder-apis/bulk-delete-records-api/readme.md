[<img src="https://about.mappls.com/images/mappls-logo.svg" height="40"/> </p>](https://about.mappls.com/api/)

# Custom Search - Bulk Delete Records API


## Introduction

This API allows one to delete added records to the Custom search database. These records are used to perform Nearby Searches on the different types of user records that are stored within custom search database.
This API allows one to `delete upto 100 records in a one` request.

## URL

```html
https://search.mappls.com/search/byod/bulk
```

## HTTPS Method

POST

## Getting Access

Before using the API in the your solution, please ensure that the related access is enabled in the [Mappls Console](https://auth.mappls.com/console/), within your app - be it for Mobile OR Web or Cloud integration.

1. Copy and paste the key from your `credentials` section from your API [keys](https://auth.mappls.com/console/) into the `access_token` query parameter.
    - Your static key can be secured by whitelisting its usage for particular IPs (in case of cloud app usage) OR a set of domains (in case of a web app)
    - Your static key obtained from your Console is to be passed as a query parameter: `access_token`.

## Authentication Object - `access_token` mandatory query parameter.

-  `access_token`: "hklmgbwzrxncdyavtsuojqpiefrbhqplnm".

## Request Content Type

Content-Type: `application/json`

## Response Type

`application/json`


## Response Codes

### Success

1. 201: To denote a successful data created.

### Client-Side Issues

2.	400: Bad Request, User made an error while creating a valid request.
3.	401: Unauthorized, Developer’s key is not allowed to send a request.
4.	403: Forbidden, Developer’s key has hit its daily/hourly limit.
5.  409: Conflict.

### Server-Side Issues

7.	500: Internal Server Error, the request caused an error in our systems.
8.	503: Service Unavailable, during our maintenance break or server downtimes.

## Response Messages

1. 200: Deleted.
2. 204: No matches we’re found for the provided query.
3. 400: Something’s just not right with the request.
4. 401: Access Denied.
5. 403: Forbidden, Services for this key has been suspended due to daily/hourly transactions limit.
6. 409: Conflict.
7. 500: Something went wrong.
8. 503: Maintenance Break.

## Request Parameters


### Mandatory Parameters

1. **`recordIds (array)`** : Array of record IDs(string) > Unique identifier of each record from the client.



## Sample cURL Request

### Sample 1
Record added with geographical coordinate values.
```curl
curl --location 'https://search.mappls.com/search/byod/bulk?access_token=hklmgbwzrxncdyavtsuojqpiefrbhqplnm' \
--header 'Content-Type: application/json' \
--data-raw '{
    "recordIds": [
        "IN3410000564",
        "IN2810009299",
        "IN2810001387",
        "IN2810006585",
        "IN3810000003"
    ]
}'
```


## Sample Response

```
{
    "responseCode": 200,
    "message": "Deleted Successfully."
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
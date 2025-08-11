[<img src="https://about.mappls.com/about/images/MAPPLS-MapmyIndia-logo.png" height="40"/> </p>](https://about.mappls.com/api/)
# FEEDBACK API

## Introduction

The API acts as a feedback loop to improve the user's search pattern by incorporating ML based personalization characteristics to further searches. This API is not billable directly; but has transactions limits to avoid abuse.


## Getting Access

Before using the API in the your solution, please ensure that the related access is enabled in the [Mappls Console](https://auth.mappls.com/console/), within your app - be it for Mobile OR Web or Cloud integration.

1. Copy and paste the key from your `credentials` section from your API [keys](https://auth.mappls.com/console/) into the `access_token` query parameter.
    - Your static key can be secured by whitelisting its usage for particular IPs (in case of cloud app usage) OR a set of domains (in case of a web app)
    - Your static key obtained from your Console is to be passed as a query parameter: `access_token`.

## Authentication Object - `access_token` mandatory query parameter.

-  `access_token`: "hklmgbwzrxncdyavtsuojqpiefrbhqplnm".

## URL
```html
https://search.mappls.com/search/places/feedback/json?
```

## Method

#### POST

## Request Body

The request must have a JSON body with the below keys and their data types:

**Note**: Bold Ones are Mandatory, Italic ones are optional parameters.

1.  **`typedKeyword`**: (string) => The string that was searched. Must be 2 characters or more.   
2.  **`selectedEloc`**: (string) => eLoc of the location that was selected. Must be exactly 6 characters.
3. *`selectedLocationName`*: (string) => name of the location that was selected.  
4.  *`apiVersion`*: (string) => version of the API that was used to get the result.    
5.  **`selectedIndex`**: (integer) => the index of the selected object that was returned from the search.    
6.  *`username`*: (string) => the username of the user that’s logged in.    
7.  **`appVersion`**: (double) => the version of the app that was used to make the request.    
8.  *`latitude`*: (double) => the latitude of the location from where the search is made. The latitude must be a double value, must not start with 0 and must not be larger than the longitude.
9. *`longitude`*: (double) => the longitude of the location from where the search is made. The longitude must be a double value, must not start with 0.
  
### Request Headers

1.  **Content-Type:** Defines the type of content being sent to the API. It must be set to **“application/x-www-form-urlencoded”.** Please note: sending any request without it or different than it would lead to a 400: Bad request.
    

### Security Type:
OAuth 2.0 based security using AES 256 and SHA-1.

### Response Type
• JSON: if the user passed in “/json”.  

### Response Codes {as HTTP response code}

**Success:**

1. 201: To denote that the feedback was successfully created.

**Client-Side Issues:**

1. 400: Bad Request, User made an error while creating a valid request or the body of the request is invalid.
2. 401: Unauthorized, Developer’s key is not allowed to send a request with restricted parameters  
3. 403: Forbidden, Developer’s key has hit its daily/hourly limit

**Server-Side Issues:**

1. 500: Internal Server Error, the request caused an error in our systems.  
2. 503: Service Unavailable, during our maintenance break or server downtimes.

### Response Messages {as HTTP response message}

1. 201: Feedback submitted.  
2. 400: Something’s just not right with the request.  
3. 401: Access Denied.  
4. 403: Services for this key has been suspended due to daily/hourly transactions limit. 
5. 500: Something went wrong.  
6. 503: Maintenance Break.

### Response Parameters

The response of this API would be empty. Success would be denoted by the response codes and error would be denoted with the response codes while information on what went wrong with the request in-case of a 400: bad request would be a part of the response headers message.

### Sample cURL Request

```c
curl --location --request POST 'https://search.mappls.com/search/places/feedback/json?access_token=hklmgbwzrxncdyavtsuojqpiefrbhqplnm' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'typedKeyword=hotel' \
--data-urlencode 'selectedEloc=531C42' \
--data-urlencode 'selectedIndex=1' \
--data-urlencode 'appVersion=1.1.1'
```


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




<div align="center">@ Copyright 2025 CE Info Systems Ltd. All Rights Reserved.</div>

<div align="center"> <a href="https://about.mappls.com/api/terms-&-conditions">Terms & Conditions</a> | <a href="https://about.mappls.com/about/privacy-policy">Privacy Policy</a> | <a href="https://about.mappls.com/pdf/mapmyIndia-sustainability-policy-healt-labour-rules-supplir-sustainability.pdf">Supplier Sustainability Policy</a> | <a href="https://about.mappls.com/pdf/Health-Safety-Management.pdf">Health & Safety Policy</a> | <a href="https://about.mappls.com/pdf/Environment-Sustainability-Policy-CSR-Report.pdf">Environmental Policy & CSR Report</a>

<div align="center">Customer Care: +91-9999333223</div>
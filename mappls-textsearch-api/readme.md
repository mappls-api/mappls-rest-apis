[<img src="https://about.mappls.com/about/images/MAPPLS-MapmyIndia-logo.png" height="40"/> </p>](https://about.mappls.com/api/)
# Text Search API

**Easy To Integrate Maps & Location APIs & SDKs For Web & Mobile Applications**

Powered with India's most comprehensive and robust mapping functionalities.
**Now Available**  for Srilanka, Nepal, Bhutan and Bangladesh

You can get your api key to be used in this document here: [https://about.mappls.com/api/](https://about.mappls.com/api/)

# Note 
1. The response listed in the below documentation is ONLY indicative of the overall capabilities of Mappls's Search APIs.
2. Not all response parameters mentioned in the below documentation is assured to be present in all the use-cases. The response of any of the below search API is thus, dependent on the use-case agreed upon between Mappls & it's API consumer.
3. For any further clarifications on what all of the response structure is available for your use case, please contact your business relationship manager or contact Mappls API support.
4. PREMIUM APIs/Parameters are not available for evalulation on signup. To get access, please contact API Support.

## Introduction
Text Search API is a service that aims to provide information about a list of places on the basis of a text string entered by the user. It uses the location information that is provided along with the query to try to understand the request. This API now supports Hindi language so you can now search queries in Hindi too.


## Getting Access

Before using the API in the your solution, please ensure that the related access is enabled in the [Mappls Console](https://auth.mappls.com/console/), within your app - be it for Mobile OR Web or Cloud integration.

1. Copy and paste the key from your `credentials` section from your API [keys](https://auth.mappls.com/console/) into the `access_token` query parameter.
    - Your static key can be secured by whitelisting its usage for particular IPs (in case of cloud app usage) OR a set of domains (in case of a web app)
    - Your static key obtained from your Console is to be passed as a query parameter: `access_token`.

## Authentication Object - `access_token` mandatory query parameter.

-  `access_token`: "hklmgbwzrxncdyavtsuojqpiefrbhqplnm".

## Input Method
GET

## Input URL

[https://search.mappls.com/search/places/textsearch/json?](https://search.mappls.com/search/places/textsearch/json?)

## Request Parameters

### Mandatory Parameters:
1.  **`query`**  (string) e.g. FODCOF, Shoes, Coffee, Versace, Gucci, H&M, Adidas, Starbucks, B130 {POI, House Number, keyword, tag}


### Optional Parameters:
1. *`region`* (string): it takes in the country code. LKA, IND, BTN, BGD, NPL for Sri-Lanka, India, Bhutan, Bangladesh, Nepal respectively. Default is India (IND)
2. *`location`*  {string (latitude[double],longitude[double])}: Provides the location around which the search will be performed. e.g. `location=28.454,77.435`
It is STRONGLY RECOMMENDED to use this parameter for accurate location biased results.
1. *`filter`*  {filter=pin:110020}: Filter parameter helps you restrict the result by mentioning pincode. e.g. `filter=pin:110020`

## Response Parameters

Multiple objects: 

a. suggestedLocations ([object array])

1.  `type` (string): Type of location POI or Country or City.
2. `typeX` (integer): for internal use only.
3. `placeAddress` (string): Address of the location.
4. `eLoc` (string): Place Id of the location 6-char alphanumeric.
5. `placeName` (string): Name of the location.
6. `alternateName` (string): Alternate name of the location.
7. `keywords` (nullable [ string ] ): provides an array of matched keywords or codes.
8. `p` (long integer): for internal use only.
9. `distance` (nullable integer): for internal use only.
10. `orderIndex` (integer): the order where this result should be placed
11. `score` (double): for internal use only.
12. `suggester` (string): for internal use only.
13. `addressTokens` (array of objects): It shows the admin details along with the house address. Address token information is NOT available in generic response; and is RESTRICTED.

b. userAddedLocations ([object array])

1. `eLoc` (string): Place Id of the location 6-char alphanumeric.
2. `placeName` (string): Name of the location.
3. `placeAddress` (string): Address of the location.
4. `type` (string): type of location POI or Country or City (if available)
5. `orderIndex` (integer): the order where this result should be placed
6. `resultType` (string): Type of the result according to user generated content (UGC). Mostly is 'UAP'.
7. `userName` (string): The username of the person who has added this place.

## Response Type

JSON

## Response Codes {as HTTP response code}

### Success:

1. `200`: To denote a successful API call. 
2. `204`: To denote the API was a success but no results we’re found.

### Client-Side Issues:
1. `400`: Bad Request, User made an error while creating a valid request. 
2. `401`: Unauthorized, Developer’s key is not allowed to send a request with restricted parameters. 
3. `403`: Forbidden, Developer’s key has hit its daily/hourly limit

### Server-Side Issues:
1. `500`: Internal Server Error, the request caused an error in our systems. 
2. `503`: Service Unavailable, during our maintenance break or server downtime.


## Sample Input
```html
https://search.mappls.com/search/places/textsearch/json?query=okhla phase 3&region=ind&filter=pin:110020&access_token=hklmgbwzrxncdyavtsuojqpiefrbhqplnm
```

## Sample Response

```json
{
    "suggestedLocations": [
        {
            "type": "POI",
            "typeX": 7,
            "placeAddress": "Sikandra Road, Connaught Place, New Delhi, Delhi, 110001",
            "eLoc": "38FD1E",
            "placeName": "Lady Irwin College",
            "alternateName": "",
            "keywords": [
                "COMCLG"
            ],
            "p": 3493,
            "distance": 0,
            "orderIndex": 1,
            "score": 19905.639213316852,
            "suggester": "placeName",
            "addressTokens": {},
            "richInfo": {}
        }
    ],
    "userAddedLocations": []
}
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
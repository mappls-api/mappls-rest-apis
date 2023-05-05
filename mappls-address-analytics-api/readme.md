[<img src="https://about.mappls.com/about/images/MAPPLS-MapmyIndia-logo.png" height="40"/> </p>](https://about.mappls.com/api/)
# Mappls Address Analytics API 
(erstwhile Address Standardization API)

**Easy To Integrate Maps & Location APIs & SDKs For Web & Mobile Applications**

Powered with India's most comprehensive and robust mapping functionalities.

You can get your api key to be used in this document here: [https://about.mappls.com/api/](https://about.mappls.com/api/)

## Introduction

MapmyIndia's Address Analytics API is a parsing and standardisation engine enabling a complete flow of address cleansing, extraction, validation and standardisation activities.

The engine is trained on MapmyIndia’s Comprehensive Address Directory. Address directory is a unified data product representing India addresses at different level of granularity while keeping the hierarchical sanctity of each address. 
This API supports modular functions (cleansing / parsing / standardization) to utilize the workflow as per the business needs.


## Live Demo

You can also experience this address standardization API through our demo. For experience please [click here](https://mmi.mapmyindia.com/api/addressparser_demo/)

## Getting Access

Before using the API in the your solution, please ensure that the related access is enabled in the [Mappls Console](https://apis.mappls.com/console/), in the same project you set up for the Maps SDK.

1. Copy and paste the generated `access token` from your API [keys](https://apis.mappls.com/console/) available in the dashboard in the sample code for interactive map development.
    - This APIs follow OAuth2 based security.
    - `Access Token` can be generated using Token Generation API.
    - To know more on how to create your access tokens, please use our authorization API URL. More details available [here](https://developer.mappls.com/mapping/tokenGeneration)
    - The `access token` is a valid by default for 24 hours from the time of generation. This can be configured by you in the API console.
2. **`Security Type`**
    
    This APIs follow OAuth2 based security. **To know more on how to create your authorization tokens, please use our authorization token URL. More details available**  [here](https://developer.mappls.com/mapping/tokenGeneration)

## Request Headers

The API leverages OAuth 2.0 based security. Hence, the developer would need to send a request for access token using their client_id and client_secret to the OAuth API. Once validated from the OAuth API, the access_token and the token_type need to be sent as Authorization header with the value: “{token_type} {access_token}”.

-  `Authorization:  “token_type access_token”`.


## Input Method
GET

## Input URL

```html
https://atlas.mapmyindia.com/api/places/addressAnalytics?
```

## Request Parameters

### Mandatory Parameters

 - `address`(string): Address to be cleansed, parsed and standardized. e.g. 237 Okhla industrial estate phase 3 new Delhi, Delhi 110020

### Optional Parameters

Not Applicable

## Response Parameters

1.	`inputAddress` (string): Address given by the user in the request.
2.	`parsedData` (object): 
    1. `parsedTokens` (array of objects) : The address token information tagged from the provided input address, if any are found. Each object contains following two response properties: 
        - `token` (string): The value(s) of the parsed address component. If an address token has more than one value, they are separated by a semicolon (";").
        - `tokenType` (string): the type of the token for this address component. Token type can belong to any one of the following types: 
            - `careOf` (string): Care of (C/O) name present in the input address.
            - `floor` (string): Floor information present in the input address.
            - `buildingNumber` (string): House number information present in the input address.
            - `poi/buildingName` (string): POI or Building Name present in the input address.
            - `street` (string): House number information present in the input address.
            - `landmark` (string): Landmark information present in the input address.
            - `neighbourhood` (string): Locality areas present in the input address.
            - `village` (string): Village name present in the input address.
            - `postOffice` (string): Post offices information present in the input address.
            - `subDistrict` (string): Subdistrict information present in the input address.
            - `district` (string): District information present in the input address.
            - `city` (string): City information present in the input address.
            - `state` (string): State information present in the input address.
            - `pincode` (string): Pincode information present in the input address.
            - `country` (string): Country information present in the input address.    
    2. `remainingAddress` (string): Part of input address left after tagging the token information.
    3. `formattedAddress` (string): Concatenated sequence of the parsed tokens.
4. `standardizedData` (object):
    1. `standardizedTokens` (array of objects): The information tagged, standardized/corrected from the input address as well as additional information in the form of missing components(if applicable) while validating the address.
         - `token` (string): The value(s) of the parsed address component. If an address token has more than one value, they are separated by a semicolon (";").
        - `tokenType` (string): the type of the token for this address component. Token type can belong to any one of the following types: 
            - `careOf` (string): Care of (C/O) name present in the input address.
            - `floor` (string): Floor information present in the input address.
            - `buildingNumber` (string): House number information present in the input address.
            - `poi/buildingName` (string): POI or Building Name present in the input address.
            - `street` (string): House number information present in the input address.
            - `landmark` (string): Landmark information present in the input address.
            - `subSubLocality` (string): Original name of the standardized subsublocality.
            - `subLocality` (string): Original name of the standardized sublocality.
            - `locality` (string): Original name of the standardized locality.
            - `village` (string): Original name of the standardized village.
            - `postOffice` (string): Post offices information present in the input address.
            - `subDistrict` (string): Standardized subdistrict name.
            - `district` (string): Standardized district name.
            - `city` (string): Standardized city name.
            - `state` (string): Standardized state name.
            - `pincode` (string): Standardized pincode information. It can have multiple value seperated by semicolon(";"). In case of multiple values, the first value indicates the parsed pincode as extracted from input address followed by the standardized pincode values.
    2. `remainingAddress` (string): Part of input address left after tagging the admin and other information.
    3. `formattedAddress` (string): Concatenated sequence of the parsed and standardized tokens.

## Response Type

- JSON

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

## Sample Input cURL

```js
curl --location 'https://atlas.mapmyindia.com/api/places/addressAnalytics?address=Hannah%20Sen%20Cottage%2C%20Lady%20Irwin%20College%20Campus%2C%20Sikandra%20Road%2C%20Mandi%20House%2C%20New%20Delhi%20110001' \
--header 'Authorization: bearer 6xxxxxx4-9xxx-xxx7-xxxb-8dxxa7xxxdc' 
```

## Sample Response

```json
{
    "inputAddress": "Hannah Sen Cottage, Lady Irwin College Campus, Sikandra Road, Mandi House, New Delhi 110001",
    "parsedData": {
        "formattedAddress": "Hannah Sen Cottage, Sikandra Road, Lady Irwin College Campus, New Delhi, 110001",
        "remainingAddress": "",
        "parsedTokens": [
            {
                "token": "Mandi House;Hannah Sen Cottage",
                "tokenType": "poi/buildingName"
            },
            {
                "token": "Sikandra Road",
                "tokenType": "street"
            },
            {
                "token": "Lady Irwin College Campus",
                "tokenType": "neighbourhood"
            },
            {
                "token": "New Delhi",
                "tokenType": "city"
            },
            {
                "token": "110001",
                "tokenType": "pincode"
            }
        ]
    },
    "standardizedData": {
        "formattedAddress": "Hannah Sen Cottage, Sikandra Road, Mandi  Lady Irwin College Campus, New Delhi, Delhi, 110001",
        "remainingAddress": "Campus House",
        "standardizedTokens": [
            {
                "token": "Hannah Sen Cottage",
                "tokenType": "poi/buildingName"
            },
            {
                "token": "Sikandra Road",
                "tokenType": "street"
            },
            {
                "token": "110001",
                "tokenType": "pincode"
            },
            {
                "token": "Mandi; Lady Irwin College Campus",
                "tokenType": "locality"
            },
            {
                "token": "New Delhi",
                "tokenType": "city"
            },
            {
                "token": "Delhi",
                "tokenType": "state"
            }
        ]
    }
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




<div align="center">@ Copyright 2023 CE Info Systems Ltd. All Rights Reserved.</div>

<div align="center"> <a href="https://about.mappls.com/api/terms-&-conditions">Terms & Conditions</a> | <a href="https://about.mappls.com/about/privacy-policy">Privacy Policy</a> | <a href="https://about.mappls.com/pdf/mapmyIndia-sustainability-policy-healt-labour-rules-supplir-sustainability.pdf">Supplier Sustainability Policy</a> | <a href="https://about.mappls.com/pdf/Health-Safety-Management.pdf">Health & Safety Policy</a> | <a href="https://about.mappls.com/pdf/Environment-Sustainability-Policy-CSR-Report.pdf">Environmental Policy & CSR Report</a>

<div align="center">Customer Care: +91-9999333223</div>
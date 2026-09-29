[<img src="https://about.mappls.com/images/mappls-logo.svg" height="40"/> </p>](https://about.mappls.com/api/)

# Custom Search - Search Record API


## Introduction

This API allows one to search the records as per specified search criteria from the Custom search database in either nearby search around the provided reference location OR through text search.
The custom Search Record API allows organizations and companies to search the locations based records and entities added as per their custom modules. 

## URL

```html
https://search.mappls.com/search/byod/search?
```

## Input Method

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

7.	500: Internal Server Error, the request caused an error in our systems.
8.	503: Service Unavailable, during our maintenance break or server downtimes.

## Response Messages

1. 200: Success.
2. 204: No matches we’re found for the provided query.
3. 400: Something’s just not right with the request.
4. 401: Access Denied.
5. 403: Forbidden, Services for this key has been suspended due to daily/hourly transactions limit.
6. 500: Something went wrong.
7. 503: Maintenance Break.

## Request Parameters

### Mandatory Parameters For Nearby Search

1. `recordType (string)` : The category or class of the record, referenced by a defined set of category codes from client.
2. `refLocation (string)`  : Provides the location around which the search will be performed. e.g. `refLocation=28.454,77.435`
    - The `refLocation` parameter can also accept `eLoc` as reference location. <br>
    Example: `refLocation=17ZUL7`

### Optional Parameters for Nearby Search

1.	`radius (integer)` :  The radius in meters for radial search. Default radius: 10000 meters.
2.	`sortBy (string)`  : Provides configured sorting operations for the client on cloud.    Below are the available sorts: 
    - `dist:asc`
    - `dist:desc`
        will sort data in order of distance from the passed location (default is `dist:asc`).Example : `sortBy=dist:asc`. 

### Mandatory Parameters for Text Search

1. `query (string)`: text string that will be searched on attributes specified for textual search within the customer's workspace.

### Common Parameters for Search           
1. `filter (string)` : Filter option as per customer defined data representation schema. In addition to customer specified data representation schema, MapmyIndia also offers its own geo-administrative filter criteria powered by MapmyIndia Maps' administrative hierarcy. <br>
    - `filter=cop{eLoc}` (string) : This field accepts eloc of any administrative area and restricts the search to the provided administrative area eloc. <br>Example : `filter=cop:TAVI5S`. 
    - `filter` (string): can also be customer specific as defined in the data registration schema for the project. Types of filters operations are available in the appendix table 2; which are relative to the type of custom data attributes added (as mentioned in appendix table 1). <br> Example: `filter=specialities:neurosurgery`  
2. `createdTime (integer)` : This is an epoch value in seconds. The filter acts as follows: All records whose creation time is 'greater than' the provided input time here are responded back in results. <br> Example: `createdTime=1628855941`
3. `modifiedTime (integer)` : This is an epoch value in seconds. The filter acts as follows: All records whose modified time is 'greater than' the provided input time here are responded back in results. <br> Example: `modifiedTime=1628855941`
4. `itemCount (integer)`  :  Number of items per page. Minimum is 1; Default is 10.
5. `page (integer)`: provides number of the page to provide results from.
6. `bounds (string)` : '(x1,y1;x2,y2) Allows the developer to send in map bounds to provide a nearby search of the geobounds. where x1,y1 are the lat lng of the bound. The bounds are set from topLeft to bottomRight (North-West to South-East). Example : 28.639256,77.211133;28.625214,77.237483.



## Sample cURL Request

```curl
curl --location 'https://search.mappls.com/search/byod/search?access_token=hklmgbwzrxncdyavtsuojqpiefrbhqplnm&recordType=WFHORWFO&page=1&radius=5000&refLocation=28.550492131024388%2C77.26895656485871'
```

## Sample Response

```
{
    "records": [
        {
            "recordId": "1001",
            "recordEloc": null,
            "recordType": "WFHORWFO",
            "distance": 3801,
            "orderIndex": 1,
            "latitude": 28.50833,
            "longitude": 77.33518,
            "customNote": "",
            "createdOn": 1637841635,
            "modifiedOn": 1637841635,
            "isExpired": false,
            "extendedInfo": {
                "address": "237 okhla",
                "id type": "mobile number",
                "organization": "CE Infosystems",
                "WFH": "N",
                "location": "Home",
                "team": "API Support"
            }
        },
        {
            "recordId": "1002",
            "recordEloc": "06J7HP",
            "recordType": "WFHORWFO",
            "distance": 3806,
            "orderIndex": 2,
            "latitude": null,
            "longitude": null,
            "customNote": "MapmyIndia Head Office",
            "createdOn": 1637843082,
            "modifiedOn": 1637843174,
            "isExpired": false,
            "extendedInfo": {
                "pincode": "110044",
                "address": "237 okhla",
                "id type": "mobile number",
                "organization": "CE Infosystems",
                "WFH": "N",
                "location": "Home",
                "team": "API Support"
            }
        }
    ],
    "pageInfo": {
        "pageCount": 1,
        "totalHits": 2,
        "totalPages": 1,
        "pageSize": 10
    }
}
```
<br>

## Appendix Table 1

| Serial | dataType | Description |
| --- | --- | --- |
| 1 | `text` | Supports textual data. |
| 2 | `double` | This datatype allows only fractional numbers. |
| 3 | `long` | The data type can store whole numbers from -9223372036854775808 to 9223372036854775807 |
| 4 | `integer` | The data type can store whole numbers from -2147483648 to 2147483647 |
| 5 | `boolean` | Support Boolean values true or false |

<br>

## Appendix Table 2

| Serial | Filter Name | Filter Operation | Supported dateTypes | Description |
| --- | --- | --- | --- | --- |
| 1 | `exact` | : | `text`, `integer`, `long`, `double`, `boolean` | This is used for full text search queries. |
| 2 | `range` | -le, -ge, -lt, -gt, -bt | `Integer`, `long`, `double` | Is used with comparison operators |
| 3 | `logical` | ;(or), $(and) | `text`, `integer`, `long`, `double`, `boolean` | Is used to combine two filter criteria. |

<br><br>

For any queries and support, please contact: 

[<img src="https://about.mappls.com/images/mappls-logo.svg" height="40"/> </p>](https://about.mappls.com/api/)
Email us at [apisupport@mappls.com](mailto:apisupport@mappls.com)


![](https://www.mapmyindia.com/api/img/icons/support.png)
[Support](https://about.mappls.com/contact/)
Need support? contact us!

<br></br>
<br></br>

[<p align="center"> <img src="https://cdn.jsdelivr.net/gh/glincker/thesvg@main/public/icons/stack-overflow/default.svg" height="40"/> ](https://stackoverflow.com/questions/tagged/mappls-api)[![](https://www.mapmyindia.com/api/img/icons/blog.png)](https://about.mappls.com/blog/)[<img src="https://cdn.jsdelivr.net/gh/glincker/thesvg@main/public/icons/github/mono.svg" height="40"/> ](https://github.com/mappls-api)[<img src="https://mmi-api-team.s3.ap-south-1.amazonaws.com/API-Team/npm-logo.one-third%5B1%5D.png" height="40"/> </p>](https://www.npmjs.com/org/mapmyindia) 



[<p align="center"> <img src="https://www.mapmyindia.com/june-newsletter/icon4.png"/> ](https://www.facebook.com/Mapplsofficial)[![](https://www.mapmyindia.com/june-newsletter/icon2.png)](https://twitter.com/mappls)[![](https://www.mapmyindia.com/newsletter/2017/aug/llinkedin.png)](https://www.linkedin.com/company/mappls/)[![](https://www.mapmyindia.com/june-newsletter/icon3.png)](https://www.youtube.com/channel/UCAWvWsh-dZLLeUU7_J9HiOA)




<div align="center">@ Copyright 2025 CE Info Systems Ltd. All Rights Reserved.</div>

<div align="center"> <a href="https://about.mappls.com/api/terms-&-conditions">Terms & Conditions</a> | <a href="https://about.mappls.com/about/privacy-policy">Privacy Policy</a> | <a href="https://about.mappls.com/pdf/mapmyIndia-sustainability-policy-healt-labour-rules-supplir-sustainability.pdf">Supplier Sustainability Policy</a> | <a href="https://about.mappls.com/pdf/Health-Safety-Management.pdf">Health & Safety Policy</a> | <a href="https://about.mappls.com/pdf/Environment-Sustainability-Policy-CSR-Report.pdf">Environmental Policy & CSR Report</a>

<div align="center">Customer Care: +91-9999333223</div>
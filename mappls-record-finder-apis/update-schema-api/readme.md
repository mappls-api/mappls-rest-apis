[<img src="https://about.mappls.com/images/mappls-logo.svg" height="40"/> </p>](https://about.mappls.com/api/)

# Custom Search - Update Schema API


## Introduction

This API allows the developer to update an already registered data representation schema associated with their project for Custom search database. The data representation schema is used by the search engine to configure and index the added records so that intended filters and search criteria can be applied on the added records by the consuming solution.

## URL

```html
https://search.mappls.com/search/byod/schema
```

## HTTPS Method

PUT

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

1. 201: Created.
2. 204: No matches we’re found for the provided query.
3. 400: Something’s just not right with the request.
4. 401: Access Denied.
5. 403: Forbidden, Services for this key has been suspended due to daily/hourly transactions limit.
6. 409: Conflict.
7. 500: Something went wrong.
8. 503: Maintenance Break.

## Request Parameters



### Mandatory Parameters

1. `searchFields` (object): list of attributes of records as key value pairs where values are in boolean. This list of attributes are the ones on which textual search will be active and they will be accordinly indexed.
    <br> Example: `"facilityName": true`
2. `filterFields` (object): list of attributes of records as key value pairs where describe the type of filtering active on the respective attribute. This list of attributes are the ones on which nearby search with custom filtering criteria will be active and they will be accordinly indexed.
    <br> Example: `"ownership": "exact"`
    <br> Types of accepted filter values are below in annexure table 2.
3. `extendedFields` (object): A list of all the custom attributes of a record that are maintained in the project's schema. This list of extended attributes are the ones on which either textual search or nearby search with filters will be active.
<br>Example: 
    ```json
    "ownership": {
                    "dataType": "text"
                }
    ```
    - `dataType` (string): data types of different custom attributes that are acceptable. Valid values are listed in annexure table 1 below.

<br>

### Optional Parameters

1. `isCustomSearch` (boolean): Used to enable or disable custom textual search on custom fields defined in `extendedFields` above.
2. `isCustomFilter` (boolean): Used to enable or disable filter based nearby search on custom fields defined in `extendedFields` above.

<br>

## Response Parameters

None

## Sample cURL Request

### Sample 1

```curl
curl --location --request PUT 'https://search.mappls.com/search/byod/schema?access_token=hklmgbwzrxncdyavtsuojqpiefrbhqplnm' \
--header 'Content-Type: application/json' \
--data-raw '{
    "extendedFields": 
    {},
    "searchFields":
    {
        "facilityName": true,
        "district": true
    },
    "filterFields":
    {
        "ownership": "exact",
        "medicineSystem": "logical",
        "specialities": "logical",
        "state": "logical",
        "district": "logical"

    },
    "isCustomSearch": true,
    "isCustomFilter": true
}'
```

## Sample Response

```json
{
    "message": "UPDATED",
    "responseCode": 200
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

[<p align="center"> <img src="https://cdn.jsdelivr.net/gh/glincker/thesvg@main/public/icons/stack-overflow/default.svg" height="40"/> ](https://stackoverflow.com/questions/tagged/mappls-api)[![](https://www.mapmyindia.com/api/img/icons/blog.png)](https://about.mappls.com/blog/)[<img src="https://cdn.jsdelivr.net/gh/glincker/thesvg@main/public/icons/github/dark.svg" height="40"/> ](https://github.com/mappls-api)[<img src="https://mmi-api-team.s3.ap-south-1.amazonaws.com/API-Team/npm-logo.one-third%5B1%5D.png" height="40"/> </p>](https://www.npmjs.com/org/mapmyindia) 



[<p align="center"> <img src="https://www.mapmyindia.com/june-newsletter/icon4.png"/> ](https://www.facebook.com/Mapplsofficial)[![](https://www.mapmyindia.com/june-newsletter/icon2.png)](https://twitter.com/mappls)[![](https://www.mapmyindia.com/newsletter/2017/aug/llinkedin.png)](https://www.linkedin.com/company/mappls/)[![](https://www.mapmyindia.com/june-newsletter/icon3.png)](https://www.youtube.com/channel/UCAWvWsh-dZLLeUU7_J9HiOA)




<div align="center">@ Copyright 2025 CE Info Systems Ltd. All Rights Reserved.</div>

<div align="center"> <a href="https://about.mappls.com/api/terms-&-conditions">Terms & Conditions</a> | <a href="https://about.mappls.com/about/privacy-policy">Privacy Policy</a> | <a href="https://about.mappls.com/pdf/mapmyIndia-sustainability-policy-healt-labour-rules-supplir-sustainability.pdf">Supplier Sustainability Policy</a> | <a href="https://about.mappls.com/pdf/Health-Safety-Management.pdf">Health & Safety Policy</a> | <a href="https://about.mappls.com/pdf/Environment-Sustainability-Policy-CSR-Report.pdf">Environmental Policy & CSR Report</a>

<div align="center">Customer Care: +91-9999333223</div>
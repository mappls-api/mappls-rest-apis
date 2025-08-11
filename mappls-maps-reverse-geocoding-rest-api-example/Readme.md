[<img src="https://about.mappls.com/about/images/MAPPLS-MapmyIndia-logo.png" height="40"/> </p>](https://about.mappls.com/api/)
# Reverse Geocoding API

**Easy To Integrate Maps & Location APIs & SDKs For Web & Mobile Applications**

Powered with India's most comprehensive and robust mapping functionalities.

## Global Coverage Now Available !

Reverse Geocoding API is **Now Available**  for [238 countries](https://github.com/mappls-api/mappls-rest-apis/blob/main/docs/countryISO.md) across the world.

You can get your api key to be used in this document here: [https://about.mappls.com/api/](https://about.mappls.com/api/)

**Full documentation available here**: [https://www.mapmyindia.com/api/advanced-maps/doc/reverse-geocoding-api](https://www.mapmyindia.com/api/advanced-maps/doc/reverse-geocoding-api).

## Introduction
Reverse Geocoding is a process to give the closest matching address to a provided geographical coordinates (latitude/longitude). Mappls reverse geocoding API provides real addresses along with nearest popular landmark for any such geo-positions on the map. This API also works in Hindi language so for that you have to add new paramter introduced lang. 


## Getting Access

Before using the API in the your solution, please ensure that the related access is enabled in the [Mappls Console](https://auth.mappls.com/console/), within your app - be it for Mobile OR Web or Cloud integration.

1. Copy and paste the key from your `credentials` section from your API [keys](https://auth.mappls.com/console/) into the `access_token` query parameter.
    - Your static key can be secured by whitelisting its usage for particular IPs (in case of cloud app usage) OR a set of domains (in case of a web app)
    - Your static key obtained from your Console is to be passed as a query parameter: `access_token`.

## Authentication Object - `access_token` mandatory query parameter.

-  `access_token`: "hklmgbwzrxncdyavtsuojqpiefrbhqplnm".

## Live Demo

[Click here to visit live demonstration page](https://about.mappls.com/api/advanced-maps/doc/sample/mapmyindia-vector-maps-reverse-geocoding-rest-api-example.php)

## Input Method
GET

## Input URL

`https://search.mappls.com/search/address/rev-geocode?`

## Response Type

JSON


## Response Codes {as HTTP response code}

- 200: To denote a successful API call.
- 204: DB Connection error.
- 400: Bad Request, User made an error while creating a valid request.
- 401: Unauthorized, Developer’s key is not allowed to send a request.
- 403: Forbidden, Developer’s key has hit its daily/hourly limit or IP or domain not white-listed.
- 404: HTTP not found
- 412: Precondition Failed, i.e. Mandatory parameter is missing
- 500: Internal Server Error, the request caused an error in our systems.
- 503: Service Unavailable, during our maintenance break or server down-times.

<br><br>

## Request Parameters
The “**bold**” one’s are mandatory, and the “*italic*” one’s are optional.

1.  **`lat`**: The latitude of the location for which the address is required.
2.  **`lng`**: The longitude of the location for which address is required.
3.  *`region`*(string): This parameter is optional for India; for other countries (such as Sri Lanka, Nepal, Bangladesh, Bhutan + many more) this parameter is mandatory. Possible values are listed in a table [here](https://github.com/mappls-api/mappls-rest-apis/blob/main/docs/countryISO.md). Default is India (IND)
4.  *`lang`* (string): This parameter accepts the "hi" (ISO 639-1 Language Code for Hindi) as a value. 

## Response Parameters
1. **`responseCode`**: The response code value for the API request call.
2. **`version`**: The version changes after data update. The version numbers are internal.
3. **`results`**: The data returned for the request made with input parameters. Below are the each response components :
   - **`houseNumber`**: The house number (if exists) of the location sent in the request. 
   - **`houseName`**: The house name (if exists) of the location sent in the request.
   - **`poi`**: The POI name of the location (if exists) for the given location.
   - **`poi_dist`**: The distance between of the given location and the POI.
   - **`street`**: The available street name for the given location or the nearest street name from the given location.
   - **`street_dist`**:  The distance from street to the point given in the request.
   - **`subSubLocality`**: The sub-sub locality name (if exists) for the given location.
   - **`subLocality`**: The sub locality name (if exists) for the given location.
   - **`locality`**: The locality name (if exists) for the given location.
   - **`village`**: The village name if the given location in request is nearby village. If village name is coming in the response, city name and locality names will not be present in the response. The locations are defined on the basis of urban and rural regions.
   - **`district`**: The district name of the given location.
   - **`subDistrict`**: The sub district name of the given location.
   - **`city`**: The city name of the given location. There will be no village name in case of the availibilty of city name.  The locations are defined on the basis of urban and rural regions.
   - **`state`**: The state name of the given location.
   - **`pincode`**:  The pincode of the given location. 
   - **`lat`**: The latitude value of the given location in the request. 
   - **`lng`**: The longitude value of the given location in the request.
   - **`area`**: The country name of the given location.
   - **`formatted_address`**: The compelete formatted address for the passed location in the request.

## Premium Response Parameters (only for India region)
1. Census Information: (as per last census)
    - `sttCenCd` (string): State's census code.
    - `dstCenCd` (string): District's census code.
    - `sdbCenCd` (string): Subdistrict's census code.
    - `vlgCenCd` (string): Village's census code, if address is rural.
    - `twnCenCd` (string): Town's census code, if address is within any census town. <br>
    Note: Here town means a census town - an urban agglomeration defined by GoI during census; which is different from a city.
    - `twnName` (string): Town's name as per last census.
2. Local Government Directory (LGD Information)
    - `sttLgdCd` (string): State's LGD code.
    - `dstLgdCd` (string): District's LGD code.
    - `sdbLgdCd` (string): Subdistrict's LGD code.
    - `vlgLgdCd` (string): Village's LGD code, if address is rural.
    - `twnLgdCd` (string): Town's LGD code, if address is within any census town.

## Sample Input

`https://search.mappls.com/search/address/rev-geocode?lat=26.5645&lng=85.9914&access_token=hklmgbwzrxncdyavtsuojqpiefrbhqplnm`

## Sample Output
```json
{
    "responseCode": 200,
    "version": "270.191",
    "results": [
        {
            "houseNumber": "",
            "houseName": "",
            "poi": "Panchayat Headquarter",
            "poi_dist": "508",
            "street": "Unnamed Road",
            "street_dist": "7",
            "subSubLocality": "",
            "subLocality": "",
            "locality": "",
            "village": "Basopatti",
            "district": "Madhubani District",
            "subDistrict": "Basopatti",
            "city": "",
            "state": "Bihar",
            "pincode": "847225",
            "lat": "26.5645",
            "lng": "85.9914",
            "area": "India",
            "formatted_address": "Unnamed Road, Basopatti, Basopatti, Madhubani District, Bihar. 508 m from Panchayat Headquarter pin-847225 (India)"
        }
    ]
}
```
<br> <br>



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
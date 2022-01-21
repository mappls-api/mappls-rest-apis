[<img src="https://www.mappls.com/api/img/mappls-api.png" height="40"/> </p>](https://www.mappls.com/api)
# Reverse Geocoding API

**Easy To Integrate Maps & Location APIs & SDKs For Web & Mobile Applications**

Powered with India's most comprehensive and robust mapping functionalities.

## Global Coverage Now Available !

Reverse Geocoding API is **Now Available**  for [238 countries](https://github.com/Mappls-api/mappls-rest-api/blob/master/docs/countryISO.md) across the world.

You can get your api key to be used in this document here: [https://www.mappls.com/api/](https://www.mappls.com/api/)

**Full documentation available here**: [https://www.mapmyindia.com/api/advanced-maps/doc/reverse-geocoding-api](https://www.mapmyindia.com/api/advanced-maps/doc/reverse-geocoding-api).

## Introduction
Reverse Geocoding is a process to give the closest matching address to a provided geographical coordinates (latitude/longitude). Mappls reverse geocoding API provides real addresses along with nearest popular landmark for any such geo-positions on the map. This API also works in Hindi language so for that you have to add new paramter introduced lang. 

## Live Demo

[Click here to visit live demonstration page](https://www.mapmyindia.com/api/advanced-maps/doc/sample/mapmyindia-maps-reverse-geocoding-rest-api-example)

## Input Method
GET

## Input URL

`https://apis.mappls.com/advancedmaps/v1/<licence_key>/rev_geocode?lat=<latidude>&lng=<longitude>`

## Response Type

JSON


## Request Parameters
The “**bold**” one’s are mandatory, and the “*italic*” one’s are optional.

1.  **`lat`**: The latitude of the location for which the address is required.
2.  **`lng`**: The longitude of the location for which address is required.
3.  **`Licence_key`**: The REST API licence key allocated to you by signing into our services and registering yourself as a developer (28 Char Alphanumeric).
4.  *`region`*(string): This parameter is optional for India; for other countries (such as Sri Lanka, Nepal, Bangladesh, Bhutan + many more) this parameter is mandatory. Possible values are listed in a table [here](https://github.com/Mappls-api/mappls-rest-api/blob/master/docs/countryISO.md). Default is India (IND)
5.  *`lang`* (string): This parameter accepts the "hi" (ISO 639-1 Language Code for Hindi) as a value. 


## Sample Input

`https://apis.mappls.com/advancedmaps/v1/<licence_key>/rev_geocode?lat=26.5645&lng=85.9914`

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



For any queries and support, please contact: 

[<img src="https://www.mappls.com/images/logo.png" height="40"/> </p>](https://www.mappls.com/api)
Email us at [apisupport@mappls.com](mailto:apisupport@mappls.com)


![](https://www.mapmyindia.com/api/img/icons/support.png)
[Support](https://www.mappls.com/api/index.php#f_cont)
Need support? contact us!

<br></br>
<br></br>

[<p align="center"> <img src="https://www.mapmyindia.com/api/img/icons/stack-overflow.png"/> ](https://stackoverflow.com/questions/tagged/mappls-api)[![](https://www.mapmyindia.com/api/img/icons/blog.png)](http://www.mappls.com/blog/)[![](https://www.mapmyindia.com/api/img/icons/gethub.png)](https://github.com/Mappls-api)[<img src="https://mmi-api-team.s3.ap-south-1.amazonaws.com/API-Team/npm-logo.one-third%5B1%5D.png" height="40"/> </p>](https://www.npmjs.com/org/mapmyindia) 



[<p align="center"> <img src="https://www.mapmyindia.com/june-newsletter/icon4.png"/> ](https://www.facebook.com/Mappls)[![](https://www.mapmyindia.com/june-newsletter/icon2.png)](https://twitter.com/Mappls)[![](https://www.mapmyindia.com/newsletter/2017/aug/llinkedin.png)](https://www.linkedin.com/company/mappls)[![](https://www.mapmyindia.com/june-newsletter/icon3.png)](https://www.youtube.com/user/Mappls/)




<div align="center">@ Copyright 2022 CE Info Systems Ltd. All Rights Reserved.</div>

<div align="center"> <a href="https://www.mappls.com/api/terms-&-conditions">Terms & Conditions</a> | <a href="https://www.mappls.com/about/privacy-policy">Privacy Policy</a> | <a href="https://www.mappls.com/pdf/mappls-sustainability-policy-healt-labour-rules-supplir-sustainability.pdf">Supplier Sustainability Policy</a> | <a href="https://www.mappls.com/pdf/Health-Safety-Management.pdf">Health & Safety Policy</a> | <a href="https://www.mappls.com/pdf/Environment-Sustainability-Policy-CSR-Report.pdf">Environmental Policy & CSR Report</a>

<div align="center">Customer Care: +91-9999333223</div>
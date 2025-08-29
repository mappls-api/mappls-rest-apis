[<img src="https://about.mappls.com/about/images/MAPPLS-MapmyIndia-logo.png" height="40"/> </p>](https://about.mappls.com/api/)
# Mappls Digipin APIs 

**Easy To Integrate Maps & Location APIs & SDKs For Web & Mobile Applications**

Powered with India's most comprehensive and robust mapping functionalities.

You can get your api key to be used in this document here: [https://about.mappls.com/api/](https://about.mappls.com/api/)

## Introduction

India Post’s Digipin initiative introduces a standardized, grid-based digital addressing format for every 4m x 4m (approximately) location across India — covering both built-up and unbuilt areas. While not a unique identifier for specific addressable entities like buildings or shops (unlike property-linked IDs), it serves as a simple, fixed-location reference similar in concept to global systems like Geohash.

MapmyIndia is developing a powerful and easy-to-integrate Digipin Conversion API that enables two-way conversion between Digipins and geographic coordinates (latitude/longitude). This API offers a lightweight, scalable alternative for applications requiring standardized grid references—ideal for digital infrastructure, coverage mapping, verification, and planning use cases.

Designed to complement MapmyIndia’s advanced location-based services, this API can enhance your product’s ability to engage with India's evolving digital address ecosystem. Whether you're building platforms for logistics, utility planning, rural outreach, or governance, this API provides a reliable, uniform location reference layer—backed by the geospatial expertise of MapmyIndia.


<!-- ## Alternative Introduction

India Post’s Digipin initiative introduces a standardized, grid-based digital addressing format that assigns a unique code to every 4m x 4m location across India—spanning both built and unbuilt areas. While it does not uniquely identify addressable entities like buildings or shops, Digipin serves as a precise geospatial reference point, much like global systems such as Geohash.

MapmyIndia has developed a robust and developer-friendly Digipin Conversion API, enabling seamless two-way translation between Digipins and geographic coordinates (latitude/longitude). This API offers a lightweight, standardized grid reference, ideal for large-scale mapping, data indexing, infrastructure rollout, and verification tasks.

This API is designed to supplement MapmyIndia’s comprehensive location-based services, giving businesses and government platforms a scalable tool to engage with India’s digital location framework. Whether you're building logistics, rural delivery, utility, or geospatial planning solutions, this API equips your platform with a consistent, pan-India location grid—powered by MapmyIndia’s trusted technology stack. -->

## Live Demo

You can also experience this Digipin Conversion through our Mappls Portal. For experience please [click here](https://www.mappls.com/)

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

```html
https://sdk.mappls.com/map/api/digipin?
```

## Request Parameters

### Mandatory Parameters

 - `digipin`(string): Digipin (with or without hyphens) 10 characters of digipin.
  
OR

- `mapplsPin`(string): 6 charater Mappls pin for which the user wishes to fetch the Digipin for.

OR

- `coordinates`(string):  latitude,longitude - comma separated latitude & longitude pair in decimal degree format (WGS-84 datum) for which you need to determin the Digipin for. The coordinates should be at-least of atleast 5 decimal precision or better for accurate Digipin determination.

### Optional Parameters

Not Applicable

## Response Parameters

### When input is Digpin

1. `latitude`(double): the latitude of the Digipin in WPS-84 decimal degree format.
2. `longitude`(double): the longitude of the Digipin in WPS-84 decimal degree format.

### When input are Coordinates

1. `digipin`(string): The raw Digipin (10 chars) for the input coordinates.
2. `formattedDigipin`(string) The formatted Digipin with hyphens for the provided coordinates.

### When input is Mappls pin

1. `digipin`(string): The raw Digipin (10 chars) for the input Mappls pin.
2. `formattedDigipin`(string) The formatted Digipin with hyphens for the provided Mappls pin.


> **Important Note**: This response needs to be claim controlled. When claim of `useMapplsPin` (valueless) is present, only then the API should allow for translation of a Mappls pin / eLoc to its Digipin.


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

### Input is coordinates

```js
curl --location 'https://sdk.mappls.com/map/api/digipin?coordinates="28.62722117136,77.235543104"&access_token=hklmgbwzrxncdyavtsuojqpiefrbhqplnm'
```

### Sample Response

```json
{
    "responseCode": 200,
    "digipin": "39J49P7FTJ", 
	"formattedDigipin": "39J-49P-7FTJ"
}
```

### Input is Digipin

```js
curl --location 'https://sdk.mappls.com/map/api/digipin?digipin=39J-49P-7FTJ&access_token=hklmgbwzrxncdyavtsuojqpiefrbhqplnm'
```

### Sample Response

```json
{
    "responseCode": 200,
    "latitude": 28.62722206, 
	"longitude": 77.23553658
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
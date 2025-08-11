[<img src="https://about.mappls.com/about/images/MAPPLS-MapmyIndia-logo.png" height="40"/> </p>](https://about.mappls.com/api/)

# Mappls Aerial Distance API

**Easy To Integrate Maps & Location APIs & SDKs For Web & Mobile Applications**

Powered with India's most comprehensive and robust mapping functionalities.
**Now Available**  for Srilanka, Nepal, Bhutan, Myanmar and Bangladesh

You can get your api key to be used in this document here: [https://about.mappls.com/api/](https://about.mappls.com/api/)

## Disclaimer
The document contains sensitive information on parameters and responses that can be accessed only by Mappls.
Redistribution without permissions is prohibited.
It is mandatory to take permissions from the author before sharing with any personnel outside Mappls.


## Introduction

### Aerial Distance

Adding Aerial Distance API would help to calculate the distance between two points on the map. For example, you can measure the mileage in a straight line between two cities.

You can now easily estimate how big the lake near your house is, or just the **aerial distance** between Delhi and Mumbai is 1150.06 km (714.61 mi). Same time this **API  doesn't calculate road distance between two points.**

## Getting Access

Before using the API in the your solution, please ensure that the related access is enabled in the [Mappls Console](https://auth.mappls.com/console/), within your app - be it for Mobile OR Web or Cloud integration.

1. Copy and paste the key from your `credentials` section from your API [keys](https://auth.mappls.com/console/) into the `access_token` query parameter.
    - Your static key can be secured by whitelisting its usage for particular IPs (in case of cloud app usage) OR a set of domains (in case of a web app)
    - Your static key obtained from your Console is to be passed as a query parameter: `access_token`.

## Authentication Object - `access_token` mandatory query parameter.

-  `access_token`: "hklmgbwzrxncdyavtsuojqpiefrbhqplnm".


## Input Method
GET


### Example URL using coordinates: 
```html
https://tile.mappls.com/map/raster_tile/distanceA?from=34.506172,76.108652&to=28.4586,77.85698&unit=K&access_token=hklmgbwzrxncdyavtsuojqpiefrbhqplnm
```
where: 
- "distanceA" is the chosen resource.
- `from` request parameter denotes the start position.
	- Example: `from=34.506172,76.108652`
- `to` request parameter denotes the destination position.
	- Example: `to=28.4586,77.85698`

**Note**: The position input is in decimal degree notation of latitude,longitude.

### Example URL using eLoc: 
```html
https://tile.mappls.com/map/raster_tile/distanceA?from=mmi000&to=17zul7&unit=K&access_token=hklmgbwzrxncdyavtsuojqpiefrbhqplnm
```
where: 
- "distanceA" is the chosen resource.
- `from` request parameter denotes the start position.
	- Example: `from=mmi000`
- `to` request parameter denotes the destination position.
	- Example: `to=17zul7`

**Note**: The position input is in decimal degree notation of longitude,latitude.


## Request Parameters

###  Mandatory Parameters:

1.  `from` request parameter denotes the start position.
2.  `to` request parameter denotes the destination position.

### Optional Parameters:

1. `Unit`: unit of distance (default value is K)
	- K: Kilometre
	- N: Nautical Miles
	- M: Miles


## Response Type
JSON: response will served as JSON

## Response Parameters

The Aerial_Distance API will return only one result object. The following output parameters will be supported in the Aerial_Dstance API response.

1. `responseCode`: See the service dependent and general status codes.
2.  `results`: array of results, each consisting of the following parameters.
	- `distance`: a distance between strart & destinaton.
	- `unit`: unit of distance.

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


 
## Sample Request:

URL: 
```html
https://tile.mappls.com/map/raster_tile/distanceA?from=34.506172,76.108652&to=28.4586,77.85698&unit=K&access_token=hklmgbwzrxncdyavtsuojqpiefrbhqplnm
```


## Sample Response data:
```json
{  
	"responseCode": 200, 
	"distance": 692.52185107232, 
	"unit": "K"
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
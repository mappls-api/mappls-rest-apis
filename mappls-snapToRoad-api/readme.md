[<img src="https://about.mappls.com/about/images/MAPPLS-MapmyIndia-logo.png" height="40"/> </p>](https://about.mappls.com/api/)

# Mappls Snap To Road API

**Easy To Integrate Maps & Location APIs & SDKs For Web & Mobile Applications**

Powered with India's most comprehensive and robust mapping functionalities.
## Global Coverage Now Available !

Snap to Road API is **Now Available**  for [238 countries](https://github.com/mappls-api/mappls-rest-apis/blob/main/docs/countryISO.md) across the world.

You can get your api key to be used in this document here: [https://about.mappls.com/api/](https://about.mappls.com/api/)

## Disclaimer
The document contains sensitive information on parameters and responses that can be accessed only by Mappls.
Redistribution without permissions is prohibited.
It is mandatory to take permissions from the author before sharing with any personnel outside Mappls.

## Document Version History

| Version | Last Updated | Author |
| ---- | ---- | ---- |
| 0.0.2 | July 2021 | Mappls API Team ([KB](https://github.com/kunalbharti)) |
| 0.0.1 | February 2019 | Mappls API Team ([KB](https://github.com/kunalbharti)) |

## API Version History

| Version | Last Updated | Author | Revised Sections |
| ---- | ---- | ---- | ---- |
| 270.19 | 2021-07-13 | Mappls API Team ([PS](https://github.com/map-123)) | [Global](https://github.com/mappls-api/mappls-rest-apis/blob/main/docs/countryISO.md) support added. |
| 191.17 | 2019-02-07 | Mappls API Team ([PS](https://github.com/map-123)) | Data update to V19.1; Added support for SNBB |
| 1.0 | 2018-06-07 | Mappls API Team ([PS](https://github.com/map-123)) | Initial release |


## Introduction

### Route and Navigation

Snap-To-Road API, snaps given GPS points to the road network in the most plausible way. Maximum number of points are limited to 100 only. Snap to Road API is supported for [238 countries](https://github.com/mappls-api/mappls-rest-apis/blob/main/docs/countryISO.md) via the region parameter.

#### Note
1. The request might result multiple sub-traces. 
2. Large jumps in the timestamps (> 60s) or improbable transitions lead to trace splits if a complete matching could not be found. 
3. The algorithm might not be able to match all points. Outliers are removed if they cannot be matched successfully. 

## Getting Access

Before using the API in the your solution, please ensure that the related access is enabled in the [Mappls Console](https://auth.mappls.com/console/), within your app - be it for Mobile OR Web or Cloud integration.

1. Copy and paste the key from your `credentials` section from your API [keys](https://auth.mappls.com/console/) into the `access_token` query parameter.
    - Your static key can be secured by whitelisting its usage for particular IPs (in case of cloud app usage) OR a set of domains (in case of a web app)
    - Your static key obtained from your Console is to be passed as a query parameter: `access_token`.

## Authentication Object - `access_token` mandatory query parameter.

-  `access_token`: "hklmgbwzrxncdyavtsuojqpiefrbhqplnm".


## Input Method
GET / POST

## Constructing the request URL

```
https://route.mappls.com/route/movement/snapToRoad?
```

### Important Note
1. When using POST method, the parameters are sent with `Content-Type` as `application/x-www-form-urlencoded`.


### Example using GET
```json
https://route.mappls.com/route/movement/snapToRoad?pts=78.40573,17.37317;78.40958,17.37314;78.41845,17.37449;78.409992,17.37328;78.420460,17.377443;78.421350,17.380200&timestamps=1527056019;1527056020;1527056021;1527056022;1527056023;1527056024&access_token=hklmgbwzrxncdyavtsuojqpiefrbhqplnm
```

### Example using POST
```c
curl --location --request POST 'https://route.mappls.com/route/movement/snapToRoad?access_token=hklmgbwzrxncdyavtsuojqpiefrbhqplnm' \
--data-urlencode 'pts=78.40573,17.37317;78.40958,17.37314;78.41845,17.37449;78.409992,17.37328;78.420460,17.377443;78.421350,17.380200' \
--data-urlencode 'timestamps=1527056019;1527056020;1527056021;1527056022;1527056023;1527056024' \
--data-urlencode 'geometries=polyline' \
--data-urlencode 'radiuses=50;50;50;50;50;50'
```

**Note**: The position input is in decimal degree notation of longitude,latitude.


## Request Parameters

### Mandatory Parameters

The “**bold**” one’s are mandatory, and the “*italic*” one’s are optional.

1.  **`pts`**: Coordinate is pair of comma separated longitude & latitude value, First coordinate will be consider as start point; a last coordinate will be as end points and between are via points; like {longitude},{latitude};{longitude},{latitude}[;{longitude},{latitude} ...]. 
At present maximum number of points are limited to 100 in a single request. 
For example 77.983936,28.255904;77.05993,28.487555.

### Optional Parameters

1. *`timestamps`*: Timestamps for the input locations in seconds since UNIX epoch. Timestamps need to be monotonically increasing. Values must be integer {timestamp};{timestamp};{timestamp} ...
2.  *`geometries`*: This parameter used to change the route geometry format/density (influences overview and per step). Default value is `polyline` with 5 digit precision; `polyline6` for 6digit precision; `geojson` for geometries as geojson. **Please note that “timestamps” parameter is mandatory for enabling geometries**
3. *`radiuses`*: Standard deviation of GPS precision used for map matching. If available use GPS accuracy in meters. Default value is `5` metres. Values must be integer {radius};{radius};{radius} ...
4. *`region`*: This parameter is optional for India; for other countries (such as Sri Lanka, Nepal, Bangladesh, Bhutan + many more) this parameter is mandatory. Possible values are listed in a table [here](https://github.com/mappls-api/mappls-rest-apis/blob/main/docs/countryISO.md).

## Response Type
JSON: response will served as JSON


## Response Parameters

1.	`responseCode`: See the service dependent and general status codes.
2.	`version`: API’s version information.
3.	`results`: array of results, each consisting of the following parameters:
	- `snappedPoints`: Array of Waypoint objects representing all points of the trace in order. If the trace point was omitted by map matching because it is an outlier, the entry will be null. Each Waypoint object has the following additional properties.
		- `location`: Location of Matched point (Longitude, Latitude)
		- `distance`: Distance from the snapped point.
		- `waypoint_index`: Index of the waypoint inside the matched route.
	- `matchings`: An array of Route objects that assemble the trace.
		- `geometry`: Returns the whole geometry of the route as per given parameter ‘geometries’ default is encoded ‘polyline’ with 5 digit accuracy for positional coordinates.


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

## Sample Input

`https://route.mappls.com/route/movement/snapToRoad?pts=78.40573,17.37317;78.40958,17.37314;78.41845,17.37449;78.409992,17.37328;78.420460,17.377443;78.421350,17.380200&timestamps=1527056019;1527056020;1527056021;1527056022;1527056023;1527056024&access_token=hklmgbwzrxncdyavtsuojqpiefrbhqplnm`

## Sample Response
```json
{
    "responseCode": 200,
    "version": "220.19.522",
    "results": {
        "snappedPoints": [
            {
                "location": [
                    78.40573,
                    17.373168
                ],
                "distance": 0.221335,
                "waypoint_index": 0
            },
            {
                "location": [
                    78.40958,
                    17.373151
                ],
                "distance": 1.217342,
                "waypoint_index": 1
            },
            null,
            null,
            {
                "location": [
                    78.420424,
                    17.377454
                ],
                "distance": 4.014843,
                "waypoint_index": 2
            },
            {
                "location": [
                    78.421362,
                    17.380197
                ],
                "distance": 1.317787,
                "waypoint_index": 3
            }
        ],
        "matchings": [
            {
                "geometry": "ie`iByrp}MN{HKeMXmOKuGq@}JaBaHaDmIgB{BuDcCuGeBeP{D"
            }
        ]
    }
}
```

## Live Demo

[Snap To Road API](https://about.mappls.com/api/advanced-maps/doc/sample/mapmyindia-maps-snaptoroad-example)

For more details, please visit our full documentation.

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
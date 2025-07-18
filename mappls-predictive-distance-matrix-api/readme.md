[<img src="https://about.mappls.com/about/images/MAPPLS-MapmyIndia-logo.png" height="40"/> </p>](https://about.mappls.com/api/)

# Mappls Distance-Time Matrix API for Predictive ETA

**Easy To Integrate Maps & Location APIs & SDKs For Web & Mobile Applications**

Powered with India's most comprehensive and robust mapping functionalities.

You can get your api key to be used in this document here: [https://about.mappls.com/api/](https://about.mappls.com/api/)

## Disclaimer
1. This API is released for select use cases only; Please contact Mappls API Support or your account manager for discussions on usage of this solution. 
2. Mappls reserves the right to revoke access of this API at its own discrection.


## Document Version History

| Version | Last Updated | Author |
| ---- | ---- | ---- |
| 0.0.1 | November 2021 | Mappls API Team ([KB](https://github.com/kunalbharti)) |
| 0.0.2 | July 2023 | Mappls API Team ([KB](https://github.com/kunalbharti)) |

## API Version History

| Version | Last Updated | Author | Revised Sections |
| ---- | ---- | ---- | ---- |
| 0.1 | 2021-06-17 | Mappls API Team ([PS](https://github.com/map-123)) | Initial release |
| 0.2 | 2021-07-01 | Mappls API Team ([PS](https://github.com/map-123)) | standardizing request & response |

## Introduction

### Route and Navigation

This API computes the distance and duration of a route between a set of source positions and a set of supplied target or destination positions.
Optionally one can specify the `date_time` parameter and get the distance and duration optimized for that part of day of a week. Time based functionality is available for selected areas only.
Supported region (countries) is India at the moment. Please note that maximum number of points are limited to 100 only including source and destination positions.

## Security Type
This APIs follow OAuth2 based security. **To know more on how to create your authorization tokens, please use our authorization token URL. More details available**  [here](https://github.com/mappls-api/mappls-rest-apis/tree/main/mappls-token-generation-api)

## Request Headers

The API leverages OAuth 2.0 based security. Hence, the developer would need to send a request for access token using their client_id and client_secret to the OAuth API. Once validated from the OAuth API, the access_token and the token_type need to be sent as Authorization header with the value: “{token_type} {access_token}”.

-  `Authorization:  “token_type access_token”`.


## Input Method
GET

## Contructing the request cURL

```c
curl --location --request GET 'https://apis.mappls.com/advancedmaps/v2/distance?source=77.26893112158996,28.550614332693453&target=77.20815617692985,28.566618140144396&profile=driving&speedTypes=predictive&date_time=1,2021-12-20T11:00' \
--header 'Authorization: bearer 0XXXXXXf-dXX0-4XX0-8XXa-eXXXXXXXXXX6'
```


## Request Parameters

### Mandatory Parameters

1.  `source`: The set of source positions, separated by a semi-colon. The input is supported as a set of latitude,longitude separated by a semi-colon(;).
	- For example `77.08572454324664,28.555390931473642;77.42172454324664,28.152390931473642`.
2. `target`: The set of destination positions, separated by a semi-colon. The input is supported as a set of latitude,longitude separated by a semi-colon(;).
	- For example `77.08572454324664,28.555390931473642;77.42172454324664,28.152390931473642`.
3. `profile`:  Profile for routing engine. Choose of the available profiles available: 
    - `driving`: for 4 wheelers.
    - `walking`: for pedestrians.
    - `biking`: for motorized 2 wheelers.
    - `trucking`: for heavy vehicles.

    Example `profile=driving`.
4. `speedTypes`: To specify the type of ETA calculations. Available values are: 
	- `predictive` (default) - used to specify predictive ETA calculation. In case if this is used, then the optional parameter of `date_time` becomes mandatory.
	- `optimal`: To specify ETA calculation acc. to current time but on the basis of historical traffic patterns.
    - `traffic`: To specify ETA calculation on the basis of live traffic. If `speedTypes` is `traffic`, then input `date_time` value of `0,""` is required.

    The default value is `optimal`.


### Optional Parameters

1. `date_time`: This is the local date and time at the source location along with its type. The date and time is specified in ISO 8601 format (YYYY-MM-DDThh:mm) in the local time zone of departure. For example `2020-07-24T12:00`. Applicable types are: 
	- `0`: Current departure time.
	- `1`: Specified departure time.
    - `2`: Specified arrival time. 
- Example: `date_time=1,2021-12-20T11:00`


## Response Type
JSON: response will served as JSON


## Response Parameters

1. `sources`: array of arrays of source coordinates object.
	- `lon`: Longitude of the source in degrees.
	- `lat`: Latitude of the source in degrees.
2. `targets`: array of arrays of target coordinates object.
	- `lon`: Longitude of the target in degrees.
	- `lat`: Latitude of the target in degrees.
3. `sources_to_targets`: Returns an array of time and distance between the sources and the targets. The array is row-ordered. This means that the time and distance from the first location to all targets forms the first row of the array, followed by the time and distance from the second source location to all target locations, etc.
	- `distance` - The computed distance between each set of points in units specified by the `units` response parameter.
	- `time` - Time in seconds. The computed time between each set of points.
	- `from_index` - The origin index into the locations array.
    - `to_index` - The destination index into the locations array.
5.  `units`: Distance units for output. Allowable unit types are mi (miles) and km (kilometers). If no unit type is specified, the units defaults to kilometers.

### Optional Parametes for `trucking` profile

1. `height`: (float)  - The height of the truck (in meters).
2. `width`: (float)  - The width of the truck (in meters).
3. `length`: (float)  - The length of the truck (in meters). Default is `21.64`.
4. `weight`: (float)  - The weight of the truck (in metric tons). Default is `21.77`.
5. `axle_load`: (float)  - The axle load of the truck (in metric tons). Default is `9.07`.
6. `hazmat`: (boolean)  - A value indicating if the truck is carrying hazardous materials. Default is `false`.


## Response Codes {as HTTP response code}


| Status Code |	Status | Description
| --- | --- | --- |
| 	200	 | 	Successful Response	 | 	A happy bit of json describing your result
| 	400	 | 	Failed to parse request	 | 	You need a valid request
| 	400	 | 	Failed to parse location	 | 	You need a valid location object in your json request
| 	400	 | 	Failed to parse correlated location	 | 	There was a problem with the location once correlated to the routing network
| 	400	 | 	No profile provided	 | 	You forgot the profile parameter
| 	400	 | 	Insufficient number of locations provided	 | 	You didn't provide enough locations
| 	400/401	 | 	Exceeded max route locations of X	 | 	You are asking for too many locations
| 	400	 | 	Locations are in unconnected regions.  | 	You are routing between regions of no connectivity
| 	400	 | 	No profile method found for 'X'	 | 	You are asking for a non-existent profile mode
| 	400	 | 	No suitable road network near location	 | 	There were no roads applicable to your mode of travel near the input location
| 	400	 | 	No data found for location	 | 	There was no route data found at the input location
| 	400	 | 	No path could be found for input	 | 	There was no path found between the input locations
| 401 | Unauthorized | Developer’s key is not allowed to send a request |
| 403 | Forbidden | Developer’s key has hit its daily/hourly limit.
| 	405	 | 	Try a GET request instead	 | 	We only support GET requests
| 	412	 | 	Precondition Failed	 | 	Mandatory parameter is missing
| 	500	 | 	Internal Server Error	 | 	The request caused an error in our systems.
| 	501	 | 	Not implemented	 | 	Not Implemented
| 503 | Service Unavailable | Maintenance break or server down-times

## Sample Response
```json
{
    "sources_to_targets": [
        [
            {
                "from_index": 0,
                "distance": 23.366,
                "time": 1860,
                "to_index": 0
            }
        ]
    ],
    "sources": [
        [
            {
                "lon": 77.268931,
                "lat": 28.550614
            }
        ]
    ],
    "units": "kilometers",
    "targets": [
        [
            {
                "lon": 77.085725,
                "lat": 28.555391
            }
        ]
    ]
}
```

## Live Demo

[Not applicable]

<br><br>
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




<div align="center">@ Copyright 2022 CE Info Systems Ltd. All Rights Reserved.</div>

<div align="center"> <a href="https://about.mappls.com/api/terms-&-conditions">Terms & Conditions</a> | <a href="https://about.mappls.com/about/privacy-policy">Privacy Policy</a> | <a href="https://about.mappls.com/pdf/mapmyIndia-sustainability-policy-healt-labour-rules-supplir-sustainability.pdf">Supplier Sustainability Policy</a> | <a href="https://about.mappls.com/pdf/Health-Safety-Management.pdf">Health & Safety Policy</a> | <a href="https://about.mappls.com/pdf/Environment-Sustainability-Policy-CSR-Report.pdf">Environmental Policy & CSR Report</a>

<div align="center">Customer Care: +91-9999333223</div>
[<img src="https://about.mappls.com/about/images/MAPPLS-MapmyIndia-logo.png" height="40"/> </p>](https://about.mappls.com/api/)

# Mappls Snap to Road V2 API

**Easy To Integrate Maps & Location APIs & SDKs For Web & Mobile Applications**

Powered with India's most comprehensive and robust mapping functionalities.

You can get your api key to be used in this document here: [https://about.mappls.com/api/](https://about.mappls.com/api/)

## Disclaimer
1. This API is released for select use cases only; Please contact Mappls API Support or your account manager for discussions on usage of this solution. 
2. Mappls reserves the right to revoke access of this API at its own discrection.  

## Introduction

The `trace_route` variant of Snap to Road V2 API requires two parameters: a costing mode and a series of latitude and longitude coordinates. This function is designed to transform these coordinates, typically obtained from a GPS trace, into a route that closely follows the road network. Additionally, it generates a set of guidance directions for navigation purposes.

  
## Getting Access

Before using the API in the your solution, please ensure that the related access is enabled in the [Mappls Console](https://auth.mappls.com/console/), within your app - be it for Mobile OR Web or Cloud integration.

1. Copy and paste the key from your `credentials` section from your API [keys](https://auth.mappls.com/console/) into the `access_token` query parameter.
    - Your static key can be secured by whitelisting its usage for particular IPs (in case of cloud app usage) OR a set of domains (in case of a web app)
    - Your static key obtained from your Console is to be passed as a query parameter: `access_token`.

## Authentication Object - `access_token` mandatory query parameter.

-  `access_token`: "hklmgbwzrxncdyavtsuojqpiefrbhqplnm".

## Input Method
POST

## Contructing the request cURL

```c
curl --location 'https://route.mappls.com/routev2/movement/trace_route&access_token=hklmgbwzrxncdyavtsuojqpiefrbhqplnm' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'points=72.8632,21.207756;72.86322,21.207582;72.86325,21.207506;72.86324,21.207438;72.86321,21.207426;72.8632,21.207474;72.8632,21.207546;72.86319,21.20757;72.863174,21.207487;72.863174,21.20747;72.86319,21.20743;72.863174,21.207357;72.863144,21.2073;72.862976,21.207394;72.86255,21.207676;72.86244,21.207796;72.86244,21.207764' \
--data-urlencode 'type=break' \
--data-urlencode 'search_radius=12'
```

## Request Parameters

### Mandatory Parameters

1. `points`: set of sequential (time-based sequence) coordinates as pairs of longitude,latitude separated by a semicolon. At present maximum number of points is limited to 100 in a single request.
For example 77.983936,28.255904;77.05993,28.487555.
2. `type`: (string) type of additional actions applicable. Valid values: 
    - `break`: split the route response into multiple legs.
    As of now only one `type` is applicable.

### Optional Parameters

1. `search_radius`: Limits the search of nearest snappable road network to the given radius in meters.


## Response Type
JSON: response will served as JSON

## Response Parameters

1.  `tracepoints` (array of objects): each containing:     
    -   `matchings_index` (integer)
    -   `waypoint_index` (integer)
    -   `alternatives_count` (integer)
    -   `distance` (float)
    -   `name` (string)
    -   `location` (list of float values, latitude and longitude)
2.  `code` (string): status message of the request
3.  `matchings`(array of objects): each containing    
    -   `weight_name` (string): MMI Internal Usage for debugging purposes.
    -   `weight` (float)
    -   `duration` (float) in seconds of the road section to which the raw input was snapped to & not considering live traffic. 
    -   `distance` (float) in meters of the road section to which the raw input was snapped to.
    -   `legs` (array of objects): each containing: 
        -   `weight` (float): Internal usage.
        -   `duration` (float): in seconds between successive location sent for snapping as per road section snapped to.
        -   `steps` (array): empty array as of now.
        -   `distance` (float):in meters between successive location sent for snapping as per road section snapped to. 
        -   `summary` (string): Not processed as of now.
    - `geometry`(string): the 1e5 standard encoded polyline of the snapped road section.
    - `confidence`(float): Confidence with which the snapping has been performed to the provided geometry. Values range between 0 & 1.

## Response Codes {as HTTP response code}


| Status Code |	Status | Description
| --- | --- | --- |
| 	200	 | 	Successful Response	 | 	A happy bit of json describing your result
| 	400	 | 	Failed to parse request	 | 	You need a valid request
| 	400	 | 	Failed to parse location	 | 	You need a valid location object in your json request
| 	400	 | 	Failed to parse correlated location	 | 	There was a problem with the location once correlated to the routing network
| 	~~400~~	 | 	~~No profile provided~~	 | 	~~You forgot the profile parameter~~
| 	400	 | 	Insufficient number of locations provided	 | 	You didn't provide enough locations
| 	400/401	 | 	Exceeded max route locations of X	 | 	You are asking for too many locations
| 	400	 | 	Locations are in unconnected regions.  | 	You are routing between regions of no connectivity
| 	~~400~~	 | 	~~No profile method found for 'X'~~	 | 	~~You are asking for a non-existent profile mode~~
| 	400	 | 	No suitable road network near location	 | 	There were no roads applicable to your mode of travel near the input location
| 	400	 | 	No data found for location	 | 	There was no route data found at the input location
| 	400	 | 	No path could be found for input	 | 	There was no path found between the input locations
| 401 | Unauthorized | Developer’s key is not allowed to send a request |
| 403 | Forbidden | Developer’s key has hit its daily/hourly limit.
| 	405	 | 	Incorrect Method	 | 	Use valid HTTP method
| 	412	 | 	Precondition Failed	 | 	Mandatory parameter is missing
| 	500	 | 	Internal Server Error	 | 	The request caused an error in our systems.
| 	501	 | 	Not implemented	 | 	Not Implemented
| 503 | Service Unavailable | Maintenance break or server downtime


## Sample Response

```json

{
    "tracepoints": [
        {
            "matchings_index": 0,
            "waypoint_index": 0,
            "alternatives_count": 0,
            "distance": 10.22,
            "name": "",
            "location": [
                72.863187,
                21.207665
            ]
        },
        {
            "matchings_index": 0,
            "waypoint_index": 1,
            "alternatives_count": 0,
            "distance": 1.361,
            "name": "",
            "location": [
                72.863207,
                21.207579
            ]
        },
        {
            "matchings_index": 0,
            "waypoint_index": 2,
            "alternatives_count": 0,
            "distance": 2.585,
            "name": "",
            "location": [
                72.863226,
                21.207501
            ]
        },
        {
            "matchings_index": 0,
            "waypoint_index": 3,
            "alternatives_count": 0,
            "distance": 0.0,
            "name": "",
            "location": [
                72.863241,
                21.207438
            ]
        },
        {
            "matchings_index": 0,
            "waypoint_index": 4,
            "alternatives_count": 0,
            "distance": 3.38,
            "name": "",
            "location": [
                72.863242,
                21.207433
            ]
        },
        {
            "matchings_index": 0,
            "waypoint_index": 5,
            "alternatives_count": 0,
            "distance": 6.337,
            "name": "",
            "location": [
                72.863242,
                21.207433
            ]
        },
        {
            "matchings_index": 0,
            "waypoint_index": 6,
            "alternatives_count": 0,
            "distance": 37.068,
            "name": "",
            "location": [
                72.863291,
                21.207224
            ]
        },
        {
            "matchings_index": 0,
            "waypoint_index": 7,
            "alternatives_count": 0,
            "distance": 39.847,
            "name": "",
            "location": [
                72.863269,
                21.20722
            ]
        },
        {
            "matchings_index": 0,
            "waypoint_index": 8,
            "alternatives_count": 0,
            "distance": 31.145,
            "name": "",
            "location": [
                72.863239,
                21.207214
            ]
        },
        {
            "matchings_index": 0,
            "waypoint_index": 9,
            "alternatives_count": 0,
            "distance": 29.299,
            "name": "",
            "location": [
                72.863239,
                21.207214
            ]
        },
        {
            "matchings_index": 0,
            "waypoint_index": 10,
            "alternatives_count": 0,
            "distance": 24.592,
            "name": "",
            "location": [
                72.863239,
                21.207214
            ]
        },
        {
            "matchings_index": 0,
            "waypoint_index": 11,
            "alternatives_count": 0,
            "distance": 16.978,
            "name": "",
            "location": [
                72.863207,
                21.207208
            ]
        },
        {
            "matchings_index": 0,
            "waypoint_index": 12,
            "alternatives_count": 0,
            "distance": 13.933,
            "name": "",
            "location": [
                72.863091,
                21.207185
            ]
        },
        {
            "matchings_index": 0,
            "waypoint_index": 13,
            "alternatives_count": 0,
            "distance": 14.391,
            "name": "",
            "location": [
                72.86284,
                21.207367
            ]
        },
        {
            "matchings_index": 0,
            "waypoint_index": 14,
            "alternatives_count": 0,
            "distance": 12.871,
            "name": "",
            "location": [
                72.862671,
                21.207699
            ]
        },
        {
            "matchings_index": 0,
            "waypoint_index": 15,
            "alternatives_count": 0,
            "distance": 6.755,
            "name": "",
            "location": [
                72.862376,
                21.207784
            ]
        },
        {
            "matchings_index": 0,
            "waypoint_index": 16,
            "alternatives_count": 0,
            "distance": 6.047,
            "name": "",
            "location": [
                72.862383,
                21.207753
            ]
        }
    ],
    "code": "Ok",
    "matchings": [
        {
            "weight_name": "auto",
            "weight": 773.477,
            "duration": 95.636,
            "distance": 245.203,
            "legs": [
                {
                    "weight": 5.155,
                    "duration": 3.495,
                    "steps": [],
                    "distance": 9.708,
                    "summary": ""
                },
                {
                    "weight": 4.718,
                    "duration": 3.198,
                    "steps": [],
                    "distance": 8.884,
                    "summary": ""
                },
                {
                    "weight": 3.787,
                    "duration": 2.568,
                    "steps": [],
                    "distance": 7.133,
                    "summary": ""
                },
                {
                    "weight": 0.336,
                    "duration": 0.228,
                    "steps": [],
                    "distance": 0.632,
                    "summary": ""
                },
                {
                    "weight": 0.0,
                    "duration": 0.0,
                    "steps": [],
                    "distance": 0.0,
                    "summary": ""
                },
                {
                    "weight": 12.554,
                    "duration": 8.511,
                    "steps": [],
                    "distance": 23.642,
                    "summary": ""
                },
                {
                    "weight": 1.038,
                    "duration": 0.847,
                    "steps": [],
                    "distance": 2.353,
                    "summary": ""
                },
                {
                    "weight": 1.393,
                    "duration": 1.137,
                    "steps": [],
                    "distance": 3.158,
                    "summary": ""
                },
                {
                    "weight": 0.0,
                    "duration": 0.0,
                    "steps": [],
                    "distance": 0.0,
                    "summary": ""
                },
                {
                    "weight": 0.0,
                    "duration": 0.0,
                    "steps": [],
                    "distance": 0.0,
                    "summary": ""
                },
                {
                    "weight": 1.437,
                    "duration": 1.173,
                    "steps": [],
                    "distance": 3.258,
                    "summary": ""
                },
                {
                    "weight": 5.394,
                    "duration": 4.403,
                    "steps": [],
                    "distance": 12.231,
                    "summary": ""
                },
                {
                    "weight": 630.297,
                    "duration": 20.187,
                    "steps": [],
                    "distance": 46.767,
                    "summary": ""
                },
                {
                    "weight": 43.638,
                    "duration": 16.771,
                    "steps": [],
                    "distance": 46.587,
                    "summary": ""
                },
                {
                    "weight": 61.886,
                    "duration": 31.868,
                    "steps": [],
                    "distance": 77.375,
                    "summary": "Abhaynagar Society Road"
                },
                {
                    "weight": 1.844,
                    "duration": 1.25,
                    "steps": [],
                    "distance": 3.473,
                    "summary": ""
                }
            ],
            "geometry": "aflmg@e|e~iCjDg@zCe@|B]HA??`LaBFj@Jz@????J~@l@fFvAjKcMhB{MlBYFORLjCSTm@N}ATcQ~BpBlOfH_A|@M",
            "confidence": 1.0
        }
    ]
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
[<img src="https://about.mappls.com/about/images/MAPPLS-MapmyIndia-logo.png" height="40"/> </p>](https://about.mappls.com/api/)

# Mappls Routing API for Predictive ETA

**Easy To Integrate Maps & Location APIs & SDKs For Web & Mobile Applications**

Powered with India's most comprehensive and robust mapping functionalities.

You can get your api key to be used in this document here: [https://about.mappls.com/api/](https://about.mappls.com/api/)

## Disclaimer
1. This API is released for select use cases only; Please contact Mappls API Support or your account manager for discussions on usage of this solution. 
2. Mappls reserves the right to revoke access of this API at its own discrection.

## [Introduction](#Introduction)

This API computes optimal routes between two or more specified locations. The API supports both live and predictive traffic to calculate ETAs based on arrival or departure time.
Optionally one can specify the `date_time` parameter and get the optimal route for that part of day of the week. Time based functionality is available for selected areas only.
Supported region (countries) is India at the moment. Please note that maximum number of points are limited to 100 only including source and destination positions. 

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

## Contructing the request cURL

```c
curl --location --request GET 'https://apis.mappls.com/advancedmaps/v2/route?locations=80.014307,12.993915;81.835378,25.358969&profile=driving&speedTypes=optimal&date_time=0,""' \
--header 'Authorization: bearer 0XXXXXXf-dXX0-4XX0-8XXa-eXXXXXXXXXX6'
```

## Request Parameters

### Mandatory Parameters

1.  `locations`: (string) A set of comma separated longitude & latitude values - first coordinate pair will be considered as start point (mandatory) & a last coordinate pair will be considered as end point (mandatory) and those in between are via points (optional). Multiple locations are seperated by semicolon (;).
	- For example `80.014307,12.993915;80.070466,13.1723473;81.835378,25.358969`.
2. `profile`:  (string) Profile for routing engine. Applicable values are:
    - `driving`
    - `trucking`
    - `biking`
    - `walking`

    Example `profile=driving`.
3. `speedTypes`: (string) To specify the type of ETA calculations. Available values are: 
	- `predictive`: (default) - used to specify predictive ETA calculation. In case if this is used, then the optional parameter of `date_time` becomes mandatory.
	- `optimal`: To specify ETA calculation acc. to current time. The `date_time` parameter is not required in this case.
    - `traffic`: To specify ETA calculation according to live traffic conditions. In this case, `date_time` parameter should be set to `0,""`
4. `date_time`: (string) This is the local date and time at the source location along with its type. The date and time is specified in ISO 8601 format (YYYY-MM-DDThh:mm) in the local time zone of departure. For example `2020-07-24T12:00`. Applicable types are: 
	- `0`: Current departure time.
	- `1`: Specified departure time.
    - `2`: Specified arrival time. 

    Example: `date_time=1,2021-12-20T11:00`


### Optional Parameters

1. `alternatives`: (string) A number denoting how many alternate routes should be provided. There may be no alternates or less alternates than the user specifies. Alternates are not supported on multipoint routes (that is, routes with more than 2 locations). They are also not supported on time dependent routes.
2. `heading`: (integer) Preferred direction of travel for the start from the location. This can be useful for mobile routing where a vehicle is traveling in a specific direction along a road, and the route should start in that direction. The heading is indicated in degrees from north in a clockwise direction, where north is 0°, east is 90°, south is 180°, and west is 270°.
3. `heading_tolerance`: (integer) How close in degrees a given street's angle must be in order for it to be considered as in the same direction of the heading parameter. The default value is 60 degrees.
4. `preferred_side`: (string) If the location is not offset from the road centerline or is closest to an intersection this option has no effect. Otherwise the determined side of street is used to determine whether or not the location should be visited from the same, opposite or either side of the road with respect to the side of the road the given locale drives on. In Germany (driving on the right side of the road), passing a value of same will only allow you to leave from or arrive at a location such that the location will be on your right. In Australia (driving on the left side of the road), passing a value of same will force the location to be on your left. A value of opposite will enforce arriving/departing from a location on the opposite side of the road from that which you would be driving on while a value of either will make no attempt limit the side of street that is available for the route.

    Applicable values are: 
    - `left`
    - `right`
    - `opposite`
5. `search_cutoff`: (integer) The cutoff at which we will assume the input is too far away from civilisation to be worth correlating to the nearest graph elements.
6. `avoid_locations`: (array of locations) A set of locations to exclude or avoid within a route can be specified using a JSON array of `avoid_locations`. The `avoid_locations` have the same format as the locations list. At a minimum each avoid location must include latitude and longitude. The `avoid_locations` are mapped to the closest road or roads and these roads are excluded from the route path computation.
7. `avoid_polygons`: (array of polygons) One or multiple exterior rings of polygons in the form of nested JSON arrays.  Roads intersecting these rings will be avoided during path finding. If you only need to avoid a few specific roads, it's much more efficient to use `avoid_locations`. API will close open rings (i.e. copy the first coordinate to the last position).
    - example: `[[[lon1,lat1], [lon2,lat2]],[[lon1,lat1],[lon2,lat2]]].`
8. `id`: (string) Name your route request. If id is specified, the naming will be sent through.
9. `use_ferry`: (float) This value indicates the willingness to take ferries. This is a range of values between 0 and 1. Values near 0 attempt to avoid ferries and values near 1 will favor ferries. The default value is 0.5. Note that sometimes ferries are required to complete a route so values of 0 are not guaranteed to avoid ferries entirely.
10. `use_highways`: (float) This value indicates the willingness to take highways. This is a range of values between 0 and 1. Values near 0 attempt to avoid highways and values near 1 will favor highways. The default value is 1.0. Note that sometimes highways are required to complete a route so values of 0 are not guaranteed to avoid highways entirely.
11. `search_filter`: (string) A set of optional filters to exclude candidate edges based on their attribution. The following exclusion filters are supported:
    - `exclude_tunnel`  - (boolean, defaults to false): whether to exclude roads marked as tunnels.
    - `exclude_bridge`  - (boolean, defaults to false): whether to exclude roads marked as bridges.
    - `exclude_road_class`  - (string, defaults to "service_other"): whether to exclude roads class. Road classes from highest to lowest are: 
        - motorway, 
        - trunk, 
        - primary, 
        - secondary, 
        - tertiary, 
        - unclassified, 
        - residential. 
### Optional Parametes for `trucking` profile

1. `height`: (float)  - The height of the truck (in meters).
2. `width`: (float)  - The width of the truck (in meters).
3. `length`: (float)  - The length of the truck (in meters). Default is `21.64`.
4. `weight`: (float)  - The weight of the truck (in metric tons). Default is `21.77`.
5. `axle_load`: (float)  - The axle load of the truck (in metric tons). Default is `9.07`.
6. `hazmat`: (boolean)  - A value indicating if the truck is carrying hazardous materials. Default is `false`.


## Response Type

`Content-Type: application/json`

## Response Parameters

- `trip`: Object containing API response.
    1. `summary`:
        - `min_lon`: (decimal) The minimal longitudinal view bound to show the route on map. 
        - `max_lat`: (decimal) The maximum latitudinal view bound to show the route on map.
        - `cost`: 
        - `max_lon`: (decimal) The maximum longitudinal view bound to show the route on map.
        - `length`: (float) The distance of the route in kilometres.
        - `time`: (float) The duration of the route in seconds.
        - `min_lat`: (decimal) The minimal latitudinal view bound to show the route on map.
        - `has_time_restrictions`:	(boolean) indicates whether the proposed route has any segments where travel is time restricted.
    2. `status_message`	- description of the status (e.g. "Found route between points")
    3. `language` - language of the output displayed(e.g. en-US)
    4. `legs`: array of route object
        - `summary`:
            - `min_lon`: (decimal) The minimal longitudinal view bound to show the route on map. 
            - `max_lat`: (decimal) The maximum latitudinal view bound to show the route on map.
            - `cost`: 
            - `max_lon`: (decimal) The maximum longitudinal view bound to show the route on map.
            - `length`: (float) The distance of the route in kilometres.
            - `time`: (float) The duration of the route in seconds.
            - `min_lat`: (decimal) The minimal latitudinal view bound to show the route on map.
            - `has_time_restrictions`:	(boolean) indicates whether the proposed route has any segments where travel is time restricted.
        - `shape`: (string) geometry of the route.
        - `maneuvers`: (array) set of maneuver objects, each containing: 
            - `verbal_multi_cue`: (boolean) If the maneuver has multiple verbal instructions that need to be followed at the same point. <br>
                Example: `Drive south. Then Turn right.`
            - `cost`: (float) 
            - `begin_shape_index`: (integer) 
            - `travel_mode`: (string) The mode prescribed by the api for this maneuver.
            - `instruction`: (string) The short instruction for this maneuver.
            - `length`: (decimal) The distance in kms from the previous maneuver to this maneuver.
            - `end_shape_index`: (integer) 
            - `verbal_post_transition_instruction`: (string) The post instruction that should be provided as audible feedback to user after traversing this maneuver.
            - `time`: (float) The time in seconds from the previous maneuver to this maneuver.
            - `type`: (integer) The type of this maneuver.
            - `roundabout_exit_count`: (integer) The exit number from the roundabout maneuver counting in the direction of travel from the spoke from which one enters the roundabout. 
            - `verbal_pre_transition_instruction`: (string) Any pre-transition instruction that should be spoken out to user before one traverses the maneuver.
            - `travel_type`: (string) The proposed vehicular mode of transport for this traversing this maneuver.
            - `sign`: (object) contains the road signages applicable for undertaking this maneuver that aids the user.
                - `exit_branch_elements`: (array of objects) Exit road signages for performing an exit from a major road.
                    - `text`: (string) text that needs to be presented to user as applicable exit signage for this maneuver. 
            - `verbal_transition_alert_instruction`: (string) Instructions that need to be spoken out to the user before one traverses the maneuver. 
            - `street_names`: (array of string) The array of street names that indicate which street the particular maneuver traverses / intersects.
    5. `locations`: (array of location objects)
		 - `lon`: (decimal)
		 - `type`: (string)
		 - `lat`: (decimal)
         - `date_time`: (string)
         - `original_index`: (integer)
    6. `language`: The language of API response, Default is `"en-US"`.
	7. `units`: (string)  Unit of distance Default is `"kilometers"`.
    8. `status`: 
-  `id`: (string) The identity or name of your route request. This is the same value as you pass in the `id` request parameter.


## Response Codes {as HTTP response code}


| Status Code |	Status | Description
| --- | --- | --- |
| 	200	 | 	Successful Response	 | 	A happy bit of json describing your result
| 	400	 | 	Failed to parse request	 | 	You need a valid request
| 	400	 | 	Failed to parse location	 | 	You need a valid location object in your json request
| 	400	 | 	Failed to parse correlated location	 | 	There was a problem with the location once correlated to the routing network
| 	400	 | 	No costing provided	 | 	You forgot the costing parameter
| 	400	 | 	Insufficient number of locations provided	 | 	You didn't provide enough locations
| 	400/401	 | 	Exceeded max route locations of X	 | 	You are asking for too many locations
| 	400	 | 	Locations are in unconnected regions.  | 	You are routing between regions of no connectivity
| 	400	 | 	No costing method found for 'X'	 | 	You are asking for a non-existent costing mode
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


## Sample cURL Request

```c
curl --location --request GET 'https://apis.mappls.com/advancedmaps/v2/route?locations=77.231416,28.6186381;77.2355289,28.627248&profile=driving&speedTypes=traffic&date_time=0,""' \
--header 'Authorization: bearer 0XXXXXXf-dXX0-4XX0-8XXa-eXXXXXXXXXX6'
```

## Sample Response
```json
{
    "trip": {
        "summary": {
            "min_lon": 77.231443,
            "max_lat": 28.627248,
            "cost": 874.345,
            "max_lon": 77.23588,
            "length": 1.499,
            "time": 211.16,
            "min_lat": 28.618635,
            "has_time_restrictions": false
        },
        "status_message": "Found route between points",
        "legs": [
            {
                "summary": {
                    "min_lon": 77.231443,
                    "max_lat": 28.627248,
                    "cost": 874.345,
                    "max_lon": 77.23588,
                    "length": 1.499,
                    "time": 211.16,
                    "min_lat": 28.618635,
                    "has_time_restrictions": false
                },
                "shape": "wwvqu@uuyhrCkVi@ag@sAeR]i]_Ai]}@sd@iAeFIaGSgQy@qSWmQe@uEEqMk@oCIoO_@gWa@uj@oByJUoW[oDGuFTm@rEcBhFiCtCaDnB_Br@mBf@}FZqBQuDa@kA[kBw@uBkBuAuBq@yA{@qBm@cCe@}DOyE@uAZ{CbAqD|AwCjAkAtCqBbEyArDi@b@sQ|@u`@d@gVPmJtAmn@dAuo@c@eZac@y@{[m@iWg@k@tRQj@c@L_Ie@",
                "maneuvers": [
                    {
                        "cost": 139.803,
                        "begin_shape_index": 0,
                        "travel_mode": "drive",
                        "instruction": "Drive north on Copernicus Marg.",
                        "street_names": [
                            "Copernicus Marg"
                        ],
                        "length": 0.736,
                        "end_shape_index": 21,
                        "verbal_post_transition_instruction": "Continue for 700 meters.",
                        "time": 98.497,
                        "type": 1,
                        "verbal_pre_transition_instruction": "Drive north on Copernicus Marg.",
                        "travel_type": "car"
                    },
                    {
                        "cost": 37.389,
                        "begin_shape_index": 21,
                        "street_names": [
                            "Rotary Number 6"
                        ],
                        "length": 0.223,
                        "verbal_transition_alert_instruction": "Enter Rotary Number 6 and take the 8th exit onto Sikandra Road.",
                        "type": 26,
                        "roundabout_exit_count": 8,
                        "travel_mode": "drive",
                        "instruction": "Enter Rotary Number 6 and take the 8th exit onto Sikandra Road.",
                        "end_shape_index": 47,
                        "time": 32.059,
                        "verbal_pre_transition_instruction": "Enter Rotary Number 6 and take the 8th exit onto Sikandra Road.",
                        "travel_type": "car"
                    },
                    {
                        "cost": 56.032,
                        "begin_shape_index": 47,
                        "travel_mode": "drive",
                        "instruction": "Exit the roundabout onto Sikandra Road.",
                        "street_names": [
                            "Sikandra Road"
                        ],
                        "length": 0.329,
                        "end_shape_index": 54,
                        "verbal_post_transition_instruction": "Continue for 300 meters.",
                        "time": 51.788,
                        "type": 27,
                        "verbal_pre_transition_instruction": "Exit the roundabout onto Sikandra Road.",
                        "travel_type": "car"
                    },
                    {
                        "cost": 629.36,
                        "begin_shape_index": 54,
                        "travel_mode": "drive",
                        "instruction": "Turn left.",
                        "length": 0.158,
                        "end_shape_index": 57,
                        "verbal_transition_alert_instruction": "Turn left.",
                        "verbal_post_transition_instruction": "Continue for 200 meters.",
                        "time": 20.546,
                        "type": 15,
                        "verbal_pre_transition_instruction": "Turn left.",
                        "travel_type": "car"
                    },
                    {
                        "verbal_multi_cue": true,
                        "cost": 11.76,
                        "begin_shape_index": 57,
                        "length": 0.053,
                        "verbal_transition_alert_instruction": "Turn left.",
                        "type": 15,
                        "travel_mode": "drive",
                        "instruction": "Turn left.",
                        "end_shape_index": 61,
                        "verbal_post_transition_instruction": "Continue for 50 meters.",
                        "time": 8.267,
                        "verbal_pre_transition_instruction": "Turn left. Then You will arrive at your destination.",
                        "travel_type": "car"
                    },
                    {
                        "cost": 0.0,
                        "begin_shape_index": 61,
                        "travel_mode": "drive",
                        "instruction": "You have arrived at your destination.",
                        "length": 0.0,
                        "end_shape_index": 61,
                        "verbal_transition_alert_instruction": "You will arrive at your destination.",
                        "time": 0.0,
                        "type": 4,
                        "verbal_pre_transition_instruction": "You have arrived at your destination.",
                        "travel_type": "car"
                    }
                ]
            }
        ],
        "locations": [
            {
                "original_index": 0,
                "date_time": "current",
                "lon": 77.231416,
                "type": "break",
                "lat": 28.618638
            },
            {
                "original_index": 1,
                "lon": 77.235528,
                "type": "break",
                "lat": 28.627248
            }
        ],
        "language": "en-US",
        "units": "kilometers",
        "status": 0
    },
    "id": "What are clouds made of?"
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




<div align="center">@ Copyright 2022 CE Info Systems Ltd. All Rights Reserved.</div>

<div align="center"> <a href="https://about.mappls.com/api/terms-&-conditions">Terms & Conditions</a> | <a href="https://about.mappls.com/about/privacy-policy">Privacy Policy</a> | <a href="https://about.mappls.com/pdf/mapmyIndia-sustainability-policy-healt-labour-rules-supplir-sustainability.pdf">Supplier Sustainability Policy</a> | <a href="https://about.mappls.com/pdf/Health-Safety-Management.pdf">Health & Safety Policy</a> | <a href="https://about.mappls.com/pdf/Environment-Sustainability-Policy-CSR-Report.pdf">Environmental Policy & CSR Report</a>

<div align="center">Customer Care: +91-9999333223</div>
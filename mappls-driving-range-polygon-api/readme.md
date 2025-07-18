[<img src="https://about.mappls.com/about/images/MAPPLS-MapmyIndia-logo.png" height="40"/> </p>](https://about.mappls.com/api/)

# Driving Range Polygon API

## Introduction
Mappls Driving Range Polygon API computes areas that are reachable within specified time or distance intervals from a location, and returns the reachable regions as contours of polygons or lines that you can display on a map. This create the drive time polygons that use actual street networks based on given distance or time. This is required in order to quickly determine how much time or distance one will need to get to other locations on map and in specified time where can he reached.

## What it looks like

<img src="../docs/images/driving-range-polygon1.gif?raw=true" style="margin-left:auto;margin-right:auto"/>

<!-- ![](https://mappls-api.github.io/mappls-rest-apis/images/driving-range-polygon1.gif) -->

> In the above clip, you can see the driving range calculated from Bhuntar Airport, Kullu for a 30 mins (purple) and a 60 mins (pink) driving range. 

## Getting Access

Before using the API in the your solution, please ensure that the related access is enabled in the [Mappls Console](https://apis.mappls.com/console/), in the same project you set up for the Maps SDK.

1. Copy and paste the generated `access token` from your API [keys](https://apis.mappls.com/console/) available in the dashboard in the sample code for interactive map development.
    - This APIs follow OAuth2 based security.
    - `Access Token` can be generated using Token Generation API.
    - To know more on how to create your access tokens, please use our authorization API URL. More details available [here](https://github.com/mappls-api/mappls-rest-apis/tree/main/mappls-token-generation-api)
    - The `access token` is a valid by default for 24 hours from the time of generation. This can be configured by you in the API console.
2. **`Security Type`**
    
    This APIs follow OAuth2 based security. **To know more on how to create your authorization tokens, please use our authorization token URL. More details available**  [here](https://github.com/mappls-api/mappls-rest-apis/tree/main/mappls-token-generation-api)

## URL

```html
https://apis.mappls.com/advancedmaps/v2/isopolygon?
```

## Input Method

GET

## Request Headers

The API leverages OAuth 2.0 based security. Hence, the developer would need to send a request for access token using their client_id and client_secret to the OAuth API. Once validated from the OAuth API, the access_token and the token_type need to be sent as Authorization header with the value: “{token_type} {access_token}”.

-  `Authorization:  “token_type access_token”`.

## Request Parameters

### Mandatory Parameters

1.  `locations`: Location which will be center point for driving range polygon that will surrounded by roads which can be reached from this point in specified time or distance range(s). The input is supported as a latitude,longitude in decimal degrees.
	- For example `28.555390931473642,77.08572454324664`.
2. `rangeType`: To specify the type of range which is used to calculate the polygon. Default value is "time". Acceptable values are:   
	- `time`: to specify driving range calculation reachable within the specified time.
    - `distance`: to specify driving range calculation reachable within the specified distance from the reference position specified in the `locations` parameter.
3. `costing`:  Profile for routing engine. Currently the only applicable profile is set to automatic detection or `auto`. 
	- Example `costing=auto`.
4. `speedTypes`: To specify the type of ETA calculations. Available values are: 
	- `predictive` (default) - used to specify predictive ETA calculation. In case if this is used, then the optional parameter of `date_time` becomes mandatory.
	- `optimal`: To specify ETA calculation acc. to current time.
5. `contours`: An array of contour objects with either time in minutes or distance in kilometers and color to use for each isopolygon contour. One can specify up to five contours.
Input is specified as a pair comprising of: 
    - `time` or `distance`: 
        - `time`: A floating point value specifying the time in minutes and maximun value is 120 minutes.
        - `distance`: A floating point value specifying the distance in kilometer and maximun value is 100 kilometer.
    - `color`: The color for the output of the contour. Specify it as a Hex value, such as "color":"ff0000" for red. If no color is specified, the driving range polygon service will assign a default color to the output.

### Optional Parameters

1. `date_time`: This is the local date and time at the source location along with its type. The date and time is specified in ISO 8601 format (YYYY-MM-DDThh:mm) in the local time zone of departure. For example `2020-07-24T12:00`. Applicable types are: 
	- `0`: Current departure time.
	- `1`: Specified departure time.
        - Example: `date_time=1,2021-12-20T11:00`
2. `denoise`: A floating point value from 0 to 1 (default of 1) which can be used to remove smaller contours. A value of 1 will only return the largest contour for a given time value. A value of 0.5 drops any contours that are less than half the area of the largest contour in the set of contours for that same time/distance value.
3. `polygons`: A boolean value to determine whether to return geojson polygons or linestrings as the contours. The default is false, which returns lines; when true, polygons are returned. Note: When polygons is true, any contour that forms a ring is returned as a polygon.
4. `generalize`: A floating point value in meters used as the tolerance for Douglas-Peucker generalization. Note: Generalization of contours can lead to self-intersections, as well as intersections of adjacent contours.
5. `id`: Name of the input request. If `id` is specified, the same is returned with the response.
6. `show_locations`(boolean): A boolean indicating whether the input locations should be returned as MultiPoint features: one feature for the exact input coordinates and one feature for the coordinates of the network node it snapped to. Default false.

Please contact [API Support](mailto:apisupport@mappls.com) in case you have any queries related to above request parameters.


## Response Status Codes
 

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

```curl
curl --location --request GET 'https://apis.mappls.com/advancedmaps/v2/isopolygon?locations=28.632282,77.218527&costing=auto&rangeType=time&contours=1,ff0000&speedTypes=predictive&date_time=1,2021-12-12T15:00&denoise=0.5&polygons=false&generalize=1.2&id=walk from office&show_locations=true' \
--header 'Authorization: Bearer 0XXXXXXf-dXX0-4XX0-8XXa-eXXXXXXXXXX6'
```

## Document Version History

| Version | Last Updated | Author |
| ---- | ---- | ---- |
| 0.0.1 | June 2022 | Mappls API Team ([KB](https://github.com/kunalbharti)) |

## API Version History

| Version | Last Updated | Author | Revised Sections |
| ---- | ---- | ---- | ---- |
| 0.1 | 2021-06-17 | Mappls API Team ([PS](https://github.com/map-123)) | Initial release |


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
[<img src="https://about.mappls.com/about/images/MAPPLS-MapmyIndia-logo.png" height="40"/> </p>](https://about.mappls.com/api/)
# Mappls Route Image API

**Easy To Integrate Maps & Location APIs & SDKs For Web & Mobile Applications**

Powered with India's most comprehensive and robust mapping functionalities.

You can get your api key to be used in this document here: [https://about.mappls.com/api/](https://about.mappls.com/api/)

## Introduction

This API has two variants:

> Provide a route drawn on a static map on the basis of input origin & destination pair.

OR

> Provide a route drawn on a static map on the basis of the input path of that route.

Both variants differ in the HTTP methods used and features they offer and this document highlights them


## Getting Access

Before using the API in the your solution, please ensure that the related access is enabled in the [Mappls Console](https://auth.mappls.com/console/), within your app - be it for Mobile OR Web or Cloud integration.

1. Copy and paste the key from your `credentials` section from your API [keys](https://auth.mappls.com/console/) into the `access_token` query parameter.
    - Your static key can be secured by whitelisting its usage for particular IPs (in case of cloud app usage) OR a set of domains (in case of a web app)
    - Your static key obtained from your Console is to be passed as a query parameter: `access_token`.

## Authentication Object - `access_token` mandatory query parameter.

-  `access_token`: "hklmgbwzrxncdyavtsuojqpiefrbhqplnm".


## Variants: 
1. GET
2. POST

## 1. GET - Route Image API

### Request Parameters

The following input parameters will be supported in the GET Route Image API request

#### Mandatory Parameters

1. `points` (string) The array of coordinates from origin to destination with optional via points in between. Each coordinate is .separated by a semi-colon. 
<br>Example: "28.550716,77.268928;28.4070,77.8498;27.90,78.0880;27.5981,78.049;27.1767,78.0081;26.7829,79.0276".


#### Optional Parameters
1. `size` (string): size of the image is widthXheight. Min 100X100 & Max 1000X1000; default is 400x400.
2. `color` (string): RGB Color in "R,G,B" values. Default is "0,0,255".
3. `strokeWidth` (number): The stroke width of the route polyline. Min: 1;  max: 8; default: 5.
4. `from_icon` (string): URL for the origin marker.
5. `to_icon` (string): URL for the destination marker.
6. `via_icon` (string): URL for the via-point marker.


## 2. POST Route Image API

### Request Content Type

`Content-Type:application/json` 

### Request Body

The following input properties will be supported in the POST Route Image API request

#### Mandatory Properties

1. `polyline` (array of objects) The Polyline & its properties; each containing: 
    - `color` (string): hexadecimal color code. 
    <br>Example: `#0000FF`
    - `strokeWidth` (integer): number indicating thickness of the polyline drawn on the map.
    <br>Example: `6`
    - `geometry` (array of arrays): Array of longitude, latitude values that indicate the path of the route polyline which needs to be drawn on the map.
    <br>Example: `[77.58416,13.00086]`.


#### Optional Optional Properties
1. `from_icon` (string): URL for the origin marker.
2. `to_icon` (string): URL for the destination marker.
3. `via_icon` (string): URL for the via-point marker.
4. `height` (integer): indicating the height of the map.
5. `width` (integer): indicating the width of the map.

## Response Type

Content-Type: image/png

## Response Codes 
**Note**:  as HTTP response code

### Success
1. 200: To denote a successful API call.
2. 204: To denote the API was a success but no results were found.
### Client-Side Issues
3. 400: Bad Request, User made an error while creating a valid request.
4. 401: Unauthorized, Developer’s key is not allowed to send a request with restricted parameters.
5. 403: Forbidden, Developer’s key has hit its daily/hourly limit.
6. 412: Pre-condition failed; incorrect or invalid combination of input coordinates
Server-Side Issues:
7. 500: Internal Server Error, the request caused an error in our systems.
8. 503: Service Unavailable, during our maintenance break or server down-times.

## Response Messages 

**Note**: as HTTP response message

1. 200: Success.
2. 204: No matches we’re found for the provided query.
3. 400: Something’s just not right with the request.
4. 401: Access Denied.
5. 403: Services for this key has been suspended due to daily/hourly transactions limit.
6. 412: Pre-condition failed; incorrect or invalid combination of input coordinates
7. 500: Something went wrong.
8. 503: Maintenance Break.


## Transaction Information

One request using the API link will be considered as one transaction.

## Sample request

### cURL - GET - Route Image API

```json
curl --location 'https://tile.mappls.com/map/raster_tile/route_image?points=28.550716%2C77.268928%3B28.4070%2C77.8498&size=400x400&color=255%2C0%2C0&strokeWidth=2&from_icon=https%3A%2F%2Fimg.icons8.com%2Fcolor%2F48%2F000000%2Fgreen-flag.png&to_icon=https%3A%2F%2Fimg.icons8.com%2Fdoodle%2F48%2F000000%2Ffinish-flag.png&access_token=hklmgbwzrxncdyavtsuojqpiefrbhqplnm'
```

### cURL - GET - Route Image API

```json
curl --location 'https://tile.mappls.com/map/raster_tile/route_image?access_token=hklmgbwzrxncdyavtsuojqpiefrbhqplnm' \
--header 'Content-Type: application/json' \
--data '{
    "height": 500,
    "width": 500,
    "from_icon": "https://img.icons8.com/color/48/000000/green-flag.png",
    "to_icon": "https://img.icons8.com/doodle/48/000000/finish-flag.png",
    "via_icon": "",
    "polyline": [        
        {
            "color": "#0000FF",
            "strokeWidth": 6,
            "geometry": [
                [
                    77.58416,
                    13.00086
                ],
                [
                    77.58416,
                    13.00065
                ],
                [
                    77.58421,
                    13.00007
                ],
                [
                    77.58421,
                    12.99972
                ],
                [
                    77.58427,
                    12.99877
                ],
                [
                    77.58434,
                    12.99828
                ],
                [
                    77.58439,
                    12.99793
                ],
                [
                    77.58443,
                    12.99773
                ],
                [
                    77.58443,
                    12.99772
                ],
                [
                    77.58446,
                    12.99754
                ],
                [
                    77.58454,
                    12.99709
                ],
                [
                    77.58456,
                    12.99701
                ],
                [
                    77.5846,
                    12.99686
                ],
                [
                    77.58461,
                    12.99684
                ],
                [
                    77.58471,
                    12.99654
                ],
                [
                    77.58474,
                    12.9964
                ],
                [
                    77.58476,
                    12.99634
                ],
                [
                    77.58479,
                    12.99623
                ]                
            ]
        },
        {
            "color": "#DE3500",
            "strokeWidth": 6,
            "geometry": [
                [
                    77.58495,
                    12.99546
                ],
                [
                    77.58498,
                    12.99528
                ],
                [
                    77.58511,
                    12.99469
                ],
                [
                    77.58512,
                    12.99458
                ],
                [
                    77.58514,
                    12.99443
                ],
                [
                    77.58524,
                    12.99376
                ],
                [
                    77.58523,
                    12.99333
                ],
                [
                    77.58529,
                    12.99315
                ],
                [
                    77.58534,
                    12.99301
                ]
            ]
        }
    ]
}'
```

## Sample Response

![](https://mmi-api-team.s3.ap-south-1.amazonaws.com/API-Team/Draw-Route-Image-API.png)

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
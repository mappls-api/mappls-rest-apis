[<img src="https://about.mappls.com/about/images/MAPPLS-MapmyIndia-logo.png" height="40"/> </p>](https://about.mappls.com/api/)
# Mappls Location Verification API 

**Easy To Integrate Maps & Location APIs & SDKs For Web & Mobile Applications**

Powered with India's most comprehensive and robust mapping functionalities.

You can get your api key to be used in this document here: [https://about.mappls.com/api/](https://about.mappls.com/api/)

## Introduction

Introducing our Location Verification API, a robust solution designed to enhance the accuracy and reliability of location-based data through advanced geospatial checks. Developed by Mappls MapmyIndia, this API is an essential tool for any business or application requiring precise location verification, ensuring that addresses and coordinates are not only geographically accurate but also contextually consistent.

In the context of address verification, especially within processes like KYC (Know Your Customer), our API excels by integrating multiple critical steps; such as during the KYC process, customers provide a structured address, which is converted into geographical coordinates through geocoding. Conversely, coordinates captured during field or digital KYC activities are converted back into a recognizable address through reverse geocoding. 

The Location Verification API performs an in-depth comparison between these data points. It checks the radial proximity between the two sets of coordinates, ensuring that they are within an acceptable distance from each other. This step verifies that the address provided by the customer and the physical location captured during verification are aligned geographically.

Furthermore, the API evaluates the consistency of the address hierarchy between the geocoded address and the reverse-geocoded address. This involves comparing administrative levels or tokens—such as country, state, city, and district—between the two addresses to ensure they match. By cross-referencing these administrative tokens, the API ensures that the input address and coordinates not only align spatially but also belong to the same geopolitical context.

This dual-layered approach—combining radial proximity checks with administrative level matching—provides a comprehensive solution for location verification. It guarantees that the specified location is accurate and trustworthy, making it particularly valuable in processes where location integrity is crucial, such as KYC in the BFSI sector, logistics, real estate, or any service dependent on precise location data.

The Location Verification API is designed for ease of integration, offering a straightforward API call structure and extensive documentation to support seamless implementation into existing systems. It is versatile for use across different platforms and industries. Backed by Mappls MapmyIndia’s extensive geospatial data, this API delivers reliable and accurate results every time.

In summary, our Location Verification API is a vital tool for businesses that rely on accurate location data. By ensuring that addresses and coordinates are both geographically proximate and contextually consistent, it adds an extra layer of trust and accuracy to your location-based services. Whether you’re verifying customer addresses during KYC processes or ensuring the accuracy of location data in other contexts, our API offers a powerful, easy-to-integrate solution that enhances the reliability of your operations.


## Live Demo

>Under Construction

## Getting Access

Before using the API in the your solution, please ensure that the related access is enabled in the [Mappls Console](https://auth.mappls.com/console/), within your app - be it for Mobile OR Web or Cloud integration.

1. Copy and paste the key from your `credentials` section from your API [keys](https://auth.mappls.com/console/) into the `access_token` query parameter.
    - Your static key can be secured by whitelisting its usage for particular IPs (in case of cloud app usage) OR a set of domains (in case of a web app)
    - Your static key obtained from your Console is to be passed as a query parameter: `access_token`.

## Authentication Object - `access_token` mandatory query parameter.

-  `access_token`: "hklmgbwzrxncdyavtsuojqpiefrbhqplnm".


## Input Method
POST

## Input URL

```html
http://search.mappls.com/search/address/address-verification
```

## Request Body

### Request Type

Content-Type: `application/json`

### Mandatory Parameters

 - `inputAddress`(string): The structured address provided by the customer. <br> Example: `"inputAddress": "8, Block D, Maurice Nagar, Model Town, North District, New Delhi, Delhi, 110007"`
 - `latitude` (double): latitude of the field location in decimal degrees.
 - `longitude` (double): longitude of the field location in decimal degrees.


### Optional Parameters

- `thresholdMeters` (integer): the threshold for radial proximity check for urban areas that is to be considered a success. In Meters. Default: `200`, mininum: `50`, maximum: `10000`.
- `confidenceThreshold` (double): The threshold for confidence score check to be considered a success. In double ranging from 0 to 1 within single decimal precision. Default: `0.6`
- `geocodeLevelThreshold` (string): The threshold for geocoding level check for urban areas to be considered a success. Default: `locality`. Can be one of the following administrative levels: 
    - `houseNumber`(string): the houseNumber of the address/location.
    - `houseName`(string): houseName of the address/location.
    - `poi`(string): the point of interest or famous landmark nearby the location.
    - `street`(string): the street or road of the location.
    - `subsubLocality`(string): the subSubLocality of the location.
    - `subLocality`(string): the subLocality of the location.
    - `locality`(string): the locality of the location.    
    - `subDistrict`(string): the subDistrict of the location.
    - `district`(string): the district of the location.
    - `city`(string): the city of the location.
    - `state`(string): the state of the location.
    - `pincode`(string): the pincode of the location.  
- `includeDetails` (boolean): To include the details in the administriative hierarchy checks for each admin hierarchy matched. Default: `false`
- `ruralThresholdMeters` (integer):  the threshold for radial proximity check for rural areas that is to be considered a success. In Meters. Default: `200`, mininum: `50`, maximum: `10000`.
- `ruralGeocodeLevelThreshold` (string): The threshold for geocoding level check for rural areas to be considered a success. Default: `village`. Can be one of the following administrative levels: 
  - `houseNumber`(string): the houseNumber of the address/location.
  - `houseName`(string): houseName of the address/location.
  - `poi`(string): the point of interest or famous landmark nearby the location.
  - `street`(string): the street or road of the location.
  - `village`(string): the village of the location.
  - `subDistrict`(string): the subDistrict of the location.
  - `district`(string): the district of the location.
  - `state`(string): the state of the location.
  - `pincode`(string): the pincode of the location.
- `requestId` (string): Used to identify requests to this API. The same ID is responded back through a response header called `UID`. If this is absent - a self generated ID is present in same response header.

## Response Parameters

1. `inputAddress` (string): The input address for verification
2. `geocodingResponse` (object): The geocoded response for the input address. Contains the following sub attributes: 
   - `houseNumber`(string): the houseNumber of the address/location.
   - `houseName`(string): houseName of the address/location.
   - `poi`(string): the point of interest or famous landmark nearby the location.
   - `street`(string): the street or road of the location.
   - `subsubLocality`(string): the subSubLocality of the location.
   - `subLocality`(string): the subLocality of the location.
   - `locality`(string): the locality of the location.
   - `village`(string): the village of the location.
   - `subDistrict`(string): the subDistrict of the location.
   -  `district`(string): the district of the location.
   - `city`(string): the city of the location.
   - `state`(string): the state of the location.
   - `pincode`(string): the pincode of the location.
   - `floorNumber` (string): floor number of the address if available.
   - `formattedAddress`(string): the general protocol following address.
   - `eloc`(string): eloc of the particular location.
   - `latitude` (double): latitude of the location.
   - `longitude` (double): longitude of the location.
   - `geocodeLevel`(string): the exact matched address component.
   - `confidenceScore`(float): the confidence for current of geocodelevel.
3. `reverseGeocodingResponse` (object): The reverse geocoded response for the provide coordinates. Contains the following sub-attributes:
    - `houseNumber`: The house number (if exists) of the location sent in the request. 
   - `houseName`: The house name (if exists) of the location sent in the request.
   - `poi`: The POI name of the location (if exists) for the given location.
   - `poi_dist`: The distance between of the given location and the POI.
   - `street`: The available street name for the given location or the nearest street name from the given location.
   - `street_dist`:  The distance from street to the point given in the request.
   - `subSubLocality`: The sub-sub locality name (if exists) for the given location.
   - `subLocality`: The sub locality name (if exists) for the given location.
   - `locality`: The locality name (if exists) for the given location.
   - `village`: The village name if the given location in request is nearby village. If village name is coming in the response, city name and locality names will not be present in the response. The locations are defined on the basis of urban and rural regions.
   - `district`: The district name of the given location.
   - `subDistrict`: The sub district name of the given location.
   - `city`: The city name of the given location. There will be no village name in case of the availibilty of city name.  The locations are defined on the basis of urban and rural regions.
   - `state`: The state name of the given location.
   - `pincode`:  The pincode of the given location. 
   - `lat`: The latitude value of the given location in the request. 
   - `lng`: The longitude value of the given location in the request.
   - `area`: The country name of the given location.
   - `eLoc`: The Mappls pin for the returned address.
   - `isRooftop` (boolean): Internally used attribute - currently not being calculated; hence default: `false`. 
   - `formatted_address`: The compelete formatted address for the passed location in the request.
4. `comparison` (object): The object containing the actual comparison for verification purposes:
   - `radialProximity` (object): Contains the radial proximity check results. Each contains: 
     -  `distanceMeters` (double): The radial distance between the address and the coordinates input.
     -  `isWithinThreshold` (boolean): Whether the address and coordinates input are within acceptable threshold as defined in the input.
     -  `thresholdMeters`(integer): The threshold distance set in the input.
     -  `message` (string): The result of the radial comparison in a human readable string.
   -  `addressHierarchy` (object): The address hierarchy comparison object. Each containing: 
      -  `matchLevel` (string): Semi-colon separated administrative hierarchy which was matched in both address and coordinates input. <br> Example: `locality;district;city;state;pincode`
      -  `details` (array of objects): The details array - with each object of this array describing one of the administrative level matches as summarized in the `matchLevel` response above. Each object contains: 
         -  `field` (string): the admin level which this object describes.
         -  `input` (string): The input address's geocoded admin level which was matched.
         -  `reverse` (string): The input coordinate's reverse geocoded admin level which was matched.
         -  `match` (boolean): The match status; i.e. `true`
      -  `message` (string): The result of the administrative level comparison in a human readable string.
5. `additionalProperties` (object): The final summary of location verification with additional attributes for investigative purposes. Each contains: 
   - `verificationTimestamp` (string): Time of rhe verification in ISO 8601 format. <br> Example `2024-09-04T04:40:34Z`
   - `apiVersion` (string): The current version of API on which the location verification happened.
   - `sourceSystem` (string): The map version on which the location verification happened.
   - `remarks` (string): The result of the complete location verification process in a human readable string.

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

``` curl
curl --location 'http://search.mappls.com/search/address/address-verification?access_token=hklmgbwzrxncdyavtsuojqpiefrbhqplnm' \
--header 'Content-Type: application/json' \
--data '{
    "inputAddress": "C/O Dr. Savita Sagar, Hannah Sen Cottage, Lady Irwin College, Safdar Hashmi Marg, Mandi House, New Delhi 110001, Delhi, India",
    "latitude": 28.627221171362137,
    "longitude": 77.23554310432878,
    "thresholdMeters": 200,
    "ruralThresholdMeters": 1000,
    "confidenceThreshold": 0.8,
    "geocodeLevelThreshold": "locality",
    "ruralGeocodeLevelThreshold": "subdistrict",
    "includeDetails": true,
    "requestId": "mmi18072025_1"
}'
```

## Sample Response

```json
{
    "inputAddress": "C/O Dr. Vivek Singh, Hannah Sen Cottage, Lady Irwin College, Safdar Hashmi Marg, Mandi House, New Delhi 110001, Delhi, India",
    "geocodingResponse": {
        "houseNumber": "",
        "houseName": "",
        "poi": "Hannah Sen Cottage",
        "street": "",
        "subSubLocality": "",
        "subLocality": "",
        "locality": "Lady Irwin College Campus",
        "village": "",
        "subDistrict": "Connaught Place",
        "district": "New Delhi District",
        "city": "New Delhi",
        "state": "Delhi",
        "pincode": "110001",
        "floorNumber": "",
        "formattedAddress": "Hannah Sen Cottage, Lady Irwin College Campus, Connaught Place, New Delhi District, New Delhi, Delhi, 110001",
        "eLoc": "17ZUL7",
        "latitude": 28.62719,
        "longitude": 77.235419,
        "geocodeLevel": "poi",
        "elocAdminType": "poi",
        "confidenceScore": 0.8
    },
    "reverseGeocodingResponse": {
        "houseNumber": "",
        "houseName": "",
        "poi": "Lady Irwin College",
        "poi_dist": "137",
        "street": "Sikandra Lane",
        "street_dist": "40",
        "subSubLocality": "",
        "subLocality": "",
        "locality": "Lady Irwin College Campus",
        "village": "",
        "district": "New Delhi District",
        "subDistrict": "Connaught Place",
        "city": "New Delhi",
        "state": "Delhi",
        "pincode": "110001",
        "lat": "28.627221171362137",
        "lng": "77.23554310432878",
        "area": "India",
        "areaCode": "IN",
        "eLoc": "38FD1E",
        "isRooftop": false,
        "formatted_address": "Sikandra Lane, Lady Irwin College Campus, New Delhi, Delhi. 137 m from Lady Irwin College, Pin-110001 (India)"
    },
    "comparison": {
        "radialProximity": {
            "distanceMeters": 12.598903162702024,
            "isWithinThreshold": true,
            "thresholdMeters": 200,
            "message": "The input address and the reverse geocoded address are within the threshold distance."
        },
        "addressHierarchy": {
            "matchLevel": "locality;district;subDistrict;city;state;pincode",
            "details": [
                {
                    "field": "locality",
                    "input": "Lady Irwin College Campus",
                    "reverse": "Lady Irwin College Campus",
                    "match": true
                },
                {
                    "field": "district",
                    "input": "New Delhi District",
                    "reverse": "New Delhi District",
                    "match": true
                },
                {
                    "field": "subDistrict",
                    "input": "Connaught Place",
                    "reverse": "Connaught Place",
                    "match": true
                },
                {
                    "field": "city",
                    "input": "New Delhi",
                    "reverse": "New Delhi",
                    "match": true
                },
                {
                    "field": "state",
                    "input": "Delhi",
                    "reverse": "Delhi",
                    "match": true
                },
                {
                    "field": "pincode",
                    "input": "110001",
                    "reverse": "110001",
                    "match": true
                }
            ],
            "message": "The address hierarchy matches up to the locality, district, subDistrict, city, state and pincode levels."
        }
    },
    "additionalProperties": {
        "verificationTimestamp": "2025-07-03T06:59:05Z",
        "apiVersion": "1.0.0",
        "sourceSystem": "Mappls 2024.11",
        "remarks": "The input address is verified successfully within the specified thresholds."
    }
}
```

## Appendix A
### Possible "message" Values in "radialProximity" Object

1. When the distance is within the threshold: 
<br>Condition: isWithinThreshold is true.<br>
"The input address and the reverse geocoded address are within the threshold distance."

2. When the distance exceeds the threshold:
<br>Condition: isWithinThreshold is false.<br>
"The input address and the reverse geocoded address exceed the threshold distance."

3. When the threshold distance is not defined:
<br>Condition: thresholdMeters is not provided or is null.<br>
"Threshold distance is not defined. Cannot determine proximity."

4. When the geocoded coordinates are not available:
<br>Condition: latitude and longitude in geocodingResponse are null or not provided.<br>
"Geocoded coordinates are not available for the input address."

5. When the reverse geocoded coordinates are not available:
<br>Condition: latitude and longitude in reverseGeocodingResponse are null or not provided.<br>
"Reverse geocoded coordinates are not available."

6. When both geocoded and reverse geocoded coordinates are missing:
<br>Condition: latitude and longitude in both geocodingResponse and reverseGeocodingResponse are null or not provided.<br>
"Both geocoded and reverse geocoded coordinates are missing. Proximity cannot be determined."

7. When the input address is exactly the same as the reverse geocoded address:
<br>Condition: distanceMeters is 0.<br>
"The input address and the reverse geocoded address are exactly the same."

These messages help provide clear and specific feedback on the outcome of the radial proximity assessment, ensuring that the users understand the results of the address verification process.

## Appendix B

### Assessment Summary (Remarks)

The "remarks" field at the end of the API response can provide various pieces of feedback or additional information regarding the address verification process. Here are some possible values for "remarks":

1. Successful Verification:
"The input address is verified successfully within the specified thresholds."
   - When both radial proximity and address hierarchy comparisons are successful.
2. Partial Match:
"The input address partially matches the reverse geocoded address."
   - When the address hierarchy matches only up to a certain level, but not completely.
3. Proximity Match Only:
"The input address and the reverse geocoded address are within the threshold distance, but some address components do not match."
   - When the radial proximity is within the threshold but there are discrepancies in the address hierarchy.
4. Hierarchy Match Only:
"The address hierarchy matches up to the specified level, but the radial proximity exceeds the threshold distance."
   - When the address components match up to a certain level but the distance between the locations is beyond the threshold.
5. Verification Failed:
"The input address could not be verified."
   - When both the radial proximity and address hierarchy comparisons fail.
6. Coordinates Missing:
"Geocoded or reverse geocoded coordinates are missing. Verification could not be completed."
   - When the required coordinates for comparison are not available.
7. Exact Match:
"The input address and the reverse geocoded address are exactly the same."
   - When there is an exact match between the input address and the reverse geocoded address.
8. Multiple Results:
"Multiple geocoded addresses found. Verification may not be accurate."
   - When the geocoding API returns multiple potential addresses.
9. Low Score:
"The geocoding level & confidence score for the geocoded address is low. Verification may not be reliable."
   - When the confidence score provided by the geocoding API is below a certain threshold, indicating potential inaccuracies.

These remarks help provide clear and specific feedback on the outcome of the address verification process, ensuring that users understand the results and any issues that may have occurred during the verification.


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
[<img src="https://about.mappls.com/about/images/MAPPLS-MapmyIndia-logo.png" height="40"/> </p>](https://about.mappls.com/api/)
# Mappls GeoVerify v2 API

**Easy To Integrate Maps & Location APIs & SDKs For Web & Mobile Applications**

Powered with India's most comprehensive and robust mapping functionalities.

You can get your API key to be used in this document here: [https://about.mappls.com/api/](https://about.mappls.com/api/)

---

## Introduction

Introducing the **Mappls GeoVerify v2 API**, a robust solution designed to enhance the accuracy and reliability of location-based data through advanced geospatial checks. Developed by Mappls MapmyIndia, this API is an essential tool for any business or application requiring precise location verification, ensuring that addresses and coordinates are not only geographically accurate but also contextually consistent.

In the context of address verification, especially within processes like KYC (Know Your Customer), our API excels by integrating multiple critical steps. For example, during the KYC process, customers provide a structured or unstructured address, which is converted into geographical coordinates through geocoding. Conversely, coordinates captured during field or digital KYC activities are converted back into a recognizable address through reverse geocoding. 

The **Mappls GeoVerify v2 API** performs an in-depth comparison between these data points. It checks the radial proximity between the two sets of coordinates, ensuring they are within an acceptable distance from each other. This step verifies that the address provided by the customer and the physical location captured during verification are aligned geographically.

Furthermore, the API can validate the consistency of the administrative hierarchy between the geocoded address and the reverse-geocoded address. This validation is performed across configurable administrative levels, with each hierarchy level supporting independently defined tolerance thresholds (radial values) as specified by the consuming application.

The validation process compares administrative components such as country, state, district, city, locality, and pincode between the two address representations to determine whether they belong to the same administrative context. By cross-verifying these hierarchy tokens in addition to the spatial proximity check, the API provides a stronger confidence measure that the supplied address and coordinates correspond to the same geopolitical and administrative region.

This dual-layered approach—combining radial proximity checks with administrative level matching—provides a comprehensive solution for location verification. It guarantees that the specified location is accurate and trustworthy, making it particularly valuable in processes where location integrity is crucial, such as KYC in the BFSI sector, logistics, real estate, or any service dependent on precise location data.

The API is designed for ease of integration, offering a straightforward API call structure and extensive documentation to support seamless implementation into existing systems. Backed by Mappls MapmyIndia’s extensive geospatial data, this API delivers reliable and accurate results every time.

---

## Live Demo

> Under Construction

---

## Getting Access

Before using the API in your solution, please ensure that the related access is enabled in the [Mappls Console](https://auth.mappls.com/console/), within your app—be it for Mobile, Web, or Cloud integration.

1. Copy and paste the key from your `credentials` section from your API [keys](https://auth.mappls.com/console/) into the `access_token` query parameter.
2. Your static key can be secured by whitelisting its usage for particular IPs (for cloud app usage) OR a set of domains (for a web app).
3. Pass the static key obtained from your Console as a mandatory query parameter: `access_token`.

---

## Authentication Object
- **Parameter Name**: `access_token` (mandatory query parameter)
- **Example**: `access_token=hklmgbwzrxncdyavtsuojqpiefrbhqplnm`

---

## HTTP Method
`POST`

---

## Endpoint URL
```html
https://search.mappls.com/search/address/geoverify
```

---

## Request Headers
- `Content-Type: application/json`

---

## Request Body Parameters

### Root Parameters

| Parameter | Type | Mandatory? | Range / Limit | Description |
|---|---|---|---|---|
| `inputAddress` | string | **Yes** | No enforced limit | The free-form address provided by the customer. Supports Unicode (Indian scripts, diacritics, etc.). |
| `latitude` | double | **Yes** | `-90.0` to `+90.0` | Latitude of the field-captured location in decimal degrees. Up to 15 significant decimal digits (IEEE 754). For India, the expected range is `8.0` to `37.6`. |
| `longitude` | double | **Yes** | `-180.0` to `+180.0` | Longitude of the field-captured location in decimal degrees. Up to 15 significant decimal digits (IEEE 754). For India, the expected range is `68.0` to `97.4`. |
| `requestId` | string | No | Recommended `≤ 32` chars | Client-generated reference identifier for traceability. Act as Request ID. Not auto-generated by the API. |
| `geocodeConfig` | object | No | — | Configuration for geocoding settings. |
| `tokenizedAddress` | object | No | — | Key-value mapping of pre-parsed/tokenized address parts. |
| `thresholdMeters` | object | No | — | Radial proximity thresholds for urban/rural checks. |
| `adminThresholdMeters` | object | No | — | Granular tolerance thresholds (in meters) for administrative hierarchy elements. |
| `includeDetails` | boolean | No | `true` or `false` | Set to `true` to include per-level detail breakdown in `comparison.addressHierarchy.details`. Default is `false`. |

---

### Object Parameters Details

#### 1. `geocodeConfig` (Object)
| Attribute | Type | Mandatory? | Description |
|---|---|---|---|
| `geocodeBound` | string | No | Geospatial boundary filter parameter (i.e. eLoc of bounding admin - 6 characters). |

#### 2. `tokenizedAddress` (Object)
Provides pre-tokenized details of the address to enhance accuracy.
| Attribute | Type | Mandatory? | Description |
|---|---|---|---|
| `houseNumber` | string | No | House or flat number. |
| `careOf` | string | No | C/O name or person. |
| `houseName` | string | No | Building or house name. |
| `landmark` | string | No | Landmark name. |
| `street` | string | No | Street/road name. |
| `locality` | string | No | Sub-locality or locality. |
| `village_city` | string | No | Village or City name. |
| `state` | string | No | State name. |
| `subDistrict` | string | No | Sub-district / Tehsil name. |
| `district` | string | No | District name. |
| `postcode` | string | No | Pincode / Postal Code. |
| `country` | string | No | Country name. |

#### 3. `thresholdMeters` (Object)
Specifies the acceptable distance bounds (in meters) for the radial proximity validation.
| Attribute | Type | Default | Range | Description |
|---|---|---|---|---|
| `urban` | integer | `200` | `50` - `50000` | Threshold for urban areas. |
| `rural` | integer | `1000` | `50` - `50000` | Threshold for rural areas. |

#### 4. `adminThresholdMeters` (Object)
Allows custom distance thresholds (in meters) for matching different administrative hierarchy levels.
| Attribute | Type | Description | Range |
|---|---|---|---|
| `subSubLocality` | integer | Max allowed distance for sub-sub locality matches. | `50` - `50000` |
| `subLocality` | integer | Max allowed distance for sub-locality matches. | `50` - `50000` |
| `locality` | integer | Max allowed distance for locality matches. | `50` - `50000` |
| `pincode` | integer | Max allowed distance for pincode matches. | `50` - `50000` |
| `street` | integer | Max allowed distance for street matches. | `50` - `50000` |
| `village` | integer | Max allowed distance for village matches. | `50` - `50000` |
| `city` | integer | Max allowed distance for city matches. | `50` - `50000` |
| `subDistrict` | integer | Max allowed distance for sub-district matches. | `50` - `50000` |
| `district` | integer | Max allowed distance for district matches. | `50` - `50000` |
| `state` | integer | Max allowed distance for state matches. | `50` - `50000` |

---

## Response Parameters

| Parameter | Type | Description |
|---|---|---|
| `inputAddress` | array (string) | Array containing the input address string(s). |
| `geocodingResponse` | object | Details from geocoding the input address. |
| `reverseGeocodingResponse` | object | Details from reverse-geocoding the input coordinates. |
| `comparison` | object | Metric and logical comparison results of geocoding vs reverse geocoding. |
| `additionalProperties` | object | Summary metadata and operational properties of the transaction. |

### 1. `geocodingResponse` (Object)
| Parameter | Type | Description |
|---|---|---|
| `houseNumber` | string | Extracted house number. |
| `houseName` | string | Extracted house/building name. |
| `poi` | string | Extracted Point of Interest / Landmark. |
| `street` | string | Extracted street/road. |
| `subSubLocality` | string | Extracted sub-sub locality. |
| `subLocality` | string | Extracted sub locality. |
| `locality` | string | Extracted locality. |
| `village` | string | Extracted village. |
| `subDistrict` | string | Extracted sub-district. |
| `district` | string | Extracted district. |
| `city` | string | Extracted city. |
| `state` | string | Extracted state. |
| `pincode` | string | Extracted pincode. |
| `floorNumber` | string | Extracted floor number if available. |
| `formattedAddress` | string | Full formatted address derived from geocoding. |
| `eLoc` | string | Alphanumeric Mappls eLoc identifier (Fixed: 6 characters). |
| `latitude` | double | Geocoded latitude (up to 15 decimal digits). |
| `longitude` | double | Geocoded longitude (up to 15 decimal digits). |
| `geocodeLevel` | string (enum) | Level at which the address was matched. |
| `elocAdminType` | string | Administrative type associated with the matched eLoc. |
| `confidenceScore` | float | Geocoding confidence score ranging from `0.0` to `1.0`. |

### 2. `reverseGeocodingResponse` (Object)
| Parameter | Type | Description |
|---|---|---|
| `houseNumber` | string | House number at the input coordinates. |
| `houseName` | string | House name at the input coordinates. |
| `poi` | string | POI / Landmark near the input coordinates. |
| `poi_dist` | string (numeric) | Distance in meters to the nearest POI. |
| `street` | string | Street/road at or nearest to the coordinates. |
| `street_dist` | string (numeric) | Distance in meters to the nearest street. |
| `subSubLocality` | string | Sub-sub locality. |
| `subLocality` | string | Sub locality. |
| `locality` | string | Locality name. |
| `village` | string | Village name (returns village name instead of city/locality for rural locations). |
| `district` | string | District name. |
| `subDistrict` | string | Sub district name. |
| `city` | string | City name (mutually exclusive with village name). |
| `state` | string | State name. |
| `pincode` | string | Pincode. |
| `lat` | string (numeric) | Latitude value returned as string. |
| `lng` | string (numeric) | Longitude value returned as string. |
| `area` | string | Country name (e.g. "India"). |
| `areaCode` | string | ISO country code (e.g. "IN"). |
| `eLoc` | string | Alphanumeric Mappls eLoc identifier (Fixed: 6 characters). |
| `isRooftop` | boolean | Indicates if footprint data is also queried. Currently defaults to `false`. |
| `isVenue` | boolean | Indicates if the location is a specific venue. |
| `formatted_address` | string | Fully formatted address from reverse geocoding. |

### 3. `comparison` (Object)
| Parameter | Type | Description |
|---|---|---|
| `radialProximity` | object | Results of the distance calculation. Contains: <br>- `distanceMeters` (double): Computed distance (Haversine) between geocoded address and input coordinates.<br>- `isWithinThreshold` (boolean): `true` if within defined threshold, else `false`.<br>- `thresholdMeters` (integer): Proximity threshold applied. |
| `addressHierarchy` | object | Results of administrative hierarchy checks. Contains: <br>- `absoluteMatchLevel` (string): Matched administrative components (comma-separated).<br>- `bestSpatialAdminMatch` (string): The most granular administrative level matching spatially.<br>- `adminDistance` (double): Distance calculated for admin boundaries.<br>- `adminThresholdMeters` (integer): Applied admin distance threshold.<br>- `isWithinAdminThreshold` (boolean): `true` if within admin threshold boundaries, else `false`. <br>- `details` (array of objects): Detailed match status per admin level (populated if `includeDetails: true`). Each object contains: `field` (string), `input` (string), `reverse` (string), and `distanceMatch` (boolean). |

### 4. `additionalProperties` (Object)
| Parameter | Type | Description |
|---|---|---|
| `verificationTimestamp` | string | Date/time in ISO 8601 format: `YYYY-MM-DDTHH:MM:SSZ`. |
| `apiVersion` | string | API version utilized (e.g. `"2.0"`). |
| `sourceSystem` | string | Reference system version (e.g. `"Mappls 2026_04"`). |
| `decision` | string | Verification decision (e.g., `"Match"`, `"No Match"`). |
| `remarks` | string | Summary human-readable validation feedback (see Appendix B). |
| `requestId` | string | Echoes the `requestId` passed in the request body. |

---

## Response Status Codes

### Success Codes
| HTTP Code | Scenario | Response Body |
|---|---|---|
| `200 OK` | Request processed successfully; verification result returned. | Full JSON response payload. |
| `204 No Content` | Request valid but no geocoding results found. | Empty response body (Client should handle gracefully). |

### Client-Side Error Codes
| HTTP Code | Scenario | `error` | `error_description` | `response_code` |
|---|---|---|---|---|
| `400 Bad Request` | Missing/malformed parameters (`inputAddress`, `latitude`, `longitude`) | `"Bad Request"` | `"Please Check mandatory parameter"` | — |
| `400 Bad Request` | Invalid/out-of-bound coordinate range values | `"Bad Request"` | `"Invalid Coordinates"` | — |
| `400 Bad Request` | Invalid characters in coordinate numbers | `"Bad Request"` | `"Invalid values in request body"` | — |
| `400 Bad Request` | Unrecognised or malformed token in query parameter | `"Invalid Token"` | `"Token was not recognised : <token>"` | `400` (integer) |
| `401 Unauthorized` | Key authentication missing from security context | `"unauthorized"` | `"An Authentication object was not found in the SecurityContext"` | `"401"` (string) |
| `401 Unauthorized` | Token provided but not valid / active | `"Invalid Token"` | `"Token was not recognised : <token>"` | `401` (integer) |
| `403 Forbidden` | API quota or credits associated with key exhausted | — | Quota/Credits exhausted. Monitor usage in Console. | — |

### Server-Side Error Codes
| HTTP Code | Meaning | Response Details |
|---|---|---|
| `500 Internal Server Error` | Unexpected server-side failure. | Body layout not fixed. Clients should not rely on a specific layout. |
| `503 Service Unavailable` | Server downtime or maintenance window. | Implement standard retry policies with exponential backoff. |

---

## Best Practices & Accuracy Optimization

1. **Input Address Quality**: The single most critical driver. Always include a **pincode** to narrow the search area, and provide **house/building numbers** and **street names** to achieve high-precision matches (`houseNumber` or `poi` levels).
2. **GPS Accuracy**: Keep in mind device GPS accuracy variations. Standard urban GPS error is 3–10m but can inflate to 30–100m in high-rise corridors. 
3. **Threshold Values**: 
   - **Urban Areas**: Recommended bounds `200m` to `300m`.
   - **Rural Areas**: Recommended bounds `1000m` to `2000m` due to sparser location mapping density.

---

## Sample Request (cURL)

```bash
curl --location 'https://search.mappls.com/search/address/geoverify?access_token=hklmgbwzrxncdyavtsuojqpiefrbhqplnm' \
--header 'Content-Type: application/json' \
--data '{
    "latitude": 28.5312995,
    "longitude": 77.244225,
    "requestId": "TC002",
    "geocodeConfig": {
        "geocodeBound": "tavi5s"
    },
    "inputAddress": "C/O Vivek Singh, 388, Block S, Greater Kailash 2, New Delhi, Delhi 110048",
    "tokenizedAddress": {
        "houseNumber": "",
        "careOf": "",
        "houseName": "",
        "landmark": "",
        "street": "",
        "locality": "",
        "village_city": "",
        "state": "",
        "subDistrict": "",
        "district": "",
        "postcode": "",
        "country": ""
    },
    "thresholdMeters": {
        "urban": 300,
        "rural": 1000
    },
    "adminThresholdMeters": {
        "subSubLocality": 400,
        "subLocality": 700,
        "locality": 1000,
        "pincode": 3000,
        "street": 1000,
        "village": 2000,
        "city": 10000,
        "subDistrict": 5000,
        "district": 10000,
        "state": 50000
    },
    "includeDetails": true
}'
```

## Sample Response (JSON)

```json
{
    "inputAddress": [
        "C/O Vivek Singh, 388, Block S, Greater Kailash 2, New Delhi, Delhi 110048, India"
    ],
    "geocodingResponse": {
        "houseNumber": "388",
        "houseName": "",
        "poi": "",
        "street": "",
        "subSubLocality": "",
        "subLocality": "Block S",
        "locality": "Greater Kailash 2",
        "village": "",
        "subDistrict": "Kalkaji",
        "district": "South East District",
        "city": "New Delhi",
        "state": "Delhi",
        "pincode": "110048",
        "floorNumber": "",
        "formattedAddress": "388, Block S, Greater Kailash 2, Kalkaji, South East District, New Delhi, Delhi, 110048",
        "eLoc": "K8X355",
        "latitude": 28.531036,
        "longitude": 77.244427,
        "geocodeLevel": "houseNumber",
        "elocAdminType": "houseNumber",
        "confidenceScore": 1.0
    },
    "reverseGeocodingResponse": {
        "houseNumber": "382",
        "houseName": "",
        "poi": "The Foundation Years",
        "poi_dist": "27",
        "street": "Gurudwara Road",
        "street_dist": "122",
        "subSubLocality": "",
        "subLocality": "Block S",
        "locality": "Greater Kailash 2",
        "village": "",
        "district": "South East District",
        "subDistrict": "Kalkaji",
        "city": "New Delhi",
        "state": "Delhi",
        "pincode": "110048",
        "lat": "28.5312995",
        "lng": "77.244225",
        "area": "India",
        "areaCode": "IN",
        "eLoc": "F88NDK",
        "isRooftop": false,
        "isVenue": false,
        "formatted_address": "382, Gurudwara Road, Block S, Greater Kailash 2, New Delhi, Delhi. 27 m from The Foundation Years, Pin-110048 (India)"
    },
    "comparison": {
        "radialProximity": {
            "distanceMeters": 35.33,
            "isWithinThreshold": true,
            "thresholdMeters": 300
        },
        "addressHierarchy": {
            "addressHierarchy": {
                "absoluteMatchLevel": "subLocality,locality,pincode,city,state",
                "bestSpatialAdminMatch": "subLocality",
                "adminDistance": 35.33,
                "adminThresholdMeters": 700,
                "isWithinAdminThreshold": true,
                "details": [
                    {
                        "field": "subLocality",
                        "input": "Block S",
                        "reverse": "Block S",
                        "distanceMatch": true
                    },
                    {
                        "field": "locality",
                        "input": "Greater Kailash 2",
                        "reverse": "Greater Kailash 2",
                        "distanceMatch": true
                    },
                    {
                        "field": "pincode",
                        "input": "110048",
                        "reverse": "110048",
                        "distanceMatch": true
                    },
                    {
                        "field": "city",
                        "input": "New Delhi",
                        "reverse": "New Delhi",
                        "distanceMatch": true
                    },
                    {
                        "field": "state",
                        "input": "Delhi",
                        "reverse": "Delhi",
                        "distanceMatch": true
                    }
                ]
            }
        }
    },
    "additionalProperties": {
        "verificationTimestamp": "2026-06-03T11:27:06Z",
        "apiVersion": "2.0",
        "sourceSystem": "Mappls 2026_04",
        "decision": "Match",
        "remarks": "The input address and the reverse geocoded address are within the threshold distance.",
        "requestId": "TC002"
    }
}
```

---

## Appendix A
### Possible "message" Values in "radialProximity" Object
1. **Within Threshold**: *"The input address and the reverse geocoded address are within the threshold distance."* (`isWithinThreshold` is true)
2. **Exceeds Threshold**: *"The input address and the reverse geocoded address exceed the threshold distance."* (`isWithinThreshold` is false)
3. **Threshold Undefined**: *"Threshold distance is not defined. Cannot determine proximity."*
4. **Geocoding Coordinates Missing**: *"Geocoded coordinates are not available for the input address."*
5. **Reverse Geocoding Coordinates Missing**: *"Reverse geocoded coordinates are not available."*
6. **All Coordinates Missing**: *"Both geocoded and reverse geocoded coordinates are missing. Proximity cannot be determined."*
7. **Exact Match**: *"The input address and the reverse geocoded address are exactly the same."* (`distanceMeters` is 0)

---

## Appendix B
### Assessment Summary (Remarks)
1. **Successful Verification**: *"The input address is verified successfully within the specified thresholds."*
2. **Partial Match**: *"The input address partially matches the reverse geocoded address."*
3. **Proximity Match Only**: *"The input address and the reverse geocoded address are within the threshold distance, but some address components do not match."*
4. **Hierarchy Match Only**: *"The address hierarchy matches up to the specified level, but the radial proximity exceeds the threshold distance."*
5. **Verification Failed**: *"The input address could not be verified."*
6. **Coordinates Missing**: *"Geocoded or reverse geocoded coordinates are missing. Verification could not be completed."*
7. **Exact Match**: *"The input address and the reverse geocoded address are exactly the same."*
8. **Multiple Results**: *"Multiple geocoded addresses found. Verification may not be accurate."*
9. **Low Score**: *"The geocoding level & confidence score for the geocoded address is low. Verification may not be reliable."*

---

For any queries and support, please contact: 

[<img src="https://about.mappls.com/images/mappls-logo.svg" height="40"/> </p>](https://about.mappls.com/api/)
Email us at [apisupport@mappls.com](mailto:apisupport@mappls.com)

![](https://www.mapmyindia.com/api/img/icons/support.png)
[Support](https://about.mappls.com/contact/)
Need support? contact us!

<br></br>
<br></br>

[<p align="center"> <img src="https://cdn.jsdelivr.net/gh/glincker/thesvg@main/public/icons/stack-overflow/default.svg" height="40"/> ](https://stackoverflow.com/questions/tagged/mappls-api)[![](https://www.mapmyindia.com/api/img/icons/blog.png)](https://about.mappls.com/blog/)[<img src="https://cdn.jsdelivr.net/gh/glincker/thesvg@main/public/icons/github/dark.svg" height="40"/> ](https://github.com/mappls-api)[<img src="https://mmi-api-team.s3.ap-south-1.amazonaws.com/API-Team/npm-logo.one-third%5B1%5D.png" height="40"/> </p>](https://www.npmjs.com/org/mapmyindia) 

[<p align="center"> <img src="https://www.mapmyindia.com/june-newsletter/icon4.png"/> ](https://www.facebook.com/Mapplsofficial)[![](https://www.mapmyindia.com/june-newsletter/icon2.png)](https://twitter.com/mappls)[![](https://www.mapmyindia.com/newsletter/2017/aug/llinkedin.png)](https://www.linkedin.com/company/mappls/)[![](https://www.mapmyindia.com/june-newsletter/icon3.png)](https://www.youtube.com/channel/UCAWvWsh-dZLLeUU7_J9HiOA)

<div align="center">@ Copyright 2026 CE Info Systems Ltd. All Rights Reserved.</div>

<div align="center"> <a href="https://about.mappls.com/api/terms-&-conditions">Terms & Conditions</a> | <a href="https://about.mappls.com/about/privacy-policy">Privacy Policy</a> | <a href="https://about.mappls.com/pdf/mapmyIndia-sustainability-policy-healt-labour-rules-supplir-sustainability.pdf">Supplier Sustainability Policy</a> | <a href="https://about.mappls.com/pdf/Health-Safety-Management.pdf">Health & Safety Policy</a> | <a href="https://about.mappls.com/pdf/Environment-Sustainability-Policy-CSR-Report.pdf">Environmental Policy & CSR Report</a>

<div align="center">Customer Care: +91-9999333223</div>

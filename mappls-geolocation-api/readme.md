[<img src="https://about.mappls.com/about/images/MAPPLS-MapmyIndia-logo.png" height="40"/> </p>](https://about.mappls.com/api/)

# Geolocation API

## [Introduction](#Introduction)

The Geolocation API returns a location on the basis of cell tower information that any mobile client can detect.<br>
Any mobile user will send the information of all the connected or recently connected cell towers information in the API, Now API will articulate approximate user location on the basis of the provided cell towers information. MMI will use its cell towers geo-location database to calculate the approximate geo-location of the user. 

## Getting Access

Before using the API in the your solution, please ensure that the related access is enabled in the [Mappls Console](https://apis.mappls.com/console/), in the same project you set up for the Maps SDK.

1. Copy and paste the generated `access token` from your API [keys](https://apis.mappls.com/console/) available in the dashboard in the sample code for interactive map development.
    - This APIs follow OAuth2 based security.
    - `Access Token` can be generated using Token Generation API.
    - To know more on how to create your access tokens, please use our authorization API URL. More details available [here](https://developer.mappls.com/mapping/tokenGeneration)
    - The `access token` is a valid by default for 24 hours from the time of generation. This can be configured by you in the API console.
2. **`Security Type`**
    
    This APIs follow OAuth2 based security. **To know more on how to create your authorization tokens, please use our authorization token URL. More details available**  [here](https://developer.mappls.com/mapping/tokenGeneration)

## [Input URL](#Input_URL) 

https://atlas.mappls.com/api/places/geo-location

## [Method](#Method)

POST

## [Request Type](Request_Type)

`Content-Type: application/json`

## [Response Type](#Response_Type)

`Content-Type: application/json`

## [Request Parameters](#Request_Parameter)

Part of Body

### [a. Mandatory Parameters](#a_Mandatory_Parameters)

#### For 2G Connections

1.	**`cellTowers`** (array of objects) : 	An array of cell tower objects. The following are the parameters are required in Cell Tower Objects:
    - **`cellId`** (number) : Unique identifier of the cell. Required for radioType gsm (default), cdma, wcdma and lte.
    - **`locationAreaCode`** (number) : The Location Area Code (LAC) for GSM and WCDMA networks.
    - **`mobileCountryCode`** (number) : The cell tower's Mobile Country Code (MCC).<br>Valid range: 0–999.
    - **`mobileNetworkCode`** (number) : The cell tower's Mobile Network Code. This is the MNC for GSM, WCDMA, LTE and NR.<br> Valid range for MNC: 0-999 and for SID: 0-32767

#### For 4G & 5G Connections

There is an additional request property that you have to send: 

1. **`radioType`** (string): a string indicating whether the radio type for the connection is 4G or 5G. Can take in the following values: 
   - `lte` - indicating that the radio of 4G connection type.
   - `NR` - indicating that the radio of 5G connection type.

>> Only in case of when `radioType` is `NR`, `cellId` variable changes to `newRadioCellId`. 

Note: 
1. **A minimum of one cell tower object is required and a maximum of six cell tower objects are allowed as input.**
2. **To get the best result, a minimum of three cell tower objects should be input >  in accordance with one active and two latest historical cell info objects**

## [Response Parameters](#Response-Parameters)

1.	`location`(object): The estimated geolocation i.e. latitude and longitude, in degrees. Contains the following parameters:
    - `lon` (number): longitude of the estimated location.
    - `lat` (number): latitude of the estimated location.

 
## [Sample cURL Request](#Sample-cURL_Request)

### 2G Connections

```
curl --location --request POST 'https://atlas.mapmyindia.com/api/places/geo-location' \
--header 'Authorization: Bearer 0XXXXXXf-dXX0-4XX0-8XXa-eXXXXXXXXXX6' \
--header 'Content-Type: application/json' \
--data-raw '{
    "cellTowers": [
        {
            "cellId": 900372,
            "locationAreaCode": 57,
            "mobileCountryCode": 405,
            "mobileNetworkCode": 872
        }
    ]
}'
```

### 4G Connections

```curl
curl --location --request POST 'https://atlas.mapmyindia.com/api/places/geo-location' \
--header 'Authorization: Bearer 0XXXXXXf-dXX0-4XX0-8XXa-eXXXXXXXXXX6' \
--header 'Content-Type: application/json' \
--data-raw '{
    "radioType": "lte",
    "cellTowers": [
        {
            "cellId": 900372,
            "locationAreaCode": 57,
            "mobileCountryCode": 405,
            "mobileNetworkCode": 872
        }
    ]
}'
```

### 5G Connections

```curl
curl --location --request POST 'https://atlas.mapmyindia.com/api/places/geo-location' \
--header 'Authorization: Bearer 0XXXXXXf-dXX0-4XX0-8XXa-eXXXXXXXXXX6' \
--header 'Content-Type: application/json' \
--data-raw '{
    "radioType": "NR",
    "cellTowers": [
        {
            "newRadioCellId": 900372,
            "locationAreaCode": 57,
            "mobileCountryCode": 405,
            "mobileNetworkCode": 872
        }
    ]
}'
```


## [Sample Response](#Sample_Response)
```
{
    "location": {
        "lon": 77.268947,
        "lat": 28.550847
    }
}
```


## [Response Codes {as HTTP response codes}](#a1_Response_Codes_{as_HTTP_response_codes})

#### [Success](#Success)

1. 200: To denote a successful API call. 
2. 204: To denote the API was a success but no results were found. 

#### [Client-Side Issues](Client-Side_Issues) 

3. 400: Bad Request, User made an error while creating a valid request. 
4. 401: Unauthorized, Developer’s key is not allowed to send a request.
5. 403: Forbidden, Developer’s key has hit its daily/hourly limit.

#### [Server-Side Issues](#Server-Side_Issues)

6. 500: Internal Server Error, the request caused an error in our systems.
7. 503: Service Unavailable, during our maintenance break or server downtimes.


## [Response Messages (as HTTP response messages)](#a2_Response_Messages_(as_HTTP_response_messages))

1.	200: Success.
2.	201: Created. 
3.	204: No matches were found for the provided query. 
4.	400: Something’s just not right with the request. 
5.	401: Access Denied. 
6.	403: Services for this key has been suspended due to daily/hourly transactions limit. 
7.	500: Something went wrong. 
8.	503: Maintenance Break. 
9.	410 : Deleted
10.	422 : Unprocessable entity
11.	412 : Precondition Failed
12.	428 : Precondition Required.


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
[<img src="https://about.mappls.com/about/images/MAPPLS-MapmyIndia-logo.png" height="40"/> </p>](https://about.mappls.com/api/)

## [Table of Contents](#Table_of_Contents)
- ***[Introduction](#introduction)***
- ***[Input URL](#input-url)***
- ***[Input Method](#input-method)***
- ***[Request Parameters](#request-parameters)***
     - ***[a. Mandatory Parameters](#a-mandatory-parameters)*** 
- ***[Request Headers](#request-headers)***
- ***[1. Security Type](#1-security-type)***
     - ***[1.1 Response Type](#11-response-type)***
     - ***[1.2 Response Codes {as HTTP response codes}](#12-response-codes-as-http-response-codes)***
     - ***[1.3 Response Messages (as HTTP response messages)](#13-response-messages-as-http-response-messages)***
- ***[Response Parameters](#response-parameters)***
- ***[Claim Request Parameters](#claim-request-parameters)***
- ***[Sample Response](#sample-response)***

# [Place Details API](#Place_Details_API)

## [Introduction](#Introduction)

The Place detail API is to extract the details of a place with the help of its eLoc i.e. a 6 character code. Since a place may or may not have additional attributes associated with it, the response from the place details may be different for each record. However the response will be an extract from an existing set of master key-value pairs grouped as objects.

## Getting Access

Before using the API in the your solution, please ensure that the related access is enabled in the [Mappls Console](https://apis.mappls.com/console/), in the same project you set up for the Maps SDK.

1. Copy and paste the generated `access token` from your API [keys](https://apis.mappls.com/console/) available in the dashboard in the Authorization header of this API.
    - This APIs follow OAuth2 based security.
    - `Access Token` can be generated using Token Generation API.
    - To know more on how to create your access tokens, please use our authorization API URL. More details available [here](https://developer.mappls.com/mapping/tokenGeneration)
    - The `access token` is a valid by default for 24 hours from the time of generation. This can be configured by you in the API console.
2. **`Security Type`**
    
    This APIs follow OAuth2 based security. **To know more on how to create your authorization tokens, please use our authorization token URL. More details available**  [here](https://developer.mappls.com/mapping/tokenGeneration)



## [Input URL](#Input_URL) 
https://explore.mappls.com/apis/O2O/entity/{eLoc}

## [Input Method](#Input_Method)

GET

## [Request Parameters](#Request_Parameter)

### [a. Mandatory Parameters](#a_Mandatory_Parameters)

**`eLoc`** :  eLoc of the place whose details are required. The 6-digit alphanumeric code for any location.

## [Request Headers](#Request-Headers)


1. **`Authorization:`** `“{token_type} {access_token}”`


## [1.1 Response Type](#1_1_Response_Type)

- JSON

## [1.2 Response Codes {as HTTP response codes}](#1_2_Response_Codes_{as_HTTP_response_codes})

#### [Success](#Success)

1. 200: To denote a successful API call.  
2. 204: To denote the API was a success but no results we’re found.  

#### [Client-Side Issues](#Client_Side_Issues) 

3. 400: Bad Request, User made an error while creating a valid request. 
4. 401: Unauthorized, Developer’s key is not allowed to send a request.
5. 403: Forbidden, Developer’s key has hit its daily/hourly limit 

#### [Server-Side Issues](#Server-Side_Issues)

6. 500: Internal Server Error, the request caused an error in our systems.
7. 503: Service Unavailable, during our maintenance break or server downtimes.

## [1.3 Response Messages (as HTTP response messages)](#1_3_Response_Messages_(as_HTTP_response_messages))

1. 200: Success. 
2. 204: No matches we’re found for the provided query. 
3. 400: Something’s just not right with the request. 
4. 401: Access Denied. 
5. 403: Services for this key has been suspended due to daily/hourly transactions limit. 
6. 500: Something went wrong. 
7. 503: Maintenance Break.

## [Place Detail with Sub Template based Configuration](#Place_Detail_with_Sub_Template_based_Configuration)

The API is highly configurable to  configuration enables to provide the required set of attributes to the user on the basis of assigned sub templates.
The default configuration with available with basic pay-as-you-go rates is that of `General Details` subtemplate.

## [Response Parameters for Place Details - Sub Templates](#Response_Parameters_for_Place_Details-Sub_Templates)

The parameters are group in sub templates. Here is the list of attributes with sub template information.  

#### [Subtemplate 1 : General Details](#Subtemplate_1_:_sbt_general_details)
1.	eloc (string) : 6 characters alphanumeric unique identifier 
2.	name (string) : Name of the place 
3.	address (string) : address of the place 
4.	type: defines the type of location matched (HOUSE_NUMBER, HOUSE_NAME, POI, 
	STREET, SUB_LOCALITY, LOCALITY, VILLAGE, DISTRICT, SUB_DISTRICT, CITY, STATE, 
     SUBSUBLOCALITY, PINCODE)

#### [Subtemplate 2 : Admin Tokens (PREMIUM OFFERING)](#Subtemplate_2_:_sbt_admin_token)
1.	city (string): The name of the city in which the location exists.
2.	district (string): The name of the district in which the location exists.
3.	pincode (string): The pin code of the location area.
4.	subDistrict (string): The name of the sub-district in which the location exists. 
5.	state (string): The name of the state in which the location exists.

#### [Subtemplate 3 : Address Tokens (PREMIUM OFFERING)](#Subtemplate_3_:_sbt_address_token)
1.	houseNumber (string): The house number of the location. 
2.	houseName (string): The name of the location.
3.	locality (string): The name of the locality where the location exists. 
4.	street (string): The name of the street of the location.
5.	subSubLocality (string): The name of the sub-sub-locality where the location exists. 
6.	subLocality (string): The name of the sub-locality where the location exists.
7.	village (string): The name of the village if the location exists in a village.
8.	poi (string): The name of the POI if the location is a place of interest (POI).

#### [Subtemplate 4 : Contact Details (PREMIUM OFFERING)](#Subtemplate_4_:_sbt_contact_details)

1.	email
2.	mobile
3.	telephone
4.	website


#### [Subtemplate 5 : Location Coordinates (PREMIUM OFFERING)](#Subtemplate_5_:_sbt_loc_coordinates)

1.	latitude(double): The latitude of the location. 
2.	longitude(double): The longitude of the location.

#### [Subtemplate 6 : E/E Coordinates (PREMIUM OFFERING)](#Subtemplate_6_:_sbt_nav_coordinates)

1.	entry_lat(double):The entry latitude of the location.
2.	entry_lon(double):The entry longitude of the location.

#### [Subtemplate 7 : Category details of place (PREMIUM OFFERING)](#Subtemplate_7_:_sbt_place_cat)

1. placeCategory(onject): Category of place 
2. placeType(string): Type of place

#### [Subtemplate 8 : Category details of place (PREMIUM OFFERING)](#Subtemplate_8_:_sbt_amenities)

Adds applicable `values` within an array of objects available within the `keyInfo` array of object, which itself is within `richInfo` object.

- `richInfo` (object)
  - `keyInfo` (array of objects) - a generic object array containing a wide list of response properties available as 
    - `heading` (string) - the value of this property represents the type of details available.
    - `icon` (string) - the icon url applicable for this heading.
    - `values` (array of objects) - each containing key-value pairs of applicable details.
      - `icon` (string) - icon applicable to this detail.
      - `title` (string) - the name of this detail.
      - `value` (string) - the value of this detail.

#### [Subtemplate 9 : EV details of place (PREMIUM OFFERING)](#Subtemplate_9_:_sbt_ev_details)

Adds applicable `values` within an array of objects available within the `evInformation` object, which itself is within `richInfo` object.

- `richInfo` (object)
  - `evInformation` (object) - a generic ev information object  containing a wide list of response properties available within it. 
    - `evses` (array of objects) containing ev charging machine details within it per evse.
      - `powerType`(string): power type of machine/evseId possible values AC & DC
      - `evseId`(string): Unique machine/evse id
      - `connectors` (array of objects): contains details of connectors: 
         1. `plugTyp`(string): type of plug
         2. `level`(string): Level of plug
         3. `power`(string): Power of connector in KW
         4. `connectorId`(string): Unique id of connector

#### [Subtemplate 10 : EV  Machine details of place (PREMIUM OFFERING)](#Subtemplate_10_:_sbt_ev_machine_details)

Adds applicable `values` within an array of objects available within the `evInformation` object, which itself is within `richInfo` object.

- `richInfo` (object)
  - `evInformation` (object) - a generic ev information object  containing a wide list of response properties available within it. 
    - `evses` (array of objects) containing ev charging machine details within it per evse.
      - `powerType`(string): power type of machine/evseId possible values AC & DC
      - `evseId`(string): Unique machine/evse id

#### [Subtemplate 11 : EV details with tariff of place (PREMIUM OFFERING)](#Subtemplate_11_:_sbt_ev_details_with_tariff)

Adds applicable `values` within an array of objects available within the `evInformation` object, which itself is within `richInfo` object.

- `richInfo` (object)
  - `evInformation` (object) - a generic ev information object  containing a wide list of response properties available within it. 
    - `evses` (array of objects) containing ev charging machine details within it per evse.
      - `powerType`(string): power type of machine/evseId possible values AC & DC
      - `evseId`(string): Unique machine/evse id
      - `connectors` (array of objects): contains details of connectors: 
         1. `plugTyp`(string): type of plug
         2. `level`(string): Level of plug
         3. `power`(string): Power of connector in KW
         4. `connectorId`(string): Unique id of connector5.
         5. `payMode`(string) : Mode of payment
         6. `payDuration`(string): Price/cost/tariff in time based system
         7. `priceUnit`(string): Price/cost/tariff per `Unit` of electricity consumed
   

## [Sample Response](#Sample-Response)

**1.`Subtemplate Claim set`** subTemplates = Admin Tokens, Address Tokens, General Details

**`Input URL:`** https://explore.mappls.com/apis/O2O/entity/3F45CB

**`Response:`**

```
{
    "type": "POI",
    "poi": "The Lalit New Delhi",
    "locality": "Connaught Place",
    "district": "New Delhi District",
    "subDistrict": "Connaught Place",
    "city": "New Delhi",
    "state": "Delhi",
    "pincode": "110001",
    "address": "15, Barakhamba Avenue, Connaught Place, New Delhi, Delhi, 110001",
    "name": "The Lalit New Delhi",
    "eloc": "3F45CB"
}
```

**2. `Provider with subtemplate claim set: `** subTemplates = General Details, Location Coordinates

<**`Input URL:`** https://explore.mapmyindia.com/apis/O2O/entity/3F45CB

**`Response:`**

```
{
    "type": "POI",
    "address": "15, Barakhamba Avenue, Connaught Place, New Delhi, Delhi, 110001",
    "name": "The Lalit New Delhi",
    "eloc": "3F45CB",
    "latitude": RESTRICTED,
    "longitude": RESTRICTED
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
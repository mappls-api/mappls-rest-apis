[<img src="https://about.mappls.com/about/images/MAPPLS-MapmyIndia-logo.png" height="40"/> </p>](https://about.mappls.com/api/)

#  Get Optimization Solution API

**Easy To Integrate Maps & Location APIs & SDKs For Web & Mobile Applications**

Powered with India's most comprehensive and robust mapping functionalities.

## Getting Access

Before using the API in the your solution, please ensure that the related access is enabled in the [Mappls Console](https://apis.mappls.com/console/), in the same project you set up for the Maps SDK.

1. Copy and paste the generated `access token` from your API [keys](https://apis.mappls.com/console/) available in the dashboard in the sample code for interactive map development.
    - This APIs follow OAuth2 based security.
    - `Access Token` can be generated using Token Generation API.
    - To know more on how to create your access tokens, please use our authorization API URL. More details available [here](https://developer.mappls.com/mapping/tokenGeneration)
    - The `access token` is a valid by default for 24 hours from the time of generation. This can be configured by you in the API console.
2. **`Security Type`**
    VRP
    This APIs follow OAuth2 based security. **To know more on how to create your authorization tokens, please use our authorization token URL. More details available**  [here](https://developer.mappls.com/mapping/tokenGeneration)

## Introduction
The Goal in route optimization (Job Assignment & Route Optimization) is to get an optimal set of routes for a fleet of vehicles to traverse in order to deliver to a given set of customers. It generalizes the well-known travelling salesman problem (TSP). 

The objective of this API is to minimize the duration, determine and minimize vehicles used & optimize the distance travelled(optimized route), so it can reduce the overall cost and provide maximum profit.

This is the `GET` method API where we need to pass the `requestID` received from Post Optimization API output to get the status or the desired output of Route Optimization.

## Output Description

Format: JSON

## response

The `response` object has the following properties:
| Key         | Description |
| ----------- | ----------- |
| [`summary`](#Summary) | object summarizing solution indicators | |
| [`routes`](#routes) | array of `route` objects |


## Summary

The `summary` object has the following properties:

| Key         | Description |
| ----------- | ----------- |
| `cost` | total cost for all routes |
|`computing_times`| time in miliseconds taken for the output|
| `unassigned` | number of tasks that could not be served |
| `service` | total service time for all routes |
| `violation` |  |
| `duration` | total travel time for all routes |
| `waiting_time` | total waiting time for all routes |
| `priority` | total priority sum for all assigned tasks |
| [`delivery`] | total delivery for all routes |
| [`pickup`] | total pickup for all routes |
| [`distance`] | total distance for all routes |


## computing_times

A `computing_times` object has the following properties (for internal purposes only):
| Key         | Description |
| ----------- | ----------- |
| `routing` | |
| `solving` | |
| `laoding` | |
| `total` | sum of routing, solving and loading |

## Routes

A `route` object has the following properties:

| Key         | Description |
| ----------- | ----------- |
| `vehicle` | id of the vehicle assigned to this route |
| [`steps`](#steps) | array of `step` objects |
| `cost` | cost for this route |
| `service` | total service time for this route |
| `violations` |  |
| `duration` | total travel time for this route |
| `waiting_time` | total waiting time for this route |
| `priority` | total priority sum for tasks in this route |
| [`delivery`] | total delivery for tasks in this route |
| [`pickup`] | total pickup for tasks in this route |
| [`description`] | vehicle description, if provided in input |
| [`geometry`] | polyline encoded route geometry |
| [`distance`] | total route distance |


## Steps

A `step` object has the following properties:

| Key         | Description |
| ----------- | ----------- |
| `type` | a string (either `start`, `job`, `pickup`, `delivery`, `break` or `end`) |
| `arrival` | estimated time of arrival at this step |
| `duration` | cumulated travel time upon arrival at this step |
| `service` | service time at this step |
| `violation` |  |
| `waiting_time` | waiting time upon arrival at this step |
| [`description`] | step description, if provided in input |
| [`location`] | coordinates array for this step (if provided in input) |
| [`id`] | id of the task performed at this step, only provided if `type` value is `job`, `pickup`, `delivery` or `break` |
| [`load`] | vehicle load after step completion (with capacity constraints) |
| [`distance`] | traveled distance upon arrival at this step |

<br> <br>

## HTTPS Method
GET
## Security Type
This APIs follow OAuth2 based security. **To know more on how to create your authorization tokens, please use our authorization token URL. More details available**  [here](https://developer.mappls.com/mapping/tokenGeneration)

## Request Headers

The API leverages OAuth 2.0 based security. Hence, the developer would need to send a request for access token using their client_id and client_secret to the OAuth API. Once validated from the OAuth API, the access_token and the token_type need to be sent as Authorization header with the value: “{token_type} {access_token}”.

-  `Authorization:  “token_type access_token”`

## Response Type

`application/json`
<br><br>
## Request Parameters
There is only one parameter in the Get Optimization Solution API. The query parameter in the URL of Get Optimization Solution API where unique id received from **Post Optimization API** request will be given as an input.

## Response Parameters

**1. Summary**
-  **`duration`** (integer): total traveled time for all routes. 
 - **`delivery`** (integer):  total number of delivery points for all routes. 
   - `cost` (integer): total cost for all routes.
-  **`computing_times`**: time in seconds taken for the output (for internal purposes only).
    - `routing`
    - `total` : sum of routing, solving and loading
    - `solving`
    - `loading`
- **`distance`** (integer): Total calculated distance for all routes.
- **`waiting_time`** (integet): Total waiting time for all routes.
- **`service`** (integer): Total service time for all routes in seconds.
- **`violation`** :
- **`pickup`** (integer): Total number of pickup for all routes.
   - `unassigned` : Number of tasks that could not be served.
   - `priority` : Total priority sum for all assigned tasks. 


 **2. Routes**
- **`delivery`** (integer):  Total number of delivery points for tasks on this route.
 - **`cost`** (integer): Cost for this route.
- **`distance`** (integer): Total distance of this route. 
- **`waiting_time`** (integer): Total waiting time for this route.
- **`violations`** :
- **`description`** (string): Vehicle description (if provided in input). 
- **`pickup`** (integer): Total number of pickup tasks on this route. 
- **`priority`** (integer): Sum of priority assigned for tasks on this route.
- **`steps`** (array): 
   - `duration` (integer): Cumulative travel time upon arrival at this step.
   - `load` (integer): Vehicle load after step completion (with capacity constraints). 
   - `distance` (integer):  Traveled distance upon arrival at this step.
   - `waiting_time` (integer): waiting time upon arrival at this step.
   - `arrival` (integer): Estimated time of arrival at this step. 
   - `service` (integer): Service time invested at this step. 
   - `description` (string):step description (if provided in input). 
   - `location` (float): Coordinates array for this step (if provided in input).
   - `id` (integer):  id of the task performed at this step, only provided when `type` value is given as `job`, `pickup`, `delivery` or `break` 
   - `type` (string):  a string (either `start`, `job`, `pickup`, `delivery`, `break` or `end`) 
   - `job`:
 - **`vehicle`** (integer): id of the vehicle assigned on this route. 
  - **`duration`** (integer): Total traveled time on this route.
  - **`service`** (integer): Service time invested on this route. 
  - **`geometry`** (string): Encoded polyline route geometry of this route. 

**3. Unassigned** : unassigned job,vehicle and shipment on this route
  - `location` - location of the vehicle/job/shipment whichever is unassigned
       - `id` - id of the unassigned job/vehicle/shipment

## Response Codes
### Success

1. 200: To denote a successful data submission.

### Client-Side Issues

2.	400: Bad Request, User made an error while creating a valid request.
3.	401: Unauthorized, Developer’s key is not allowed to send a request.
4.	403: Forbidden, Developer’s key has hit its daily/hourly limit.
5.  409: Conflict.

### Server-Side Issues

7.	500: Internal Server Error, the request caused an error in our systems.
8.	503: Service Unavailable, during our maintenance break or server downtimes.

## Response Messages

1. 200: Request Submitted Successfully.
2. 400: Something’s just not right with the request.
3. 401: Access Denied.
4. 403: Forbidden, Services for this key has been suspended due to daily/hourly transactions limit.
5. 409: Conflict.
6. 500: Something went wrong.
7. 503: Maintenance Break.
### Sample Input (cURL)
```
Curl --location --request	GET 'https://apis.mappls.com/advancedmaps/Route Optimization/v1/getOptimizationSolution?requestId=1da827b1-bf8f-11eb-afd9-4134b973424d' \
--header 'token: axxfxxddxxexx29xx5xx0xxdxxeexx77'
```
### Sample Output(JSON) 
```json
{
  "msg": "Completed",
  "code": 200,
  "response": {
    "summary": {
      "duration": 3222,
      "delivery": [
        10,
        2
      ],
      "cost": 3222,
      "computing_times": {
        "routing": 4,
        "total": 110,
        "solving": 0,
        "loading": 106
      },
      "distance": 32013,
      "waiting_time": 0,
      "service": 600,
      "pickup": [
        0,
        0
      ],
      "unassigned": 3,
      "priority": 0
    },
    "routes": [
      {
        "duration": 3222,
        "delivery": [
          10,
          2
        ],
        "cost": 3222,
        "distance": 32013,
        "waiting_time": 0,
        "service": 600,
        "description": "Tata Ace Dstr01",
        "pickup": [
          0,
          0
        ],
        "geometry": "mpgmDsnrvMBfA@b@DLD@DB@BDH@D?JADCFCBEBE@I?E?CCGGKCM?iBDgBFeBD_A@KAGAGEGEQQMQE@C?CAEAECeAp@m@d@KHcAj@b@hAb@`AXn@b@x@^l@PP^Tn@Zl@TxC`Ah@Pj@PbAXr@Pj@Pv@AlBf@~Af@|@\\vAdARRd@l@Rd@x@ZNFRFL@p@E~Bq@vAa@vAa@nBo@nBm@hAYfCq@`AWn@Sf@MlA_@HEb@M~CaA~C_At@UvAc@|@YvC}@vC}@xC_A|Bq@dBi@fBi@VIJEdA[pA_@~@[lA_@|@WfA]tBo@tAa@tAc@PGd@OnBk@~@]dAc@|@e@hAq@LGdBgAtA{@tA{@\\k@DMJe@BS@QAQGi@q@cBs@eBw@mBq@cBs@eBm@wAm@yAKWs@cBs@eBGM{@wB{@yBi@uAGKMWaAwBqAsCs@wBu@uBaAaC]}@aAmCo@eCo@eCw@yCY}@IYo@sB}@yCaA_DaAaDcA_D_@mASq@Uu@eAeDcA_Da@kAk@cB_@aAo@_BiAuDo@{Bq@}B}@oC{@oCs@yBs@sBs@qBm@iBGWGUq@mCw@}Ce@gBw@qCk@{B_@wAKY[{@_@{@We@q@_AiA{AW[IMc@k@w@cA}AoBeBqBIMCKE]DWL]zBsCz@eApBqC`AqBj@cAHe@}AiA}AgAeB}@[UOO_AiAgAqAw@oAoBcCqBcCoBaCoAcBqAaBMMs@_AmAyAkAwAyAiByAkByAiBi@o@qA_BqAaBqAyASWa@e@Ui@}A_BW]a@g@mAwAg@i@[c@aAwAy@mA{@mAu@aBu@cBKSc@mAUo@_@eAm@cBw@cCw@eCu@cCW_ASy@Og@{@mC_A{C_A{C}@{Cu@eCu@gCu@gCe@a@s@cCu@cCu@cCe@mA[kAMq@w@wCi@sBKm@GYAEK[MW_@g@u@}@WWU[OSGIw@i@Y]Yc@e@eAI]KQoB{CmB{CgBcCgBeC{AwByAwB{AyBkAcBiAcBUBG?GAEAGCECIIIKCGCI@U?GBIBGDIcBcCoBqCw@mAsAmBqAoBuAsBuAsBS]wAsBuAuBu@cAOSk@{@y@oAmAgBmAgBCEy@wAgBeCSYg@s@w@gAm@{@MO_@i@_AyA_AyAk@y@w@kA[e@{@oAIMOWo@y@U[mBuCq@}@kAcBGKi@y@QWe@s@g@u@a@o@{AwBu@eAWa@m@_AsAmBaB}BES?C@CBAD@JB^j@V\\PXRXp@`AlAJf@a@lAkAlAiAvBwBxBuBiA}BUiAWsBWuBnAUREYiBBOXs@Yr@CNXhBSDoATVtBVrBThAhA|ByBtBwBvBmAhAmAjAg@`@@`BpAfBx@jAV\\n@|@X`@b@p@f@p@`@p@PVbAvAj@x@dBbCtApBX^bArA~A|B~A~B|@tA`@n@BFDHTZZd@\\h@TZb@r@^j@~@vA~@vArArBpArBr@bA|@nANRvAtBdA`BdA~AhA~Av@hAfA|AzA|B|A~BhA`BhAbB|AvBHCFAN?NDDBHDFHDFDL@F?NANEJ^l@hBzCbAxAx@lA|@vAlAdBLP|AzB~AzBpAhBpAhBnAhBZ^JJdBhCT^rBzCz@bBBD@@BHNb@Pf@V|@z@lCd@p@Vr@Nf@Tv@P|@VdAp@pCd@fBf@dBr@jCt@hCt@hC|@xC|@xC|@xCb@xA\\v@j@rANlAjAvDjAvDHV|@jCLZTn@d@pAxA`Df@~@^n@hA~ARXpBlCpBxBlAtAtAvAdAhANNDD^b@zAfBxAhBl@p@t@|@b@V^NdAV~AZ~BVnAvApAvApBhCpBhCbBtBbBrBdBtB~AtBXZd@h@fBbCf@p@HLFLp@dBRlBGn@Ij@K`@k@jAcAjBuBrCuAdBsAdBKPGLEPJb@BHFJVX^d@nB`ClBbC`@h@dAtA|@pAR\\`@v@X|@Nd@ZbAl@bCl@`Cl@`C`AhDh@vBFRJTNj@^bA~@rC~@tCVz@t@~Bv@~Bt@|Bz@jCx@hCVj@h@dBbA~Cf@bBd@bBfAhDHV\\dATr@RLJTRd@Pd@z@dCf@~Af@~Ab@rARl@p@vBh@`BJZHVL^b@nB@XANCVCVCFELABU\\UZYRWJk@Tq@LQBS?OAQAOCICg@W{@_@SEOCQ?WDQHYNWL]PmAj@MFgAf@{@J{@j@gCzA{@l@eChBeCfBcCfBaCdBcCfBkAv@_Bv@uAj@iBt@iBr@qCvAsA~@gAjAWTe@d@gCtBiCtB{@r@sBtAuBtAeCbBeC`BeCbBeC`BeCbBQ\\KPQNmAjAmCbBsA|@sAz@MJIHGJILEJENEXAd@@J@`@`AbCbAdClAzCnAzCP\\JPJNVRh@\\PP^Tn@Zl@TxC`Ah@Pj@PbAXr@Pj@Pv@AlBf@~Af@|@\\vAdARRd@l@?N?HCFCBC@GAEAMGe@i@a@a@aAm@w@[sAc@}C}@a@K_AYw@Sc@OOEsBo@sBm@_Ac@YOs@g@q@k@W_@KSWImAqCkAqC@ODKBAFEJCB?L?D@HFx@`B\\GNGb@W\\YtAmA@C@CBADCD@D?D@D@@B@@BF@D?B?DDHBFJNFDHDF@J@|CKbCItAEHCHA@EBEDCDABAF?EMAc@CgA",
        "priority": 0,
        "steps": [
          {
            "duration": 0,
            "load": [
              10,
              2
            ],
            "distance": 0,
            "arrival": 1600419678,
            "location": [
              77.268443,
              28.55168
            ],
            "type": "start"
          },
          {
            "duration": 1620,
            "load": [
              0,
              0
            ],
            "distance": 16003,
            "waiting_time": 0,
            "arrival": 1600421298,
            "service": 300,
            "description": "Customer 1 , address , city, postalcode",
            "location": [
              77.370176,
              28.578955
            ],
            "id": 1,
            "type": "job",
            "job": 1
          },
          {
            "duration": 3222,
            "load": [
              0,
              0
            ],
            "distance": 32013,
            "waiting_time": 0,
            "arrival": 1600423200,
            "service": 300,
            "id": 2,
            "type": "break"
          },
          {
            "duration": 3222,
            "load": [
              0,
              0
            ],
            "distance": 32013,
            "arrival": 1600423500,
            "location": [
              77.268443,
              28.55168
            ],
            "type": "end"
          }
        ],
        "vehicle": 52
      }
    ],
    "code": 0,
    "unassigned": [
      {
        "location": [
          77.523416,
          12.96941
        ],
        "id": 6
      },
      {
        "location": [
          77.523459,
          12.969498
        ],
        "id": 5
      },
      {
        "location": [
          77.523442,
          12.969504
        ],
        "id": 2
      }
    ]
  }
}
```

## Disclaimer
1. This API is released for select use cases only; Please contact Mappls API Support or your account manager for discussions on usage of this solution. 
2. Mappls reserves the right to revoke access of this API at its own discrection.


## Document Version History

| Version | Last Updated | Author |
| ---- | ---- | ---- |
| 0.0.1 | November 2021 | Mappls API Team ([KB](https://github.com/kunalbharti)) |

## API Version History

| Version | Last Updated | Author | Revised Sections |
| ---- | ---- | ---- | ---- |
| 0.1 | 2021-06-17 | Mappls API Team ([PS](https://github.com/map-123)) | Initial release |
<br>


For any queries and support, please contact: 

[<img src="https://www.mapmyindia.com/images/logo.png" height="40"/> </p>](https://www.mapmyindia.com/api)
Email us at [apisupport@mapmyindia.com](mailto:apisupport@mapmyindia.com)


![](https://www.mapmyindia.com/api/img/icons/support.png)
[Support](https://www.mapmyindia.com/api/index.php#f_cont)
Need support? contact us!

<br>

[<p align="center"> <img src="https://www.mapmyindia.com/api/img/icons/stack-overflow.png"/> ](https://stackoverflow.com/questions/tagged/mapmyindia-api)[![](https://www.mapmyindia.com/api/img/icons/blog.png)](http://www.mapmyindia.com/blog/)[![](https://www.mapmyindia.com/api/img/icons/gethub.png)](https://github.com/MapmyIndia)[<img src="https://mmi-api-team.s3.ap-south-1.amazonaws.com/API-Team/npm-logo.one-third%5B1%5D.png" height="40"/> </p>](https://www.npmjs.com/org/mapmyindia) 



[<p align="center"> <img src="https://www.mapmyindia.com/june-newsletter/icon4.png"/> ](https://www.facebook.com/MapmyIndia)[![](https://www.mapmyindia.com/june-newsletter/icon2.png)](https://twitter.com/MapmyIndia)[![](https://www.mapmyindia.com/newsletter/2017/aug/llinkedin.png)](https://www.linkedin.com/company/mapmyindia)[![](https://www.mapmyindia.com/june-newsletter/icon3.png)](https://www.youtube.com/user/MapmyIndia/)




<div align="center">@ Copyright 2024 CE Info Systems Ltd. All Rights Reserved.</div>

<div align="center"> <a href="https://www.mapmyindia.com/api/terms-&-conditions">Terms & Conditions</a> | <a href="https://www.mapmyindia.com/about/privacy-policy">Privacy Policy</a> | <a href="https://www.mapmyindia.com/pdf/mapmyIndia-sustainability-policy-healt-labour-rules-supplir-sustainability.pdf">Supplier Sustainability Policy</a> | <a href="https://www.mapmyindia.com/pdf/Health-Safety-Management.pdf">Health & Safety Policy</a> | <a href="https://www.mapmyindia.com/pdf/Environment-Sustainability-Policy-CSR-Report.pdf">Environmental Policy & CSR Report</a>

<div align="center">Customer Care: +91-9999333223</div>
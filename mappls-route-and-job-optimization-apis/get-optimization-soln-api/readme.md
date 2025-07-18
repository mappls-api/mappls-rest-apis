[<img src="https://about.mappls.com/about/images/MAPPLS-MapmyIndia-logo.png" height="40"/> </p>](https://about.mappls.com/api/)

#  Get Optimization Solution API

**Easy To Integrate Maps & Location APIs & SDKs For Web & Mobile Applications**

Powered with India's most comprehensive and robust mapping functionalities.

## Getting Access

Before using the API in the your solution, please ensure that the related access is enabled in the [Mappls Console](https://apis.mappls.com/console/), in the same project you set up for the Maps SDK.

1. Copy and paste the generated `access token` from your API [keys](https://apis.mappls.com/console/) available in the dashboard in the sample code for interactive map development.
    - This APIs follow OAuth2 based security.
    - `Access Token` can be generated using Token Generation API.
    - To know more on how to create your access tokens, please use our authorization API URL. More details available [here](https://github.com/mappls-api/mappls-rest-apis/tree/main/mappls-token-generation-api)
    - The `access token` is a valid by default for 24 hours from the time of generation. This can be configured by you in the API console.
2. **`Security Type`**
    VRP
    This APIs follow OAuth2 based security. **To know more on how to create your authorization tokens, please use our authorization token URL. More details available**  [here](https://github.com/mappls-api/mappls-rest-apis/tree/main/mappls-token-generation-api)

## Introduction
The Goal in route optimization (Job Assignment & Route Optimization) is to get an optimal set of routes for a fleet of vehicles to traverse in order to deliver to a given set of customers. It generalizes the well-known travelling salesman problem (TSP). 

The objective of this API is to minimize the duration, determine and minimize vehicles used & optimize the distance travelled(optimized route), so it can reduce the overall cost and provide maximum profit.

This is the `GET` method API where we need to pass the `requestID` received from Post Optimization API output to get the status or the desired output of Route Optimization.

## URL

```
https://apis.mappls.com/advancedmaps/vrp/v1/getOptimizationSolution
```

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
This APIs follow OAuth2 based security. **To know more on how to create your authorization tokens, please use our authorization token URL. More details available**  [here](https://github.com/mappls-api/mappls-rest-apis/tree/main/mappls-token-generation-api)

## Request Headers

The API leverages OAuth 2.0 based security. Hence, the developer would need to send a request for access token using their client_id and client_secret to the OAuth API. Once validated from the OAuth API, the access_token and the token_type need to be sent as Authorization header with the value: “{token_type} {access_token}”.

-  `Authorization:  “token_type access_token”`

## Response Type

`application/json`
<br><br>
## Request Parameters
There is only one parameter in the Get Optimization Solution API. The query parameter in the URL of Get Optimization Solution API where unique id received from **Post Optimization API** request will be given as an input.

1. `requestId` (string): The request ID received in response of the `postOptimizationRequest` API.

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
Curl --location --request	GET 'https://apis.mappls.com/advancedmaps/vrp/v1/getOptimizationSolution?requestId=1da827b1-bf8f-11eb-afd9-4134b973424d' \
--header 'token: axxfxxddxxexx29xx5xx0xxdxxeexx77'
```
### Sample Output(JSON) 
```json
{
    "summary": {
        "delivery": [
            3
        ],
        "cost": 5813,
        "computing_times": {
            "routing": 0.007,
            "total": 0.12100000000000001,
            "solving": 0.0,
            "loading": 0.114
        },
        "distance": 63877,
        "waiting_time": 0,
        "violations": [],
        "pickup": [
            1
        ],
        "unassigned": 0,
        "priority": 0,
        "duration": 5813,
        "routes": 1,
        "service": 1200,
        "setup": 0
    },
    "msg": "Completed",
    "routes": [
        {
            "delivery": [
                3
            ],
            "cost": 5813,
            "distance": 63877,
            "waiting_time": 0,
            "violations": [],
            "pickup": [
                1
            ],
            "priority": 0,
            "steps": [
                {
                    "duration": 0,
                    "load": [
                        3
                    ],
                    "distance": 0,
                    "waiting_time": 0,
                    "arrival": 1600419146,
                    "service": 0,
                    "violations": [],
                    "setup": 0,
                    "location": [
                        77.26894638016765,
                        28.550833533042766
                    ],
                    "type": "start"
                },
                {
                    "duration": 454,
                    "load": [
                        2
                    ],
                    "distance": 4125,
                    "waiting_time": 0,
                    "arrival": 1600419600,
                    "service": 300,
                    "violations": [],
                    "setup": 0,
                    "location": [
                        77.25014802489044,
                        28.56370655591404
                    ],
                    "id": 1,
                    "type": "job",
                    "job": 1
                },
                {
                    "duration": 1678,
                    "load": [
                        1
                    ],
                    "distance": 20637,
                    "waiting_time": 0,
                    "arrival": 1600421124,
                    "service": 300,
                    "violations": [],
                    "setup": 0,
                    "location": [
                        77.25046301534559,
                        28.67277872908568
                    ],
                    "id": 5,
                    "type": "job",
                    "job": 5
                },
                {
                    "duration": 3259,
                    "load": [
                        2
                    ],
                    "distance": 34731,
                    "waiting_time": 0,
                    "arrival": 1600423005,
                    "service": 300,
                    "violations": [],
                    "setup": 0,
                    "location": [
                        77.13402954533225,
                        28.687340657215927
                    ],
                    "id": 2,
                    "type": "job",
                    "job": 2
                },
                {
                    "duration": 4901,
                    "load": [
                        1
                    ],
                    "distance": 54721,
                    "waiting_time": 0,
                    "arrival": 1600424947,
                    "service": 300,
                    "violations": [],
                    "setup": 0,
                    "location": [
                        77.20054141166888,
                        28.563214295078236
                    ],
                    "id": 6,
                    "type": "job",
                    "job": 6
                },
                {
                    "duration": 5813,
                    "load": [
                        1
                    ],
                    "distance": 63877,
                    "waiting_time": 0,
                    "arrival": 1600426159,
                    "service": 0,
                    "violations": [],
                    "setup": 0,
                    "location": [
                        77.26894638016765,
                        28.550833533042766
                    ],
                    "type": "end"
                }
            ],
            "vehicle": 1,
            "duration": 5813,
            "service": 1200,
            "setup": 0,
            "geometry": "_kgmDsqrvMDb@Bl@Bb@@ZDl@FbAcAFk@Cm@?MACFCBEBE@I?E?CCGGKCM?gBDiBFgBHeABKAGCGCGEa@k@GACCCCMFIDo@h@mA|@m@\\b@hAb@`AP^FNb@x@^l@b@^TLd@Vn@TxC~@h@Pj@Pj@NjAZj@P^AzCn@hA^|@\\vAdARRd@l@?N?HADEDG?EAQGe@i@a@a@aAm@w@[sAc@}C}@a@KQGUGOE_AWc@OOEsBo@sBm@e@Ss@_@s@g@i@Dc@Jc@Pe@Rc@Pq@\\aAt@e@`@w@~@[^}@v@i@b@}BlB_ClBw@n@iA~@gA|@OJwAnAi@f@YX_@f@[b@[l@M\\GNQj@m@`Bk@`Be@xAIVIl@CZAZJdE@P?zBBfEBfEAjACj@O|BMnBE`AEf@Gf@GVMd@Ur@_@r@KPMPg@`@WFUFw@Lq@BK?k@@q@@aBJqBLo@Du@FAUGcBK}AIk@Ic@EQIYo@eA}@uAkA{@]SsAo@sAm@_@Oc@Qo@W_@QWe@eBm@u@[g@Y[WWUa@e@i@s@a@q@KSg@sAUs@IOUa@a@q@m@u@u@iAqAqB_AaBiAkBiAkBoAyBmAwBS_@gAkBeAmBgBaDiBaDsAkCwAeCw@sAy@qAa@k@}@mAc@k@_A_@cBi@i@Is@Gc@C[?k@Bs@Hi@Jm@Tk@XmB`Ag@v@w@lAy@pA{@pA_AxA]x@}AhC_A~AaA~Ay@xAy@xAeApBYf@ABYj@QT]d@m@j@o@f@WNQHi@Tq@Rm@RUFq@FgB^gCl@eCl@eCj@}Ct@_Dr@}Cr@c@L]JeCv@eCt@eCv@kCp@kCp@yB@}AMo@Gg@Ik@OWIc@Qi@WaAw@{@}@s@eAq@sAc@sAWy@m@gBq@qBq@oBoAsDmAqDoAqDmAqDoAqDmAqDaAwCaAwCi@cB?MAKCIGUOa@a@sAKYI[ESESC[y@iC{@iCkAiDkAkDeAyCcAyCu@sB_@gAs@wBo@cBi@oAg@kAgAqBi@{@mAgBg@u@eAmAcAiAmAeA}BsBoBgBqBeBc@SUKc@YQMy@q@a@[YQSKQGWG]WkAcAQCS?WBkATyAt@uBjAsBjAk@B[NyAz@yAx@OFSJSLmBfAmBfAWN[Pc@Vy@d@{C|AuC~A}BvA}BxAyAz@{A|@sAv@sAt@[RuChBuAv@w@b@eAl@]X_@^e@p@e@z@S`@g@vA_@`AYv@c@jA]l@_@f@a@d@WTg@\\k@XcAZWFUD{@Fm@?kBGkBG_BCi@Bs@Nm@RoBlAoBhAmBhAOFMDsBHuA@o@AiAAeDNeDNeDNeDN}CP_DRcBNeBNk@Fu@FwBLyBHwBHyBHq@D_BJyBHwBHyBHy@FkBJmBJyBLyBLy@Hu@NgA\\y@Z[NcBfAsAv@qAv@k@`@{B|AyB|AyB|AcCdBkAt@UVQNe@`@i@f@kA~@iA~@aCtAoBlAg@XmBvAmBvAWPiAt@o@d@gAv@uChB}AbA}BbBi@`@]Zm@p@W\\i@hAo@|@iArB_A|A_A|AQPSNk@ZYTGJQd@k@nBi@lBaAnDWjACV?NB`@m@^k@Ta@JaBRc@COCOCKEMMGIIQIWu@}DYkAKg@E]e@}Dm@Ay@JSDk@Je@N]@_@BwA@}AC]CaBA_BCy@E[Ay@IgBYo@IMFIHGHKRGj@UhCUjCWhCEf@IfAGn@Yv@YvCWtCd@JPLVD@G@KWCUBe@KYzCWzCE`AC\\CNSdAEXQzAYbDYdDK`BAz@EfBDnABh@Br@JhAJt@RrAVbAv@pCt@rCv@pCt@rCh@pBDNz@zCz@|Cz@|Cz@|Cz@|Cn@`Cp@~Bp@vDp@tDl@fDl@fDl@fDl@fDXlAJ`@`@pAT|@Jj@TzAh@|Ch@|CRlA\\bBNfAT~A^bC^dCRnARnAVtBd@lCFh@NfARvCDr@?^Eh@Ih@[zCE`@QfBCNOfAGn@Mv@Gj@ChASxBUrBOxAEl@Ct@Bl@Dp@Hr@Lz@J^\\v@\\dAGLMPGRE^G~@Gt@BXBDBFFFXNl@NPDtBp@~Ab@v@TfB^n@Nn@PVFNDjA`@r@Vb@PWp@g@a@QI{Ak@m@~Co@~CAh@Kx@UlAWhAq@vBSv@UpBSfBSdBE\\QfAW~AETi@tCg@vCSjAId@[fB[fBI^_@vB[lB]nBa@vBe@hCIf@QbAi@zCi@|Ci@zCGXEVi@bDk@bDk@bDY`B[`Bi@bDS`BIr@E|@EjAIzDGbDArB?tBARC|@CrAA^KrBMrBGnAQrAW|B[fCWvBMlAMdAQnAWvBKx@Gd@e@zDa@rDCVW~CG`@IZa@nAWx@Un@Md@Up@Sn@ENK`@Kh@CXC^Cj@Al@B~AFr@FXJ\\ZdAn@hBj@pAXl@R^r@vAHNZn@bAnBvAfAz@l@\\XLHVLNF\\L^JR?^FN@LDNHJHHJHJDNFHDJ@P?L?DCNCFCDIJEBKDM?@t@MZk@~Ai@`Bm@lBk@hBQf@_AtC}@tCW~@Kf@MbAMrBEn@Ej@[v@c@fDEd@[xCSbB[pCYnCS|BUlCEt@WlCWlCStCUnCKpASrCOhCOhCIjAGdAMnBOpBMlBOnBUtDNx@KpAUnCUnCUpCIr@LPFNDR?F?NCPGJKNIFKBE@I?GAKEIEGGGIIUGQkBe@QLKFQBM@_@E[KcBa@cBa@wAUwAU]CY@e@P[NGNyCbByCbBo@`@EFEHABQ`CSbCEN[Ci@Ag@?_@A_DCqCAm@Am@Ac@?m@Aa@?_@A]?]?WAS?r@fBRr@H^BJBR@L@N@J?PA\\C`A?JK?i@Ag@?g@Ak@?y@AoBAqBAmCCm@DI@KFIHGLYr@@J?DADCJCZCj@AFEXGp@c@hCCJICBG@G@C^aCHwA@s@E?E?IEEICCAG?KBKBEBCDCBAhAaANGLEXARAj@@rA?vA@x@@|B@rA@~@@RQNQJQ?g@?[CYEYAKIWQk@GOIUGQSg@Oc@c@kAm@cBQc@o@gBOa@k@_B_AeC]cAOi@Mg@Gc@Iq@E_@Gs@AMA[@{@@g@@UDUTuAh@eBPa@\\i@NWHKHKHKNMTUrAgAtAgAf@a@v@m@l@e@JPZf@l@dAVb@bAbBbAbB|AlCFj@p@hAj@~@RXl@t@\\\\j@`@h@\\j@ZZLZH~A^\\Fr@NfDp@hDp@v@TnCl@nCj@nCl@nCl@fCv@hCx@vC|@vC~@fAd@`@Rb@Rl@b@t@n@\\Xp@v@p@v@z@fAjB~B|AlB|AjB|AlB^b@lA|AlA|AbApAt@ZfAvAhAxA`AlA`AnARTLPdBlBrAzAt@`Aj@`@p@j@VJJBPBp@BpBFnBFvABH@d@C~@Lv@Pt@PbBxAdAbAdAbAtBpBDh@`BxA`Az@fBzAfBzAnAhAnAfAh@^r@^z@Zl@L`AJbAAt@Gh@Ep@MzAg@rCgAxBw@zBy@rBm@rBo@rBm@nC{@f@MjBe@t@Sn@SxBm@JCjA]xAa@xAc@tCy@pBm@nBm@x@Up@QdD}@b@Kh@MtCw@tCy@tCy@zBm@|Bm@xCy@xCy@`Co@~Bq@`Co@x@UpBo@rBm@n@St@UvCy@h@OdCq@bCs@dCs@rCy@zAa@xAa@zAa@xAc@lCu@lCw@lCu@lCw@pBk@pBi@|Aa@|A_@b@Gd@CnDDpDDhAB`DG`DG`B@vCGrAEx@CfAE|@IhBa@p@[f@[lBwAr@c@rA_AtAmAtAmAb@YlBoAb@Ev@g@p@m@l@a@l@a@VQb@[dBoA|@m@v@u@bBmBr@}@fAiBv@eB^iAJ]TgCVsBJi@XiALu@RgBRgB\\gEZ}DX{DXcDVcDXcDVeDXcDV}CX_DDg@XeBV_Ab@gAz@wAz@yAlBuCnBwCtAyBrAwBpAgBnAgBpBqC`AqA^i@jBkChAaAt@k@jBiA|A_A~AaA|A_AzA}@tAy@nAu@tAy@pA{@RKz@_@fBs@bAa@fBq@pB{@x@i@l@a@rAy@rAw@`@Wl@_@nAu@nAu@Z[ZUPKLGb@Ux@e@pAs@hAk@fAo@lBgAz@e@bB{@rAo@jCwAxBcAbAe@bBu@vBeAd@UrCuAr@]fAg@n@]ZMfCgAfCiA`Bw@xAs@hCoAjCqA~BmAl@[b@SvAu@vBkAvBiAvBsA`Am@xBqBhAqAfAyApAcCd@y@Ve@`@}@rAaDb@wAReADi@Ba@HqAFmBPgDDi@DiAHyARmDRkDP{CP}CP}CDkB@aCAmACcCAqAAe@Ag@G{AAo@Ck@OgDE_AEiAQYMiDOiDAy@GuA?Qz@Av@Ax@AlDGJ?J?tACt@K^GdA_@pCqAh@Qv@Mh@GPAPArAOpBWvC_@tC_@@N_BRUD{Cd@yBRK@o@Fk@FQB{@Hs@Lo@RqAl@y@b@mA^_@Fs@HgBDqDDu@?{@D}@@?QEcBAo@?s@?y@?WHwCFoBRi@FkDDgBBeBLeEDiB@k@?m@AWCUIe@So@SYkAgBeAwBISU{@CU?s@Ba@Ha@DOZm@NWVYLKfA_An@_@`@[JMJWDMNi@ToA?wA@u@FgDFiDDgDFmCFoCDsC@O@i@DgB@wADkBH{D?]@Y@gAFuDBqABqA@w@BwAFw@JyAN{AViBTiA|@sCJa@t@aCr@_Cr@aCt@eCRm@jAoDv@qC`@mBFa@Do@Ba@HoAHiBPeENcEPsDNqDPsD@y@LcDLaDNaDNaDAwDKqDIoD_@mAI{BI{BGgBIgBGiBCm@ASE_BCc@Ag@Aa@GgBGgBGkBAu@Cg@E}AAUt@E|@Gj@CdBK|AI~AIt@IPCPCZO`@[FKLOR]Vk@Pi@DUFYBO@QD[P}CP{C@i@BiAEqDCqD?iA?}AAQCiBCiB?[BYD]HYbAoCPg@t@aCJ]JSR_@N[Vc@x@eAHKTURQvAoAJKfAw@jAcAlAcAbA{@jAcA\\WpAiAVSPMPS|@aAnAkAJIb@[r@g@|@e@\\ShAs@MSIKKSWImAqCkAqCDQDIFGJCP?D@HFx@`B\\GNGHEt@m@bA}@FEPG@CBEDA\\a@b@c@rAkArAkArAkArAiAZ]X]?K?EDGDGFCH?HBBBDFXOl@Ox@rCBLDNNn@FTBP@P@L"
        }
    ],
    "unassigned": [],
    "respCode": 200
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
[<img src="https://about.mappls.com/images/mappls-logo.svg" height="40"/> </p>](https://about.mappls.com/api/)

# Custom Search - GET Records along the route API


## Introduction

This API allows one to search the records as per specified record type from the Custom search database in an along the route manner around a provided path.
The GET Records along the route API allows organizations and companies to search the locations based records and entities added as per their custom modules along a planned route. 

## URL

```html
https://search.mappls.com/search/byod/route?
```

## Input Method

POST

## Getting Access

Before using the API in the your solution, please ensure that the related access is enabled in the [Mappls Console](https://auth.mappls.com/console/), within your app - be it for Mobile OR Web or Cloud integration.

1. Copy and paste the key from your `credentials` section from your API [keys](https://auth.mappls.com/console/) into the `access_token` query parameter.
    - Your static key can be secured by whitelisting its usage for particular IPs (in case of cloud app usage) OR a set of domains (in case of a web app)
    - Your static key obtained from your Console is to be passed as a query parameter: `access_token`.

## Authentication Object - `access_token` mandatory query parameter.

-  `access_token`: "hklmgbwzrxncdyavtsuojqpiefrbhqplnm".


## Request Type

`application/x-www-form-urlencoded`

## Response Type

`application/json`

## Response Codes

### Success

1. 200: To denote a successful API call. 
2. 204: To denote the API was a success but no results we’re found.

### Client-Side Issues

3.	400: Bad Request, User made an error while creating a valid request.
4.	401: Unauthorized, Developer’s key is not allowed to send a request.
5.	403: Forbidden, Developer’s key has hit its daily/hourly limit.

### Server-Side Issues

7.	500: Internal Server Error, the request caused an error in our systems.
8.	503: Service Unavailable, during our maintenance break or server downtimes.

## Response Messages

1. 200: Success.
2. 204: No matches we’re found for the provided query.
3. 400: Something’s just not right with the request.
4. 401: Access Denied.
5. 403: Forbidden, Services for this key has been suspended due to daily/hourly transactions limit.
6. 500: Something went wrong.
7. 503: Maintenance Break.

## Request Body

### Mandatory Parameters For Nearby Search

### Mandatory Parameters

1. `path` (string) This parameter takes the encoded route along which records have to be searched.
2. `recordType (string)` : The category or class of the record, referenced by a defined set of category codes from client.  

### Optional Parameters
3. `sort` (valueless): Gets the sorted records along route.
4. `geometries` (string): Type of geometry encoding, accepted values are `polyline5`, `polyline6`, and `base64`. Default value is `polyline5`.
5. `buffer` (number): Buffer of the road. Minimum value is `25`, maximum is `1000` and default is `25`.
6. `page` (number): Used for pagination. By default, a request returns maximum `10` results and to get the next `10` or so on pass the page value accordingly. Default is 1.



## Sample cURL Request

```c
curl --location 'https://search.mappls.com/search/byod/route?access_token=hklmgbwzrxncdyavtsuojqpiefrbhqplnm' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'path=ugimDyesvM??g@D@xB@l@@z@@~@@RBv@DxB?JAz@A`CBzD?L@J@HDJBFZl@JVSNg@^u@h@cAp@cAl@m@`@sA`Ag@Zm@b@kAv@k@^MHaAl@MHkBtAiBpAgBnAoBnA{BzA{BzAyBzA{BzA{BzAqCdBsBrAi@\\e@XoAx@oAx@_BhA_BhA_CbBcAp@_An@YRa@XKFi@\\QLuCpBsCnBwBbBkAv@cBhAcBhAqBrAqBrAyBxAsAz@sA|@e@Ti@Nc@Jw@J}BR}@JMDMJaA`AuApAwAfAkB|AmBzAkB|AGD{AlA{AjA{BjB_@Xa@Vk@\\mCjAiAf@IBiAf@sAp@IDYNOJ}BtAqBrAsBrAsBpAi@^e@ZSTKPWh@AJAFEPEDKLEBMDG@Q?GAICKEGIe@TkBlAkAv@qCfBgBhAgBjAgBhAeAl@{BpAyBnA}BpA}BnA}BpAe@VsA`As@d@mBlAgAn@a@TmBfAmBhAgB~@gB~@yAx@MFuAj@sAp@sAn@sCrAoB~@oB~@oB~@iB|@iBz@w@^EDGHEJERp@nBr@vBBX@JBV?RATALE^Kd@GJuAlCm@tAk@lAuAhCWf@GJOPOHKFQFa@H[@{@AmBGyACsAEQAaBGo@Cw@PYFQJSLUTEJ_AnBqApC}A`DDFDFBFBL?LAF?DELCDIHKDEBK?G?MCGCEEk@pA_@x@w@fB_@t@KRm@nAe@bAYh@]t@Yj@y@dB}A~C}A~COx@JNHRFRBV?RAR?DCNIRKRIHGDGFMFI@KBO?OAMCKEKG_@v@[p@u@~AaAnBaApBQ^HJBL@J?HAHENGHCBGBMBK?ULCBMNS^mAfCe@dAa@z@MXm@nAMVCFAH?NBNDJ@HBL@JALAJAHEJILIHGDIBKBG@MAM@MDGBGDo@nAQ^e@~@uAvCwAvCuAvCwAvCa@x@gA~BG\\AZLTFTDP@P?XANEXELCFILIJCT@L@PBJz@pCz@bCh@|ARh@r@vBTp@\\`AfAdDPf@fAzCN^DHBDPRJGFCNAN@D@LFLPHR@H@FAHALEJCDKJEDEZA^?HDNZv@`@hAb@nABR?HAJADGJKJOHg@AaCG_CGe@B_@HINIPMVa@x@Ud@IPS`@OZS`@g@bAwA|CFDFDDFBH@H@HALCHEFEFIDKD{@dBgA|BgA~B_ApB}@nBq@dAw@z@qA|@}@d@eCx@eB`@cB`@_Dr@}Cr@}Cr@CTADCHEFGDGBIBE?KAQNMPEHi@lCk@jCk@jC]jAqAhDCHUf@GLg@lAQ^MZ[p@k@lAu@`Bc@`ASb@gA~BeAzB}@rBKRu@bBu@bBw@fBw@fB_AtBy@lBUd@s@lAU`@_AbB_A|AKPMTq@jAw@~Aa@v@DBDHDFBN@J?JAFCHEJEBIHE@E@I?MAEA_@VUNORKT{@vB}@dBu@tAs@rAwArCy@bBgArBgArByAvC{AxCqAhCqAhCkA|BkA~B}@fBa@t@Ub@o@pAeApBgApBa@z@S^i@fAGJ}@fB{@dBe@~@EH[l@i@fA_AhB_AjBGJ}@hB{@fBUf@u@bBKR_AfBWj@s@vA}@fBgAtBYj@aAhByApCyApC_BzC_BzC_BzCe@dAg@|@_@r@eArBeApBOXS\\eApBeArBeApBc@|@w@xBe@zAiAlCaAfBaAfBa@b@}BdCgBjAgBjAqChByA|@sAz@yA|@yA~@aCzAoBfAm@b@_A~@Wb@sAtBkB`Cs@|@UBKBWR}AeB}AeB}AgBEi@s@M}@g@?A{@a@gBs@uBq@uBq@oBk@qBm@KNIFKBCd@SfEUfESfEUGY|DYzDSfDUdDUfDUfD[`EEr@SbDARY`EWbEYbEYbEWbEALUbDSbDSbDSbDSbDUfDIlAUhDWhDWvDWtDUvDIrACVIrAGl@C`@SrCSrCMtBMrBQ`CQ`CMjBSzCU|CUzCO`CO~BAPQlCQlCQlCYdDQvCOvCOxCQvCSpDUpDG~@OnBMlBUxCIdAG`BE|@Cz@KrBIpBQbES`EKfBIfBGv@OxCMrBQrDSpDSpD?NMvBOpBMrBIjBKtAQxCKrBKrBSjDUhDKdBMdBEnCQtCQxAObDKpBMpBQxCQzCEjBA`ANn@@z@AdBChDApDApCd@P\\Nh@Rf@\\rA~@rA~@FRXVTNNJjA~@jBzAvBtBfBfBJLVX`@\\bAbAdAbA`A~@THlAjAj@j@|@x@^ZpAjA`Ax@hA~@lA`Ad@\\~ApAp@h@^Zn@h@jBzAlB|Ap@h@VRDM@GHMHEJCBiA?_BBoBAy@bAA~@Az@@j@Al@@T?\\Ah@CP?d@AZ?b@?b@?Z?t@@l@@n@?Ap@' \
--data-urlencode 'recordType=Retailer' \
--data-urlencode 'buffer=1000' \
--data-urlencode 'page=1' \
--data-urlencode 'sort='
```

## Sample Response

```json
{
    "responseCode": 200,
    "suggestedPOIs": [
        {
            "distance": 23,
            "customNote": "",
            "createdOn": 1699516070,
            "recordType": "Retailer",
            "modifiedOn": "",
            "latitude": 28.5608852,
            "longitude": 77.272313,
            "address": "",
            "recordId": "2009258",
            "extendedInfo": {
                "District_Name": "South",
                "Outlet_ID": "DL-0055171",
                "Region_ID": "NDE1",
                "District_ID": "98"                
            },
            "orderIndex": 1
        },
        {
            "distance": 884,
            "customNote": "",
            "createdOn": 1699516066,
            "recordType": "Retailer",
            "modifiedOn": "",
            "latitude": 28.5651867,
            "longitude": 77.2796434,
            "address": "",
            "recordId": "2009236",
            "extendedInfo": {
                "District_Name": "South",
                "Outlet_ID": "DL-0075805",
                "Region_ID": "NDE1",
                "District_ID": "98"
            },
            "orderIndex": 2
        },
        {
            "distance": 3211,
            "customNote": "",
            "createdOn": 1699516932,
            "recordType": "Retailer",
            "modifiedOn": "",
            "latitude": 28.5806201,
            "longitude": 77.2482701,
            "address": "",
            "recordId": "2014171",
            "extendedInfo": {
                "District_Name": "South",
                "Outlet_ID": "DL-0054817",
                "Region_ID": "NDE1",
                "District_ID": "98"
            },
            "orderIndex": 3
        },
        {
            "distance": 10258,
            "customNote": "",
            "createdOn": 1699516111,
            "recordType": "Retailer",
            "modifiedOn": "",
            "latitude": 28.6326451,
            "longitude": 77.20628,
            "address": "",
            "recordId": "2009493",
            "extendedInfo": {
                "District_Name": "New Delhi",
                "Outlet_ID": "DL-0008944",
                "Region_ID": "NDE1",
                "District_ID": "94"
            },
            "orderIndex": 4
        },
        {
            "distance": 14496,
            "customNote": "",
            "createdOn": 1700466285,
            "recordType": "Retailer",
            "modifiedOn": "",
            "latitude": 28.6473928,
            "longitude": 77.1611775,
            "address": "",
            "recordId": "5285",
            "extendedInfo": {
                "District_Name": "West",
                "Outlet_ID": "DL-0036487",
                "Region_ID": "NDE1",
                "District_ID": "96"
            },
            "orderIndex": 5
        },
        {
            "distance": 14584,
            "customNote": "",
            "createdOn": 1699515000,
            "recordType": "Retailer",
            "modifiedOn": "",
            "latitude": 28.64693451,
            "longitude": 77.15950775,
            "address": "",
            "recordId": "2003189",
            "extendedInfo": {
                "District_Name": "Central",
                "Outlet_ID": "DL-5000887",
                "Region_ID": "NDE1",
                "District_ID": "95"
            },
            "orderIndex": 6
        },
        {
            "distance": 15454,
            "customNote": "",
            "createdOn": 1699514675,
            "recordType": "Retailer",
            "modifiedOn": "",
            "latitude": 28.6568867,
            "longitude": 77.1578,
            "address": "",
            "recordId": "2001508",
            "extendedInfo": {
                "District_Name": "Central",
                "Outlet_ID": "DL-5563138",
                "Region_ID": "NDE1",
                "District_ID": "95"
            },
            "orderIndex": 7
        },
        {
            "distance": 15620,
            "customNote": "",
            "createdOn": 1700465755,
            "recordType": "Retailer",
            "modifiedOn": "",
            "latitude": 28.6515736,
            "longitude": 77.1500555,
            "address": "",
            "recordId": "1765",
            "extendedInfo": {
                "District_Name": "Central",
                "Outlet_ID": "DL-0008752",
                "Region_ID": "NDE1",
                "District_ID": "95"
            },
            "orderIndex": 8
        },
        {
            "distance": 15860,
            "customNote": "",
            "createdOn": 1700466648,
            "recordType": "Retailer",
            "modifiedOn": "",
            "latitude": 28.6555859,
            "longitude": 77.1507708,
            "address": "",
            "recordId": "7639",
            "extendedInfo": {
                "District_Name": "Central",
                "Outlet_ID": "DL-0036627",
                "Region_ID": "NDE1",
                "District_ID": "95"
            },
            "orderIndex": 9
        },
        {
            "distance": 17591,
            "customNote": "",
            "createdOn": 1699514355,
            "recordType": "Retailer",
            "modifiedOn": "",
            "latitude": 28.6605541,
            "longitude": 77.1323101,
            "address": "",
            "recordId": "2000083",
            "extendedInfo": {
                "District_Name": "West",
                "Outlet_ID": "DL-5473327",
                "Region_ID": "NDE1",
                "District_ID": "96"
            },
            "orderIndex": 10
        }
    ],
    "pageInfo": {
        "pageCount": 1,
        "totalHits": 29,
        "totalPages": 3,
        "pageSize": 10
    }
}
```

<br><br>

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

[<img src="https://about.mappls.com/api/img/mapmyindia-api.png" height="40"/> </p>](https://about.mappls.com/api/)
# Elevation API

**Easy To Integrate Maps & Location APIs & SDKs For Web & Mobile Applications**

Powered with India's most comprehensive and robust mapping functionalities.
**Now Available**  for Srilanka, Nepal, Bhutan, Bangladesh and Myanmar

You can get your api key to be used in this document here: [https://about.mappls.com/api/](https://about.mappls.com/api/)

## Introduction

The **Elevation API** provides elevation data above the sea level for location on Earth’s surface. The **Elevation API** allows you to retrieve sampled elevation data along a path. This API can be useful for biking, trucking & in other routing applications.

## Input Method
GET

## Input URL

`https://apis.mappls.com/advancedmaps/v1/<REST_KEY>/elevation?locations=lat1,lon1|lat2,lon2`

## Response Type

JSON: Response will served as JSON

## Response Codes {as HTTP response code}

- 200: To denote a successful API call.
- 204: DB Connection error.
- 400: Bad Request, User made an error while creating a valid request.
- 401: Unauthorized, Developer’s key is not allowed to send a request.
- 403: Forbidden, Developer’s key has hit its daily/hourly limit or IP or domain not white-listed.
- 404: HTTP not found
- 412: Precondition Failed, i.e. Mandatory parameter is missing
- 500: Internal Server Error, the request caused an error in our systems.
- 503: Service Unavailable, during our maintenance break or server down-times.

## Request Parameters
### Mandatory Parameters
- **`locations:`** The location coordinates are expressed in pairs of (latitude,longitude|latitude,longitude).
- **`REST_KEY`**: The REST API licence key allocated to you by signing into our services and registering yourself as a developer (28 Char Alphanumeric).


## Sample Input

`https://apis.mappls.com/advancedmaps/v1/<REST_KEY>/elevation?locations=9.538350,76.998825|8.930019,76.655587`

## Sample Response

```json
{
    "responseCode": 200,
    "version": "211.18",
    "results": [
        {
            "longitude": 76.998825,
            "latitude": 9.53835,
            "elevation": 523
        },
        {
            "longitude": 76.655587,
            "latitude": 8.930019,
            "elevation": 31
        }
    ]
}
```

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

<div align="center"> <a href="https://about.mappls.com/api/terms-&-conditions">Terms & Conditions</a> | <a href="https://www.mappls.com/about/privacy-policy">Privacy Policy</a> | <a href="https://www.mappls.com/pdf/mappls-sustainability-policy-healt-labour-rules-supplir-sustainability.pdf">Supplier Sustainability Policy</a> | <a href="https://www.mappls.com/pdf/Health-Safety-Management.pdf">Health & Safety Policy</a> | <a href="https://www.mappls.com/pdf/Environment-Sustainability-Policy-CSR-Report.pdf">Environmental Policy & CSR Report</a>

<div align="center">Customer Care: +91-9999333223</div>
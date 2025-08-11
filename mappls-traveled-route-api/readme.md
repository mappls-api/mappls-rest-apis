[<img src="https://about.mappls.com/about/images/MAPPLS-MapmyIndia-logo.png" height="40"/> </p>](https://about.mappls.com/api/)

# Mappls Traveled Route API

This API can be used to get an image of map with traveled route plotted on it. The image size can be specified; which will dynamically create an image of varying zoom levels with the start and end locations plotted on it.

## Getting Access

Before using the API in the your solution, please ensure that the related access is enabled in the [Mappls Console](https://auth.mappls.com/console/), within your app - be it for Mobile OR Web or Cloud integration.

1. Copy and paste the key from your `credentials` section from your API [keys](https://auth.mappls.com/console/) into the `access_token` query parameter.
    - Your static key can be secured by whitelisting its usage for particular IPs (in case of cloud app usage) OR a set of domains (in case of a web app)
    - Your static key obtained from your Console is to be passed as a query parameter: `access_token`.

## Authentication Object - `access_token` mandatory query parameter.

-  `access_token`: "hklmgbwzrxncdyavtsuojqpiefrbhqplnm".

## API URL

1.  The API URL should be of the following construct:  https://tile.mappls.com/map/raster_tile/still_image_polyline?
2. **Output**  format will be an 8-bit PNG image of varying sizes.
3.  The method used is  **POST**.

## Request Parameters

The following input parameters will be supported in the Travelled Route API request –  
The body content will be of `form-data` type, consisting of the following parameters:

### Mandatory Parameters:

1.  `height:` The height of the image resolution that is required.
2.  `width:` The width of the image resolution that is required.
3.  `polyline:` An array of comma separated [Longitude,Latitude] points that define the polyline along which the route was traversed.

### Optional Parameters:

1. `color:` hex color ie. #3edhhs  
2. `icon_from:` url: [https://maps.mappls.com/images/from.png](https://maps.mappls.com/images/from.png)  
3. `icon_to:`url: [https://maps.mappls.com/images/to.png](https://maps.mappls.com/images/to.png)  
4. `offset:`[top,right]
5. `padding_x:`number (in pixels); Max: 150
6. `padding_y:`number (in pixels); Max: 150
7. `markers:`An Array of comma separated [Longitude,Latitude], Custom Markers to be embedded in the image during the trip.
8. `markers_icon:`URL for the Custom Marker.


### Response Parameters

The following output parameters will be supported in the Travelled Route API response

1.  An 8-bit png image of  `height` x `width`  resolution.

## Performance

The Traveled Route API is a resource intensive API that consumes considerable computing power of the server. This API is meant to be used sparingly and hence has an above average response time. The Traveled Route API must respond within 2500 ms under standard circumstances. If you are parsing the custom marker in the image with your custom marker URL than the performance average response time would be more than what in standard circumstances.

## Example

**Input**:  
```
https://tile.mappls.com/map/raster_tile/still_image_polyline?&access_token=hklmgbwzrxncdyavtsuojqpiefrbhqplnm
```

**Body**
```json
height:400
width:400
polyline:[[77.227437,28.611004],[77.227385,28.611011],[77.226859,28.610907],[77.224885,28.610022],[77.224906,28.609965],[77.224906,28.609843],[77.224885,28.609786],[77.224788,28.609682],[77.224702,28.609644],[77.224595,28.609635],[77.224456,28.609682],[77.224349,28.609795],[77.220347,28.608005],[77.21892,28.607336],[77.218963,28.607148],[77.218942,28.60696],[77.218824,28.606677],[77.21876,28.606602],[77.218578,28.606385],[77.218374,28.606263],[77.218235,28.606216],[77.218063,28.606188],[77.217956,28.606197],[77.217945,28.605199],[77.217902,28.60438],[77.217859,28.603674],[77.217827,28.603033],[77.217773,28.602223],[77.217698,28.600933],[77.217805,28.600924],[77.217902,28.600886],[77.217988,28.600829],[77.218074,28.600707],[77.218106,28.600622],[77.218106,28.6005],[77.218085,28.600434],[77.218021,28.60033],[77.217882,28.600226],[77.217753,28.600188],[77.217571,28.600197],[77.217453,28.600244],[77.217389,28.600291],[77.217292,28.600404],[77.216798,28.600197],[77.215897,28.599801],[77.214384,28.599123],[77.212785,28.598407],[77.211326,28.597729],[77.211347,28.597682],[77.211336,28.597588],[77.211239,28.597484],[77.211196,28.597465],[77.211067,28.597465],[77.210992,28.597493],[77.210938,28.59755],[77.209575,28.596947],[77.20935,28.596853],[77.207998,28.59625],[77.20759,28.596071],[77.207526,28.596005],[77.207462,28.595996],[77.207033,28.596109],[77.20684,28.596156],[77.205295,28.596495],[77.204555,28.596561],[77.203546,28.596533],[77.20243,28.59642],[77.201218,28.59609],[77.200596,28.596109],[77.19992,28.596137],[77.199019,28.596175],[77.198826,28.596053],[77.198826,28.595996],[77.198772,28.595855],[77.198675,28.59577],[77.1986,28.595742],[77.198557,28.595723],[77.198428,28.595723],[77.198299,28.595761],[77.198235,28.595808],[77.197055,28.595516],[77.196529,28.59545],[77.196132,28.595431],[77.19566,28.595459],[77.194533,28.595695],[77.193986,28.595865],[77.193911,28.595799],[77.193772,28.595761],[77.193633,28.595789],[77.193515,28.595883],[77.193472,28.596005],[77.193483,28.596062],[77.193032,28.596241],[77.190908,28.597108],[77.190854,28.597042],[77.190768,28.596995],[77.190661,28.596967],[77.190532,28.596976],[77.190457,28.597004],[77.19035,28.597089],[77.190307,28.597155],[77.190286,28.597287],[77.190318,28.597391],[77.189095,28.5979],[77.188655,28.59807],[77.187775,28.598419],[77.187743,28.598362],[77.187646,28.598296],[77.187549,28.598268],[77.18741,28.598287],[77.187313,28.598334],[77.187238,28.598438],[77.187227,28.598532],[77.187259,28.598626],[77.183686,28.600058],[77.181991,28.600727],[77.181809,28.60084],[77.181498,28.601057],[77.181058,28.601528],[77.180897,28.601726],[77.180715,28.601811],[77.180618,28.60183],[77.180403,28.601811],[77.17933,28.601265],[77.175446,28.599212],[77.17521,28.59909],[77.174877,28.598911],[77.173965,28.598431],[77.173718,28.598309],[77.173471,28.598168],[77.172666,28.597754]]
color:#ff00f7
markers:[[77.217698,28.600933],[77.193986,28.595865]]
markers_icon:https://img.icons8.com/dusk/25/000000/region-code.png
```
### Output: :
![enter image description here](https://mmi-api-team.s3.ap-south-1.amazonaws.com/API-Team/Still_Image_Polyline.png)

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
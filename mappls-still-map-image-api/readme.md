[<img src="https://about.mappls.com/about/images/MAPPLS-MapmyIndia-logo.png" height="40"/> </p>](https://about.mappls.com/api/)

# Mappls Still Map Image API

The Still Map Image API creates a map based on URL parameters sent through a standard HTTP request and returns the map as an image which you can display on your application. The API lets you embed Mappls Maps image according to geo-position, pixel size and zoom level of the map on your application without requiring any dynamic page loading. The image can be a retina image and markers can be added to the image to indicate position of any object.

## Getting Access

Before using the API in the your solution, please ensure that the related access is enabled in the [Mappls Console](https://auth.mappls.com/console/), within your app - be it for Mobile OR Web or Cloud integration.

1. Copy and paste the key from your `credentials` section from your API [keys](https://auth.mappls.com/console/) into the `access_token` query parameter.
    - Your static key can be secured by whitelisting its usage for particular IPs (in case of cloud app usage) OR a set of domains (in case of a web app)
    - Your static key obtained from your Console is to be passed as a query parameter: `access_token`.

## Authentication Object - `access_token` mandatory query parameter.

-  `access_token`: "hklmgbwzrxncdyavtsuojqpiefrbhqplnm".

## API URL

1.  The API URL should be of the following construct:  https://tile.mappls.com/map/raster_tile/still_image?<Parameters>
2. **Output**  format will be an 8-bit PNG image of varying sizes.
3.  The method used is  **GET**.

## Request Parameters

Returns PNG data to draw map tile at position specified with coordinates (centre of the image), image size, scale factor and zoom level. The request parameters that specify the image.

### Mandatory Parameters:

1.  `center:` A WGS-84 position coordinate that specifies the centre of the image requested.

### Optional Parameters:

1. `zoom:` The zoom level for which the image is requested. Ranges from 4 to 18 with 18 being the highest zoomed in level.  
2. `size:` The size of the image requested in pixels as <Width>x<Height>.
3. `ssf:`scale factor indicating retina or non-retina tiles. 
    <br>0→non-retina tiles.
    <br>1→retina tiles.
4. `markers:` Optional markers that you may want to add to the map tile.
5. `markers_icon:` The URL of the Custom Marker.


### Response Parameters

The following output parameters will be supported in the Travelled Route API response

1.  An 8-bit png image.

## Performance

The Performance is dependent on WAN/LAN/WLAN speed & also on the URL you are going to provide in the *`markers_icon`*

## Transaction Information

One Request (which returns one image) using the API link will be considered as one transaction.

## Use Cases

- To show a quick location point without having to additionally add a Map Control.
- To show multiple locations on map without the need to add a Map Control.

## Example

**Input**:  
https://tile.mappls.com/map/raster_tile/still_image?center=28.5959394,77.2255611&zoom=15&size=400x400&ssf=1&markers=28.5959394,77.2255611&access_token=hklmgbwzrxncdyavtsuojqpiefrbhqplnm

### Output: :
![enter image description here](https://mmi-api-team.s3.ap-south-1.amazonaws.com/API-Team/still_image.png)

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
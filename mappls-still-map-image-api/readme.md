[<img src="https://www.mappls.com/api/img/mappls-api.png" height="40"/> </p>](https://www.mappls.com/api)

# Mappls Still Map Image API

The Still Map Image API creates a map based on URL parameters sent through a standard HTTP request and returns the map as an image which you can display on your application. The API lets you embed Mappls Maps image according to geo-position, pixel size and zoom level of the map on your application without requiring any dynamic page loading. The image can be a retina image and markers can be added to the image to indicate position of any object.

## API URL

1.  The API URL should be of the following construct:  https://apis.mappls.com/advancedmaps/v1/<licence_key>/still_image?<Parameters>
2. **Output**  format will be an 8-bit PNG image of varying sizes.
3.  The method used is  **POST**.

## Request Parameters

Returns PNG data to draw map tile at position specified with coordinates (centre of the image), image size, scale factor and zoom level. The request parameters that specify the image.

### Mandatory Parameters:

1.  `licence_key:` The REST API licence key allocated to you.
2.  `center:` A WGS-84 position coordinate that specifies the centre of the image requested.

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
https://apis.mappls.com/advancedmaps/v1/<REST_KEY>/still_image?center=28.5959394,77.2255611&zoom=15&size=400x400&ssf=1&markers=28.5959394,77.2255611

### Output: :
![enter image description here](https://mmi-api-team.s3.ap-south-1.amazonaws.com/API%20Team/still_image.png)

For any queries and support, please contact: 

[<img src="https://www.mappls.com/images/logo.png" height="40"/> </p>](https://www.mappls.com/api)
Email us at [apisupport@mappls.com](mailto:apisupport@mappls.com)


![](https://www.mapmyindia.com/api/img/icons/support.png)
[Support](https://www.mappls.com/api/index.php#f_cont)
Need support? contact us!

<br></br>
<br></br>

[<p align="center"> <img src="https://www.mapmyindia.com/api/img/icons/stack-overflow.png"/> ](https://stackoverflow.com/questions/tagged/mappls-api)[![](https://www.mapmyindia.com/api/img/icons/blog.png)](http://www.mappls.com/blog/)[![](https://www.mapmyindia.com/api/img/icons/gethub.png)](https://github.com/Mappls-api)[<img src="https://mmi-api-team.s3.ap-south-1.amazonaws.com/API-Team/npm-logo.one-third%5B1%5D.png" height="40"/> </p>](https://www.npmjs.com/org/mapmyindia) 



[<p align="center"> <img src="https://www.mapmyindia.com/june-newsletter/icon4.png"/> ](https://www.facebook.com/Mappls)[![](https://www.mapmyindia.com/june-newsletter/icon2.png)](https://twitter.com/Mappls)[![](https://www.mapmyindia.com/newsletter/2017/aug/llinkedin.png)](https://www.linkedin.com/company/mappls)[![](https://www.mapmyindia.com/june-newsletter/icon3.png)](https://www.youtube.com/user/Mappls/)




<div align="center">@ Copyright 2022 CE Info Systems Ltd. All Rights Reserved.</div>

<div align="center"> <a href="https://www.mappls.com/api/terms-&-conditions">Terms & Conditions</a> | <a href="https://www.mappls.com/about/privacy-policy">Privacy Policy</a> | <a href="https://www.mappls.com/pdf/mappls-sustainability-policy-healt-labour-rules-supplir-sustainability.pdf">Supplier Sustainability Policy</a> | <a href="https://www.mappls.com/pdf/Health-Safety-Management.pdf">Health & Safety Policy</a> | <a href="https://www.mappls.com/pdf/Environment-Sustainability-Policy-CSR-Report.pdf">Environmental Policy & CSR Report</a>

<div align="center">Customer Care: +91-9999333223</div>
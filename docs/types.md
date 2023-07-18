[<img src="https://about.mappls.com/about/images/MAPPLS-MapmyIndia-logo.png" height="40"/> </p>](https://about.mappls.com/api/)

# List of 'type' of manoeuvres for MapmyIndia Route API response.

| Type	| Description | 
| ---- | ---- | 
| turn	| a basic turn into direction of the  modifier | 
| new name	| no turn is taken/possible, but the road name changes. The road can take a turn itself, following modifier . | 
| depart	| indicates the departure of the leg | 
| arrive	| indicates the destination of the leg | 
| merge	| merge onto a street (e.g. getting on the highway from a ramp, the  modifier specifies the direction of the merge) | 
| on ramp	| take a ramp to enter a highway (direction given my  modifier) | 
| off ramp	| take a ramp to exit a highway (direction given my  modifier) | 
| fork	| take the left/right side at a fork depending on  modifier | 
| end of road	| road ends in a T intersection turn in direction of  modifier | 
| use lane	| Deprecated replaced by lanes on all intersection entries | 
| continue	| Turn in direction of  modifier to stay on the same road | 
| roundabout	| traverse roundabout, if the route leaves the roundabout there will be an additional property  exit for exit counting. The modifier specifies the direction of entering the roundabout. | 
| rotary	| a traffic circle. While very similar to a larger version of a roundabout, it does not necessarily follow roundabout rules for right of way. It can offer rotary_name and/or rotary_pronunciation parameters (located in the RouteStep object) in addition to the exit parameter (located on the StepManeuver object). | 
| roundabout turn	| Describes a turn at a small roundabout that should be treated as normal turn. The modifier indicates the turn direciton. Example instruction:  At the roundabout turn left. | 
| notification	| not an actual turn but a change in the driving conditions. For example the travel mode or classes. If the road takes a turn itself, the  modifier describes the direction | 
| exit roundabout	| Describes a maneuver exiting a roundabout (usually preceeded by a  roundabout instruction) | 
| exit rotary	| Describes the maneuver exiting a rotary (large named roundabout) |

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
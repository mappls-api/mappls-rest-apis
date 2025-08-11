[<img src="https://about.mappls.com/about/images/MAPPLS-MapmyIndia-logo.png" height="40"/> </p>](https://about.mappls.com/api/)

# Parsing Instructions in JavaScript

## Get array of Route Advices of the route by passing complete API JSON response
```js
function instructions(data)
    {
        var _0xd813=['sharp-right','uturn','u-turn','sharp\x20left','sharp-left','left','turn-left','slight\x20left','bear-left','round','bearing_after','northeast','east','southeast','south','southwest','west','northwest','Head\x20','use\x20lane','Continue\x20','\x20onto\x20','Enter\x20the\x20roundabout','exit','\x20and\x20take\x20the\x20','\x20exit','\x20turn\x20','turn','Take\x20the\x20ramp\x20on\x20the\x20','replace','slight','merge','toUpperCase','slice','slightly','indexOf','sharp','Take\x20a\x20','Keep\x20','\x20on\x20','Intermediate\x20','destination','charAt','push','location','distance','leaflet-routing-icon-','routes','length','steps','name','maneuver','type','modifier','new\x20name','continue','depart','arrive','reached','roundabout','rotary','fork','on\x20ramp','off\x20ramp','end\x20of\x20road','head','waypointreached','via','destination\x20reached','straight','slight\x20right','bear-right','right','turn-right','sharp\x20right'];(function(_0x5eae1b,_0x235dd8){var _0x486139=function(_0x212f42){while(--_0x212f42){_0x5eae1b['push'](_0x5eae1b['shift']());}};_0x486139(++_0x235dd8);}(_0xd813,0xc5));var _0x58f8=function(_0x24ceac,_0x41a594){_0x24ceac=_0x24ceac-0x0;var _0x3c0b55=_0xd813[_0x24ceac];return _0x3c0b55;};var advise=[''];for(i=0x0;i<data[_0x58f8('0x0')][_0x58f8('0x1')];i++){var route_arr=data[_0x58f8('0x0')][i]['legs'];advise[i]=[];for(var lg=0x0;lg<route_arr[_0x58f8('0x1')];lg++){var leg=route_arr[lg][_0x58f8('0x2')];for(j=0x0;j<leg['length'];j++){var step=leg[j],maneuver='',icon='',road_name=step[_0x58f8('0x3')],type=step[_0x58f8('0x4')][_0x58f8('0x5')],modifier=step[_0x58f8('0x4')][_0x58f8('0x6')],text='';switch(type){case _0x58f8('0x7'):maneuver=_0x58f8('0x8');break;case _0x58f8('0x9'):maneuver='head';break;case _0x58f8('0xa'):maneuver=_0x58f8('0xb');break;case _0x58f8('0xc'):case _0x58f8('0xd'):maneuver=_0x58f8('0xc');break;case'merge':case _0x58f8('0xe'):case _0x58f8('0xf'):case _0x58f8('0x10'):case _0x58f8('0x11'):maneuver=step[_0x58f8('0x4')][_0x58f8('0x5')];break;default:maneuver=step[_0x58f8('0x4')]['modifier'];}switch(maneuver){case _0x58f8('0x12'):if(j===0x0)icon=_0x58f8('0x9');break;case _0x58f8('0x13'):icon=_0x58f8('0x14');break;case _0x58f8('0xc'):icon='enter-roundabout';break;case _0x58f8('0xd'):icon='enter-roundabout';break;case _0x58f8('0x15'):case _0x58f8('0xb'):icon=route_arr[_0x58f8('0x1')]==lg+0x1?_0x58f8('0xa'):_0x58f8('0x14');break;}if(!icon){switch(modifier){case _0x58f8('0x16'):icon='continue';break;case _0x58f8('0x17'):icon=_0x58f8('0x18');break;case _0x58f8('0x19'):icon=_0x58f8('0x1a');break;case _0x58f8('0x1b'):icon=_0x58f8('0x1c');break;case'turn\x20around':case _0x58f8('0x1d'):icon=_0x58f8('0x1e');break;case _0x58f8('0x1f'):icon=_0x58f8('0x20');break;case _0x58f8('0x21'):icon=_0x58f8('0x22');break;case _0x58f8('0x23'):icon=_0x58f8('0x24');break;}}if(type){var dir=Math[_0x58f8('0x25')](step['maneuver'][_0x58f8('0x26')]/0x2d)%0x8;var dd=['north',_0x58f8('0x27'),_0x58f8('0x28'),_0x58f8('0x29'),_0x58f8('0x2a'),_0x58f8('0x2b'),_0x58f8('0x2c'),_0x58f8('0x2d')][dir];if(dd)dir=dd;if(maneuver==_0x58f8('0x12'))text=_0x58f8('0x2e')+dir+(leg[j+0x1][_0x58f8('0x3')]?'\x20on\x20'+leg[j+0x1][_0x58f8('0x3')]:'');else if(maneuver==_0x58f8('0x8')||maneuver==_0x58f8('0x2f'))text=_0x58f8('0x30')+step['maneuver'][_0x58f8('0x6')]+(road_name?_0x58f8('0x31')+road_name:'');else if(maneuver==_0x58f8('0xc'))text=_0x58f8('0x32')+(step[_0x58f8('0x4')][_0x58f8('0x33')]?_0x58f8('0x34')+step[_0x58f8('0x4')]['exit']+_0x58f8('0x35'):'')+(road_name?'\x20onto\x20'+road_name:'');else if(maneuver=='roundabout\x20turn')text='At\x20the\x20roundabout'+(step[_0x58f8('0x4')][_0x58f8('0x6')]?_0x58f8('0x36')+step[_0x58f8('0x4')][_0x58f8('0x6')]:'')+(road_name?_0x58f8('0x31')+road_name:'');else if(maneuver==_0x58f8('0x37')||maneuver=='uturn')text='Make\x20a\x20'+step[_0x58f8('0x4')][_0x58f8('0x6')]+(road_name?_0x58f8('0x31')+road_name:'');else if(maneuver==_0x58f8('0x10')||maneuver==_0x58f8('0xf'))text=_0x58f8('0x38')+step[_0x58f8('0x4')]['modifier'][_0x58f8('0x39')](_0x58f8('0x3a'),'')+(road_name?_0x58f8('0x31')+road_name:'');else if(maneuver=='straight')text='Continue\x20'+step[_0x58f8('0x4')][_0x58f8('0x6')]+(road_name?'\x20onto\x20'+road_name:'');else if(maneuver==_0x58f8('0x21')||maneuver==_0x58f8('0x23')||maneuver==_0x58f8('0x19')||maneuver==_0x58f8('0x1b')||maneuver==_0x58f8('0x3b'))text=type['charAt'](0x0)[_0x58f8('0x3c')]()+type[_0x58f8('0x3d')](0x1)+'\x20'+step['maneuver']['modifier'][_0x58f8('0x39')](_0x58f8('0x3a'),_0x58f8('0x3e'))+(road_name?_0x58f8('0x31')+road_name:'');else if(maneuver==_0x58f8('0xe'))text=(step['maneuver'][_0x58f8('0x6')][_0x58f8('0x3f')](_0x58f8('0x40'))>0x0?_0x58f8('0x41'):_0x58f8('0x42'))+step[_0x58f8('0x4')][_0x58f8('0x6')]['replace'](_0x58f8('0x3a'),'')+'\x20at\x20the\x20fork\x20'+(road_name?_0x58f8('0x31')+road_name:'');else if(maneuver==_0x58f8('0x9'))text=_0x58f8('0x2e')+dir+(road_name?_0x58f8('0x43')+road_name:'');else if(maneuver==_0x58f8('0xb'))text='You\x20have\x20arrived\x20at\x20your\x20'+(route_arr[_0x58f8('0x1')]==lg+0x1?'':_0x58f8('0x44'))+_0x58f8('0x45');else text=step[_0x58f8('0x4')][_0x58f8('0x6')][_0x58f8('0x46')](0x0)['toUpperCase']()+step[_0x58f8('0x4')][_0x58f8('0x6')][_0x58f8('0x3d')](0x1)+(road_name?_0x58f8('0x31')+road_name:'');advise[i][_0x58f8('0x47')]({'text':text,'lat':step[_0x58f8('0x4')]['location'][0x1],'lng':step[_0x58f8('0x4')][_0x58f8('0x48')][0x0],'distance':step[_0x58f8('0x49')],'time':step['duration'],'icon_class':_0x58f8('0x4a')+icon});}}}} return {"routes":advise}
}
```

## Example

**The above array of routes contains instructions as follows:**
```json
routes[0][0]	//First advice from first of the possible routes 
{
	distance: 32.7
	icon_class: "leaflet-routing-icon-depart"
	lat: 28.611048
	lng: 77.227426
	text: "Head west on Akbar Road"
	time: 6.3
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




<div align="center">@ Copyright 2025 CE Info Systems Ltd. All Rights Reserved.</div>

<div align="center"> <a href="https://about.mappls.com/api/terms-&-conditions">Terms & Conditions</a> | <a href="https://about.mappls.com/about/privacy-policy">Privacy Policy</a> | <a href="https://about.mappls.com/pdf/mapmyIndia-sustainability-policy-healt-labour-rules-supplir-sustainability.pdf">Supplier Sustainability Policy</a> | <a href="https://about.mappls.com/pdf/Health-Safety-Management.pdf">Health & Safety Policy</a> | <a href="https://about.mappls.com/pdf/Environment-Sustainability-Policy-CSR-Report.pdf">Environmental Policy & CSR Report</a>

<div align="center">Customer Care: +91-9999333223</div>
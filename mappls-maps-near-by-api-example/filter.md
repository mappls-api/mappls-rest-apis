## [Filter](#Filter)
The filter feature in Nearby API empowers the user a fine discovery of rich datasets (like EV charging stations) along with the existing keyword and category code lookups. It uses multiple keys like "brandId", "model", "plugType". It uses **key:value** pair(s). 
(e.g. brandId:B420)

### Keys available
1. `brandId` : to search for the brand via its ID. IDs are available on request from Mappls.
2. `model`: to search for the places associated with the vehicle model via its model identifier. model identifiers are available on request from Mappls.
3. `plugType`: to search for the places associated with the compatible EV plug type via its identifier. Plug type identifiers are available on request from Mappls.

### How search via filter works

- Each **key:value** pair is seperated by a seperator,
(e.g. filter= brandId:B420, plugType:IEC; model:Mahindra Electric).
- We can use two or more **values** for a **key** by putting either **OR(;)** or **AND($)** operator
(e.g. brandId:B420;B316, plugType:IEC&PN3; model:Mahindra Electric).
- By default key:value pairs are treated as **AND($)** case.

Suppose you want to search all electric vehical charging station of a particular brand(e.g. "Mahindra Electric" ) and of a particular plugType (e.g. "IEC") then you can use filter as:

(filter= brandId:B420, plugType:IEC)

where B420 is brandId for Mahindra Electric and IEC is plugType.

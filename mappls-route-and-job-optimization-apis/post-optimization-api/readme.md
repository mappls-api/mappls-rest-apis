[<img src="https://about.mappls.com/about/images/MAPPLS-MapmyIndia-logo.png" height="40"/> </p>](https://about.mappls.com/api/)

#  Post Optimization Request API
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
    
    This APIs follow OAuth2 based security. **To know more on how to create your authorization tokens, please use our authorization token URL. More details available**  [here](https://developer.mappls.com/mapping/tokenGeneration)


## Introduction
The Goal in route optimization (Job Assignment & Route Optimization) is to get an optimal set of routes for a fleet of vehicles to traverse in order to deliver to a given set of customers. It generalizes the well-known travelling salesman problem (TSP). 

The objective of this API is to minimize the duration, determine and minimize vehicles used & optimize the distance travelled(optimized route), so it can reduce the overall cost and provide maximum profit.

The Post Optimization API request will provide a `requestID` which then needs to pass through a `GET` request method Get Optimization API to get the status or the desired output of Route Optimization.

<img src="https://about.mappls.com/api/optimisation/images/cost-efficient-route.gif?raw=true" style="margin-left:auto;margin-right:auto"/>


## Constraints
### `vehicles`
- Number of Vehicles
- Profile
- Vehicle Capacity
- Break Time
- Skills
- Time Window
- Maximum Travel Time
- Maximum Tasks
- Cost

### `jobs`
- Time Window
- Service Time
- Delivery/Pickup Capacity
- Skills
- Priority

### `shipments`
- Time Window
- Service Time
- Setup time
- Delivery/Pickup Capacity
- Skills
- Priority
- Amount

<br> <br>

# Input
Content-Type:application/json

| Key         | Description |
|-----------|-----------|
| [`vehicles`](#vehicles) |  array of `vehicle` objects describing the available vehicles |
| [`jobs`](#jobs) |  array of `job` objects describing the places to visit |
| [`shipments`](#shipments)|an array of `shipments` objects describing pickup and delivery tasks |

<br>

## Vehicles

**Bold** ones are mandatory; *italic* ones are optional parameters.

A `vehicle` object has the following properties:

- **`id`** (integer): assigned unique id for the vehicle. 
- *`profile`* (string): routing profile includes "driving", "biking" & "trucking" (defaults to `driving`). Only needed as input in the first vehicle, for the remaining vehicles same profile will be used. Currently mixed profiles are not supported.
- *`description`* (string) : a string describing this vehicle.
- **`start`** (float) : coordinates array of the start position.
- **`end`** (float) : coordinates array of the end postion.
- *`capacity`* (integer) : an array of integers describing multidimensional quantities.
- *`skills`* (integer) : an array of integers defining skills.
- *`time_window`* (integer) : a `time_window` object describing working hours.
- *`breaks`* : an array of `break` objects.
  - `id` (integer) : id defined for the `breaks`.
  - `time_windows` (array) :  an array of `time_window` objects describing valid slots for break start.
  - `service` (integer) : break duration (defaults to 0).
  - `description` (string) : a string describing this break.
- `max_tasks` (integer): Defines the maximum number of tasks in a route for this vehicle.
- `max_travel_time` (integer): Defines the maximum travel time for this vehicle.
  
Note: An error will be reported if two `break` objects have the same `id` for the same vehicle.


## Jobs

**Bold** ones are mandatory; *italic* ones are optional parameters.

It is assumed that all delivery-related amounts for jobs are loaded at vehicle start, while all pickup-related amounts for jobs are brought back at vehicle end.

A `job` object has the following properties:

- **`id`** (integer) : Unique id assigned to job.
- *`description`* (string) : A string describing this job.
- **`location`** (array) : Coordinates array of job location.
- *`service`* (integer) : job service duration (defaults to 0).
- **`delivery`** (integer) : An array of integers describing multidimensional quantities for delivery.
- **`pickup`** (integer) : An array of integers describing multidimensional quantities for pickup. 
- *`skills`* (integer) :  An array of integers defining mandatory skills.
- *`priority`* (integer) : An integer in the `[0, 100]` range describing priority level (defaults to 0).
- *`time_windows`* (array) : An array of `time_window` objects describing valid slots for job service start.   
Note: An error is reported if two `job` objects have the same `id`.

## Shipments
**Bold** ones are mandatory; *italic* ones are optional parameters.

A `shipments` object has the following properties:

1. **`pickup`**(object):  object describing pickup shipments step.
    - **`id`**(integer): unique ID of the shipments step.
    - *`description`*(string): a string describing this step
    - **`location`**(array): coordinate pair [lon,lat]
    - *`setup`*(integer): task setup duration (defaults to 0)
    - *`service`*(intger): task service duration (defaults to 0)
    - *`time_windows`*(array): an array of `time_window` objects describing valid slots for task service start
2. **`delivery`**(object):  object describing delivery shipments step.
    - **`id`**(integer): unique ID of the shipments step.
    - *`description`*(string): a string describing this step
    - **`location`**(array): coordinate pair [lon,lat]
    - *`setup`*(integer): task setup duration (defaults to 0)
    - *`service`*(intger): task service duration (defaults to 0)
    - *`time_windows`*(array): an array of `time_window` objects describing valid slots for task service start
3. *`amount`*(array): an array of integers describing multidimensional quantities
4. *`skills`*(array): an array of integers defining mandatory skills
5. *`priority`*(integer): an integer in the `[0, 100]` range describing priority level (defaults to 0)

### 3.A shipments Step

A `shipments_step` is similar to a `job` object (expect for shared keys already present in `shipments`)
An error is reported if two `delivery` (or `pickup`) objects have the same `id`.

## Notes

- It is assumed that all delivery-related amounts for jobs are loaded at vehicle start, while all pickup-related amounts for jobs are brought back at vehicle end.
- An error is reported if two `job` objects have the same `id`.
- the expected order for all coordinates arrays is `[lon, lat]`
- all timings are in seconds(except "computing_times" whose output is in miliseconds)
- all distances are in meters
- `waiting_time` is calcaulated on the earliness factor, It means if a vehicle has arrived before the time_window of the job to be performed then the wait between the arrival time(of vehicle) and the start time (in time_window) of the job is `waiting_time`.
- `cost` values in output are the one used in the optimization objective (currently equivalent to duration).
- key `start` and end are optional for a vehicle, as long as at least one of them is present.
- if `end` is omitted, the resulting route will stop at the last visited task, whose choice is determined by the optimization process.
- if `start` is omitted, the resulting route will start at the first visited task, whose choice is determined by the optimization process.
- to request a round trip, just specify both `start` and `end` with the same coordinates.


### Capacity restrictions

Those arrays can be used to model custom restrictions
for several metrics at once, e.g. number of items, weight, volume
etc. A vehicle is only allowed to serve a set of tasks if the
resulting load at each route step is lower than the matching value in
`capacity` for each metric. When using multiple components for
quantity, it is recommended to put the most important/limiting metric
first.


### Skills

Use `skills` to describe a problem where not all tasks can be served
by all vehicles. Job skills are mandatory, i.e. a job can only be
served by a vehicle that has **all** its required skills. In other
words: job `j` is eligible to vehicle `v`, iff, `j`'s `skills` is included
in `v`'s `skills`.

In order to ease modeling problems with no skills required, it is
assumed that there is no restriction at all if no `skills` keys are
provided.

### Task priorities

Useful in situations where not all tasks can be performed, to gain
some control on which tasks are unassigned. Setting a high `priority`
value for some tasks will tend as much as possible to have them
included in the solution over lower-priority tasks.

### Time windows

- **absolute values**, "real" timestamps. In case all times reported in output with the `arrival` key can be interpreted as timestamps.

The absence of a time window in input means no timing constraint
applies. In particular, a vehicle with no `time_window` key will be
able to serve any number of tasks, and a task with no `time_windows`
key might be included at any time in any route, to the extent
permitted by other constraints such as skills, capacity and other
vehicles/tasks time windows.
- In vehicles: time_window is the working hours in which jobs can be performed.
- In break(part of "vehicles"): time_window is an array describing valid slot(s) for break start. It means break must start between the given time_window but duration can exceed the endtime given in time_window.


## HTTPS Method
POST

## Security Type
This APIs follow OAuth2 based security. **To know more on how to create your authorization tokens, please use our authorization token URL. More details available**  [here](https://developer.mappls.com/mapping/tokenGeneration)

## Request Headers

The API leverages OAuth 2.0 based security. Hence, the developer would need to send a request for access token using their client_id and client_secret to the OAuth API. Once validated from the OAuth API, the access_token and the token_type need to be sent as Authorization header with the value: “{token_type} {access_token}”.

-  `Authorization:  “token_type access_token”`

## Response Type

`application/json`
<br>

## Request Parameters
The request parameters should go in the body in JSON format.
The “bold” one’s are mandatory, and the “italic” one’s are optional.

1. **`Vehicles`** - the array of available vehicles with related attributes. <br>Below are the vehicle attributes that one can pass:
    - **`id (integer)`** - custom ID of the vehicle (example: 1).
    - **`profile (string)`** - the type of vehicle that will be used in the route traveling. Routing profile includes "driving", "biking" & "trucking" (defaults to driving). Only needed as input in the first vehicle, for the remaining vehicles same profile will be used. (Currently mixed profiles are not supported).s
    - `description (string)` - the basic description of the available vehicle (Example: Tata Ace - DL143T3178).
    - **`start (number)`** - List of start locations with array of coordinates for the vehicles (Example: List [ 77.523442, 12.969504 ]).
    - **`end (number)`** - List of end locations with array of coordinates for the vehicles (Example: List [ 77.523442, 12.969504 ]).
    - `capacity (integer)` - describing the multi dimensional capacity or load quantities of the vehicles. The input should be list of integer values (Example: "capacity":[50,10,10]).
    - `skills (integer)` - list of especialised skill required to complete the assigned job described with integer values (Example: List [ 1, 2 ])
    - `time_window (integer)` - time interval during which task must take place. The input should be list of epoch values.
    - `break` - the array of break objects (i.e. lunch break or tea break)
      * `id (integer)` - custom ID of the break (example: 2).
      * `time_window (integer)` - time interval of break describing valid slots for break start. Break duration can surpass the endtime given in time_window.
      * `service (integer)` - duration of breaks (Example: 300)
      * `description (string)` - describing the break (Example: lunch break)

2. **`Jobs`** - The Jobs can be described as pick up and drop locations to perform certain tasks at given time.
    - `id (integer)` - Custom id of the assigned job (Example: 1)
    - `description (string)` - gives description of the job (Example: Replace hardware).
    - `location (number)` - array of coordinates of pick up or delivery locations (Example: List[77.523442, 12.969504]).
    - `delivery (integer) ` - describing single or multi dimensional quantities for delivery in the array of integer values (Example: [10,10,5]).
    - `pickup (integer) ` - describing single or multi dimensional quantities for pickup in the array of integer values (Example: [5,7,4]).
    - `skills (integer) ` - an array of integers defining mandatory skills required in vehicle for the orders (Example: List[1,2]).
    - `priority (integer)` - set the priority level of the job with range values from 100 to 0. Default priority is 0 being highest and 100 being lowest priority (Example: [10,30,10,5,2])
    - `time_window (integer)` - an array of assigned time slots for each job's service start (Example: List [1611043200, 1611082800]) .
    - `service (integer)` - the service time to perform a task in seconds unit.
3. **`Shipments`** - A `shipments` object has the following properties:
    - `pickup`(object):  object describing pickup shipments step.
        - `id`(integer): unique ID of the shipments step.
        - `description`(string): a string describing this step
        - `location`(array): coordinate pair [lon,lat]
        - `setup`(integer): task setup duration (defaults to 0)
        - `service`(intger): task service duration (defaults to 0)
        - `time_windows`(array): an array of `time_window` objects describing valid slots for task service start
    - `delivery`(object):  object describing delivery shipments step.
        - `id`(integer): unique ID of the shipments step.
        - `description`(string): a string describing this step
        - `location`(array): coordinate pair [lon,lat]
        - `setup`(integer): task setup duration (defaults to 0)
        - `service`(intger): task service duration (defaults to 0)
        - `time_windows`(array): an array of `time_window` objects describing valid slots for task service start
    - `amount`(array): an array of integers describing multidimensional quantities
    - `skills`(array): an array of integers defining mandatory skills
    - `priority`(integer): an integer in the `[0, 100]` range describing priority level (defaults to 0)


## Response Parameters
1. `msg (string)` - the response message of the request (Example: Request Submitted Successfully!).
2. `code (integer)` - the response code of the request (Example: 200).
3. `requestId (string)` - unique Id for submitted request (Example: de05643d-b484-11eb-ad11-532fdcf7908f)

## Response Codes
### Success

1. 200: To denote a successful data submission.

### Client-Side Issues

2.	400: Bad Request, User made an error while creating a valid request.
3.	401: Unauthorized, Developer’s key is not allowed to send a request.
4.	403: Forbidden, Developer’s key has hit its daily/hourly limit.
5.  409: Conflict.
6.  412: Preconditioned failed.

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
```js
curl --location --request POST 'https://apis.mappls.com/advancedmaps/vrp/v1/postOptimizationRequest' \
--header 'token: 9bxxxxxx-xx1c-4xxx-xxx6-xxxxd54dxxxf' \
--header 'Content-Type: application/json' \
--data-raw '{
    "vehicles": [
        {
            "id": 1,
            "start": [
                77.26894638016765,
                28.550833533042766
            ],
            "end": [
                77.26894638016765,
                28.550833533042766
            ],
            "capacity": [
                4
            ],
            "skills": [
                1,
                14
            ],
            "time_window": [
                1600416000,
                1600430400
            ]
        },
        {
            "id": 2,
            "start": [
                77.26894638016765,
                28.550833533042766
            ],
            "end": [
                77.26894638016765,
                28.550833533042766
            ],
            "capacity": [
                4
            ],
            "skills": [
                2,
                14
            ],
            "time_window": [
                1600416000,
                1600430400
            ],
            "breaks": [
                {
                    "id": 2,
                    "service": 300,
                    "time_windows": [
                        [
                            1600423200,
                            1600425000
                        ]
                    ]
                }
            ]
        }
    ],
    "jobs": [
        {
            "id": 1,
            "service": 300,
            "delivery": [
                1
            ],
            "location": [
                77.25014802489044,
                28.56370655591404
            ],
            "skills": [
                1
            ],
            "time_windows": [
                [
                    1600419600,
                    1600423200
                ]
            ]
        },
        {
            "id": 2,
            "service": 300,
            "pickup": [
                1
            ],
            "location": [
                77.13402954533225,
                28.687340657215927
            ],
            "skills": [
                1
            ]
        },
        {
            "id": 5,
            "service": 300,
            "delivery": [
                1
            ],
            "location": [
                77.25046301534559,
                28.672778729085678
            ],
            "skills": [
                14
            ]
        },
        {
            "id": 6,
            "service": 300,
            "delivery": [
                1
            ],
            "location": [
                77.20054141166888,
                28.563214295078236
            ],
            "skills": [
                14
            ]
        }
    ]
}'

```
### Sample Output(JSON)
``` json
{
  "msg": "Request Submitted Successfully!",
  "code": 200,
  "requestId": "a3bfb6dd8ae8a29fa537053d42eef977"
}
```

## Disclaimer
1. This API is released for select use cases only; Please contact Mappls API Support or your account manager for discussions on usage of this solution. 
2. Mappls reserves the right to revoke access of this API at its own discrection.


## Document Version History

| Version | Last Updated | Author |
| ---- | ---- | ---- |
| 0.0.1 | November 2021 | Mappls API Team ([KB](https://github.com/kunalbharti)) |
| 0.0.2 | March 2022 | Mappls API Team ([KB](https://github.com/kunalbharti)) |
| 0.0.3 | Feb 2024 | Mappls API Team ([KB](https://github.com/kunalbharti)) |

## API Version History

| Version | Last Updated | Author | Revised Sections |
| ---- | ---- | ---- | ---- |
| 0.1 | 2021-06-17 | Mappls API Team ([PS](https://github.com/map-123)) | Initial release |
| 0.2 | 2022-03-29 | Mappls API Team ([PS](https://github.com/map-123)) | shipments introduced |

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
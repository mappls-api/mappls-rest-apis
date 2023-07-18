[<img src="https://about.mappls.com/about/images/MAPPLS-MapmyIndia-logo.png" height="40"/> </p>](https://about.mappls.com/api/)

# Route Optimization APIs

## Introduction
The Goal in route optimization (Job Assignment & Route Optimization) is to get an optimal set of routes for a fleet of vehicles to traverse in order to deliver to a given set of customers. It generalizes the well-known travelling salesman problem (TSP). 

The objective of this API is to minimize the duration, determine and minimize vehicles used & optimize the distance travelled(optimized route), so it can reduce the overall cost and provide maximum profit.

<img src="https://about.mappls.com/api/optimisation/images/cost-efficient-route.gif?raw=true" style="margin-left:auto;margin-right:auto"/>


## Constraints
### vehicles
- Number of Vehicles
- Profile
- Vehicle Capacity
- Break Time
- Skills
- Time Window
### jobs
- Time Window
- Service Time
- Delivery/Pickup Capacity
- Skills
- Priority
### shipments
- Time Window
- Service Time
- setup time
- Delivery/Pickup Capacity
- Skills
- Priority



## Route Optimization Variants
- **Travelling Salesman Problem(TSP)** - This is basically Route Via point Optimization.  

- **Capacitated Route Optimization** - The vehicles have a limited carrying capacity of the goods that must be delivered. It can be single or multi quantity dimensions(e.g. volume, weight, number of packets etc.)
  <img src="https://about.mappls.com/api/optimisation/images/carrying_capacity.gif?raw=true" style="margin-left:auto;margin-right:auto"/>

- **Route Optimization with Time Windows** - The delivery locations have time windows within which the deliveries (or visits) must be made.

  <img src="https://about.mappls.com/api/optimisation/images/time_window.jpg?raw=true" style="margin-left:auto;margin-right:auto"/>

- **Route Optimization with Profits/Priority** - A maximization problem where it is not mandatory to visit all customers. The aim is to visit once customers maximizing the sum of collected profits while respecting a vehicle time limit. Vehicles are required to start and end at the depot.

  <img src="https://about.mappls.com/api/optimisation/images/profitability_priority.jpg?raw=true" style="margin-left:auto;margin-right:auto"/>

- **Route Optimization with Skill Sets** - List of vehicle skill(s). A delivery/pickup can only be served by the vehicle if its required skills is a subset of vehicle skills.

  <img src="https://about.mappls.com/api/optimisation/images/certain_jobs_1.gif?raw=true" style="margin-left:auto;margin-right:auto"/>

# Input

Format: JSON


| Key         | Description |
|-----------|-----------|
| [`vehicles`](#vehicles) |  array of `vehicle` objects describing the available vehicles |
| [`jobs`](#jobs) |  array of `job` objects describing the places to visit |
| [`shipments`](#shipments)|an array of `shipments` objects describing pickup and delivery tasks|

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
- all timings are in seconds(except "computing_times" in output is in miliseconds)
- all distances are in meters
- `waiting_time` is calculated on the earliness factor, It means if a vehicle has arrived before the time_window of the job to be performed then the wait between the start time (in time_window) and arrival time(of vehicle) is `waiting_time`.
- `cost` values in output are the one used in the optimization objective (currently equal to duration)
- key `start` and `end` are optional for a vehicle, as long as at least one of them is present
- if `end` is omitted, the resulting route will stop at the last visited task, whose choice is determined by the optimization process
- if `start` is omitted, the resulting route will start at the first visited task, whose choice is determined by the optimization process
- to request a round trip, just specify both `start` and `end` with the same coordinates

<br>

### Capacity restrictions

Those arrays can be used to model custom restrictions
for several metrics at once, e.g. number of items, weight, volume
etc. A vehicle is only allowed to serve a set of tasks if the
resulting load at each route step is lower than the matching value in
`capacity` for each metric. When using multiple components for
amounts, it is recommended to put the most important/limiting metrics
first.
<br>

### Skills

Use `skills` to describe a problem where not all tasks can be served
by all vehicles. Job skills are mandatory, i.e. a job can only be
served by a vehicle that has **all** its required skills. In other
words: job `j` is eligible to vehicle `v` iff `j.skills` is included
in `v.skills`.

In order to ease modeling problems with no skills required, it is
assumed that there is no restriction at all if no `skills` keys are
provided.
<br>

### Task priorities

Useful in situations where not all tasks can be performed, to gain
some control on which tasks are unassigned. Setting a high `priority`
value for some tasks will tend as much as possible to have them
included in the solution over lower-priority tasks.
<br> <br>

### Time windows

- **absolute values**, "real" timestamps. In that case all times reported in output with the `arrival` key can be interpreted as timestamps.

The absence of a time window in input means no timing constraint
applies. In particular, a vehicle with no `time_window` key will be
able to serve any number of tasks, and a task with no `time_windows`
key might be included at any time in any route, to the extent
permitted by other constraints such as skills, capacity and other
vehicles/tasks time windows.
- In vehicles: time_window is the working hours in which jobs can be performed.
- In break(part of "vehicles"): time_window is an array describing valid slot(s) for break start. It means break must start between the given time_window but duration can exceed the endtime given in time_window.
<br>

## Asynchronous API Call
At first input(vehicles & jobs) is given via `POST` Request which will provide a `requestID` which then needs to pass through a `GET` Request to get the status or the desired output of Route Optimization. So in this asynchronous call you do not halt all other operations while waiting for the API call to return.

The details of `POST` and `GET` request of the API are given in the separate documents.
<br>



## Output Description

Format: JSON


## response

The `response` object has the following properties:
| Key         | Description |
| ----------- | ----------- |
| [`summary`](#Summary) | object summarizing solution indicators | |
| [`routes`](#routes) | array of `route` objects |
| [`unassigned`](#unassigned) | array of `unassigned` objects |

<br>

**1. Summary**
-  `duration` : total traveled time for all routes. 
 - `delivery`:  total number of delivery points for all routes. 
   - `cost` : total cost for all routes.
-  `computing_times`: time in seconds taken for the output (for internal purposes only).
    - `routing`
    - `total` : sum of routing, solving and loading
    - `solving`
    - `loading`
- `distance`: Total calculated distance for all routes.
- `waiting_time` : Total waiting time for all routes.
- `service` : Total service time for all routes in seconds.
- `violation` :
- `pickup`: Total number of pickup for all routes.
   - `unassigned` : Number of tasks that could not be served.
  - `priority` : Total priority sum for all assigned tasks. 


 **2. Routes**
- `delivery`:  Total number of delivery points for tasks on this route.
 - `cost`: Cost for this route.
- `distance`: Total distance of this route. 
- `waiting_time` : Total waiting time for this route.
- `violations` :
- `description`: Vehicle description (if provided in input). 
- `pickup`: Total number of pickup tasks on this route. 
- `priority` : Sum of priority assigned for tasks on this route.
- `steps` : 
   - `duration` : Cumulative travel time upon arrival at this step.
   - `load`: Vehicle load after step completion (with capacity constraints). 
   - `distance` :  Traveled distance upon arrival at this step.
   - `waiting_time` : waiting time upon arrival at this step.
   - `arrival` : Estimated time of arrival at this step. 
   - `service` : Service time invested at this step. 
   - `description` step description (if provided in input). 
   - `location`: Coordinates array for this step (if provided in input).
   - `id`:  id of the task performed at this step, only provided when `type` value is given as `job`, `pickup`, `delivery` or `break` 
   - `type`:  a string (either `start`, `job`, `pickup`, `delivery`, `break` or `end`) 
   - `job`:
 - `vehicle` : id of the vehicle assigned on this route. 
  - `duration`: Total traveled time on this route.
  - `service` : Service time invested on this route. 
  - `geometry`: Encoded polyline route geometry of this route.

**3. Unassigned** : unassigned job,vehicle and shipment on this route
  - `location` - location of the vehicle/job/shipment whichever is unassigned
       - `id` - id of the unassigned job/vehicle/shipment 

<br>

![](https://about.mappls.com/api/optimisation/images/simplify_your_last_mile2.jpg)


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




<div align="center">@ Copyright 2022 CE Info Systems Ltd. All Rights Reserved.</div>

<div align="center"> <a href="https://www.mapmyindia.com/api/terms-&-conditions">Terms & Conditions</a> | <a href="https://www.mapmyindia.com/about/privacy-policy">Privacy Policy</a> | <a href="https://www.mapmyindia.com/pdf/mapmyIndia-sustainability-policy-healt-labour-rules-supplir-sustainability.pdf">Supplier Sustainability Policy</a> | <a href="https://www.mapmyindia.com/pdf/Health-Safety-Management.pdf">Health & Safety Policy</a> | <a href="https://www.mapmyindia.com/pdf/Environment-Sustainability-Policy-CSR-Report.pdf">Environmental Policy & CSR Report</a>

<div align="center">Customer Care: +91-9999333223</div>
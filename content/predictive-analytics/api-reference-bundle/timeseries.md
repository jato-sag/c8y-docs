---
title: Time series
layout: redirect
weight: 30
---

Operations for time series data/model.

>**Info**: An active subscription of Nyoka microservice is required to leverage the time series API.

### Domain Model
#### TimeSeries
|Name|Type|Description|
|:-----|:-----|:-----|
|series|array|The time series data specified as an array of values representing multiple observations.|
|observationInterval|TimePeriod|The time interval between consecutive observations.|
|startDate|DateTime|The timestamp of the first observation in UTC format.|
|seasonality|TimePeriod|Optional parameter to specify the seasonal period in the data, if present.|

#### TimePeriod
|Name|Type|Description|
|:-----|:-----|:-----|
|timeUnit|ChronoUnit|The value has to be a valid [ChronoUnit](https://docs.oracle.com/javase/8/docs/api/java/time/temporal/ChronoUnit.html) – “SECONDS”, “MINUTES”, “HOURS”, “DAYS”, “MONTHS”, “YEARS” etc.|
|periodLength|Number|Length of the period.|


### POST – Generate time series model using time series data

```
{{url}}/service/zementis/timeseries
```

Upload the time series data to generate a model. This is an asynchronous call which returns a status URL that can be used to check the status of model creation.

|HEADERS||
|:---|:---|
|Authorization|{{auth}}
|Content-Type|required header parameter with value application/json


**BODY**
```
{
    "series": [<value1>, <value2>, ...., <valueN>],
    "observationInterval": {
       "timeUnit": "<timeUnit>",
        "periodLength": <periodLength>
    },
    "startDate": "<startDate>",
    "seasonality": {
        "timeUnit": "<timeUnit>",
        "periodLength": <periodLength>
    }
}
```

**Example Request**

```
200 - OK

curl --request POST “{{url}}/service/zementis/timeseries” --header “Authorization: {{auth}}” \
	--header “Content-Type: application/json”

{
    "series": [
       112, 118, 132, 129, 121, 135, 148, 148, 136, 119, 104, 118, 115,
       126, 141, 135, 125, 149, 170, 170, 158, 133, 114, 140, 145, 150,
       178, 163, 172, 178, 199, 199, 184, 162, 146, 166, 171, 180, 193,
       181, 183, 218, 230, 242, 209, 191, 172, 194, 196, 196, 236, 235,
       229, 243, 264, 272, 237, 211, 180, 201, 204, 188, 235, 227, 234,
       264, 302, 293, 259, 229, 203, 229, 242, 233, 267, 269, 270, 315,
       364, 347, 312, 274, 237, 278, 284, 277, 317, 313, 318, 374, 413,
       405, 355, 306, 271, 306, 315, 301, 356, 348, 355, 422, 465, 467,
       404, 347, 305, 336, 340, 318, 362, 348, 363, 435, 491, 505, 404,
       359, 310, 337, 360, 342, 406, 396, 420, 472, 548, 559, 463, 407,
       362, 405, 417, 391, 419, 461, 472, 535, 622, 606, 508, 461, 390,
       432
    ],
    "observationInterval": {
       "timeUnit": "MONTHS",
       "periodLength": 1
    },
    "startDate": "2019-01-01T00:00:00+05:30",
    "seasonality": {
        "timeUnit": "YEARS",
        "periodLength": 1
    }
}
```

**Example Response**

```
200 - OK 

{
	“modelName”: “TimeSeries_11-12-2019_11-03-33”,
	“statusUrl”: "/service/zementis/timeseries/TimeSeries_11-12-2019_11-03-33/status"
}
```


**Example Request**

```
400 - Bad Request

curl --request POST “{{url}}/service/zementis/timeseries” --header “Authorization: {{auth}}” \
	--header “Content-Type: application/json”

{
    "series": [
       112, 118, 132, 129, 121, 135, 148, 148, 136, 119, 104, 118, 115,
       126, 141, 135, 125, 149, 170, 170, 158, 133, 114, 140, 145, 150,
       178, 163, 172, 178, 199, 199, 184, 162, 146, 166, 171, 180, 193,
       181, 183, 218, 230, 242, 209, 191, 172, 194, 196, 196, 236, 235,
       229, 243, 264, 272, 237, 211, 180, 201, 204, 188, 235, 227, 234,
       264, 302, 293, 259, 229, 203, 229, 242, 233, 267, 269, 270, 315,
       364, 347, 312, 274, 237, 278, 284, 277, 317, 313, 318, 374, 413,
       405, 355, 306, 271, 306, 315, 301, 356, 348, 355, 422, 465, 467,
       404, 347, 305, 336, 340, 318, 362, 348, 363, 435, 491, 505, 404,
       359, 310, 337, 360, 342, 406, 396, 420, 472, 548, 559, 463, 407,
       362, 405, 417, 391, 419, 461, 472, 535, 622, 606, 508, 461, 390,
       432
    ],
    "observationInterval": {
       "timeUnit": "MONTHS",
       "periodLength": 1
    },
    "startDate": "2019-01-01T00:00:00+05:3012",
    "seasonality": {
        "timeUnit": "YEARS",
        "periodLength": 1
    }
}
```
  
**Example Response**

```
400 - Bad Request

{
    "errors": [
        "Invalid start date. Provide start date in yyyy-MM-dd'T'HH:mm:ss.SSSXXX format"
    ]
}
```

**Example Request**

```
401 - Unauthorized

curl --request POST “{{url}}/service/zementis/timeseries” --header “Content-Type: application/json”
```
     
**Example Response**

```
401 - Unauthorized

{
    "error": "general/internalError",
    "message": "No auth information found",
    "info": "https://www.cumulocity.com/reference-guide/#error_reporting"
}
```

**Example Request**

```
500 - Internal Server Error

curl --request POST “{{url}}/service/zementis/timeseries” --header “Authorization: {{auth}}” \
	--header “Content-Type: application/json”

{
    "series": [
       112, 118, 132, 129, 121, 135, 148, 148, 136, 119, 104, 118, 115,
       126, 141, 135, 125, 149, 170, 170, 158, 133, 114, 140, 145, 150,
       178, 163, 172, 178, 199, 199, 184, 162, 146, 166, 171, 180, 193,
       181, 183, 218, 230, 242, 209, 191, 172, 194, 196, 196, 236, 235,
       229, 243, 264, 272, 237, 211, 180, 201, 204, 188, 235, 227, 234,
       264, 302, 293, 259, 229, 203, 229, 242, 233, 267, 269, 270, 315,
       364, 347, 312, 274, 237, 278, 284, 277, 317, 313, 318, 374, 413,
       405, 355, 306, 271, 306, 315, 301, 356, 348, 355, 422, 465, 467,
       404, 347, 305, 336, 340, 318, 362, 348, 363, 435, 491, 505, 404,
       359, 310, 337, 360, 342, 406, 396, 420, 472, 548, 559, 463, 407,
       362, 405, 417, 391, 419, 461, 472, 535, 622, 606, 508, 461, 390,
       432
    ],
    "observationInterval": {
       "timeUnit": "MONTHS",
       "periodLength": 1
    },
    "startDate": "2019-01-01T00:00:00+05:30",
    "seasonality": {
        "timeUnit": "YEARS",
        "periodLength": 1
    }
}
```

**Example Response**

```
500 - Internal Server Error

{
    "errors": [
        "Nyoka microservice is unsubscribed. Subscribe to Nyoka microservice to upload timeseries model."
    ]
}
```


### GET – Get status of generated time series model

```
{{url}}/service/zementis/timeseries
```

Get the status of the generation of a specific time series model. The status can either be IN_PROGRESS, SUCCESS or FAILURE.<br>
If the status is FAILURE, the `errorMessage` attribute in the response holds the reason for the failure.

|HEADERS||
|:---|:---|
|Authorization|{{auth}}

|PARAMS||
|:---|:---|
|model_name (string)|required path variable for time series model name


**Example Request**

```
200 - OK 

curl --request GET “{{url}}/service/zementis/timeseries/TimeSeries_11-12-2019_11-03-33/status” --header “Authorization: {{auth}}”
```

**Example Response**

```
200 - OK

{
    "status": "IN_PROGRESS",
    "errorMessage": "null"
}
```

**Example Request**

```
401 – Unauthorized

curl --request GET “{{url}}/service/zementis/timeseries/TimeSeries_11-12-2019_11-03-33/status” 
```

**Example Response**

```
401 - Unauthorized

{
    "error": "general/internalError",
    "message": "No auth information found",
    "info": "https://cumulocity.com/reference/rest-implementation/#error_reporting"
}
```

**Example Request**

```
404 – Not Found

curl --request GET “{{url}}/service/zementis/timeseries/dummy/status” --header “Authorization: {{auth}}”
```

**Example Response**

```
404 – Not Found

{
    "errors": [
        "Model 'dummy' not found."
    ]
}
```

**Example Request**

```
500 – Internal Server Error

curl --request GET “{{url}}/service/zementis/timeseries/TimeSeries_11-11-2019_11-22-33/status” --header “Authorization: {{auth}}”
```

**Example Response**

```
500 – Internal Server Error

{
    "errors": [
        "Model generation failed, try again"
    ]
}
```
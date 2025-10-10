<!-- This document is an example of how I have written API reference guides in previous roles. The API and endpoints described in this topic are fictional, but the style and structure are the same as I have written professionally. -->

# SCADA API Reference Guide

The SCADA API allows users to retrieve data from any Remote Terminal Uplink (RTU) conected to the SCADA network, enabling personnel to query and maintain devices in the field.

You can access the SCADA API using a REST API GUI client such as **Postman** or using a command-line interface like cURL.

All RTUs are contained within a closed network and cannot be accessed by outside devices. Please contact your supervisor if you need to add a new device to the network.

### Prerequisites

- You will require your employee credentials to authenticate with the SCADA API.
- You can only make calls to the SCADA API using an approved device. Calls from non-approved devices will automatically fail.
- You will require the network ID of each RTU you wish to query.

### Base URI

`https://<rtuid>/rest/v1/<endpoint>`

### Authentication

The SCADA API uses the **Basic Auth** as the authentication method. Provide your full name, without spaces, as the 'username' and use your employee ID as the 'password'. For example:

- Username: `johnsmith`
- Password: `1234567ABC`

### Error Response Codes

All errors are returned in the following format:

```
{
    "error": {
        "failure": 403,
        "message": "Access Denied"
    }
}
```

## Endpoints

### GET/Status

Returns the current status of the RTU.

`<rtuid>/rest/v1/status`

Parameters:

|Name|Type|Required|Description|
|---|---|---|---|
|`<rtuid>`|string|yes|The ID of the RTU.|

Response:

A successful response will return a status code in the following format:

```
{
    "status": 01
}
```

|Code|Description|
|---|---|
|00|Device offline|
|01|Device online|
|02|Device requires restart|

### GET/Temperature

Returns temperature data for the pipeline the RTU is assigned to.

`<rtuid>/rest/v1/temp/<days>/<units>`

**Parameters**

|Name|Type|Required|Description|
|---|---|---|---|
|`<rtuid>`|string|yes|The ID of the RTU.|
|`<days>`|int|yes|Specify the required time period of the results you need in days, from 01 to 28. The present day is always 01.|
|`<units>`|string|yes|Specify the units for the temperature data. C, for Celcius, F for Farenheit.|

**Response:**

A successful response will return temperature data in the following format:

```
{
  "daysCount": 5,
  "days": [
    {
      "date": "2024-06-01",
      "temperature": 60,
      "units": "C"
    },
    {
      "date": "2024-06-02",
      "temperature": 59,
      "units": "C"
    },
    {
      "date": "2024-06-03",
      "temperature": 61,
      "units": "C"
    },
    {
      "date": "2024-06-04",
      "temperature": 89,
      "units": "C"
    },
    {
      "date": "2024-06-05",
      "temperature": 60,
      "units": "C"
    }
  ]
}
```

### GET/Flow

Returns pressure, velocity, and flow rate data for the pipeline the RTU is assigned to. You can request additional properties of pressure and velocity.

`<rtuid>/rest/v1/<days>/flow/<press>/<vel>/`

**Parameters**

|Name|Type|Required|Description|
|---|---|---|---|
|`<rtuid>`|string|yes|The ID of the RTU.|
|`<days>`|int|yes|Specify the required time period of the results you need in days, from 01 to 28. Default: 01.|
|`<press>`|string|no|Enter "press" to return pressure data. Values are Bars.|
|`<vel>`|string|no|Enter "vel" to return velocity data. Values are m/s.|

**Response:**

A successful response will return data in the following format:

```
{
  "daysCount": 2,
  "days": [
    {
      "date": "2024-06-01",
      "pressure": 1.2,
      "velocity": 2
    },
    {
      "date": "2024-06-02",
      "pressure": 1.1,
      "velocity": 1.7
    }
  ]
}
```
### POST/Restart

A request that instructs the RTU to restart and returns a status code.

`<rtuid>/rest/v1/restart`

**Response**

A successful response will return data in the following format:

```
{
    "restart": 01
}
```

|Code|Description|
|---|---|
|00|Restart failed|
|01|Restart successful|
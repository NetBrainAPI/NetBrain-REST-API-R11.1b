
# Network Setting API Design

## ***GET*** /V1/CMDB/NetworkSettings/Devices
Call this API to get devices by a Network Setting. 

## Detail Information

> **Title** : Get Devices of a Network Setting API<br>

> **Version** : 03/16/2023.

> **API Server URL** : http(s)://IP address of NetBrain Web API Server/ServicesAPI/API/V1/CMDB/NetworkSettings/Devices

> **Authentication** : 

|**Type**|**In**|**Name**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|Bearer Authentication| Headers | Authentication token | 

## Headers

> **Data Format Headers**

|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
| Content-Type | string  | support "application/json" |
| Accept | string  | support "application/json" |

> **Authorization Headers**

|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
| token | string  | Authentication token, get from login API. |


## Parameters (****required***)
|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|alias*|string|The alias name of telnet/SSH login credentials. |
|limit|integer|The up limit amount of device records to return per API call. The "limit" value valid range is 10 - 100, if the assigned value exceeds the range, the server will respond error message "Parameter 'limit' must be greater than or equal to 10 and less than or equal to 100." The value can not be negative. If the value is negative, API throws exception {"statusCode":791001,"statusDescription":"Parameter 'limit' cannot be negative"}.|
|index|integer|The index number is used to indicate the last record was scanned in DB from the last API call. The value of this parameter is last API call returned index number plus 1. For exmpale, the last call returend index is 1000, then provide parameter value as 1001 to avoid duplicate record compare with the last API call. This is a required parameter if amount of records need to be skipped. The value can not be negative. If the value is negative, API throws exception {"statusCode":791001,"statusDescription":"Parameter 'index' cannot be negative"}.|
|||limit and index parameters are based on the search result from DB. If both limit and index are not provided, return the device list with 50 devices start from the first device result in DB. If only provide limit value, return from the first device result in DB. If only provide index value, return the device list with 50 devices start from the index number.  If provided both limit and index, return as required. Error exceptions follow each parameter's description.|

## Response

|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|devices | array  | A list of devices with hostname |
|index | integer  | The index number indicate the last record is scanned in DB from the current API call |
|statusCode| integer | Code issued by NetBrain server indicating the execution result.  |
|statusDescription| string | The explanation of the status code. |

## Response Codes 
|**Code**|**Message**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|790200|ok| Success |
|793404|NotFound|Not found |
|791001|NotFound|Parameter 'limit' cannot be negative|
|791001|NotFound|Parameter 'index' cannot be negative.|
|791001|NotFound|Parameter 'limit' must be greater than or equal to 10 and less than or equal to 100.|


> ***Example***

```python
{
    "devices"[US-BOS-R1, US-BOS-R2, US-BOS-R3, US-BOS-R4],
    'statusCode': 790200, 
    'statusDescription': 'Success.'
}
```

# Full Example:
    

# cURL Code from Postman


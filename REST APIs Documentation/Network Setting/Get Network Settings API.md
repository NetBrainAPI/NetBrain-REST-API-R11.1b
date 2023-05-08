
# Network Setting API Design

## ***GET*** /V1/CMDB/NetworkSettings
Call this API to get network settings Telnet/SSH information. 

## Detail Information

> **Title** : Get Network Settings API<br>

> **Version** : 02/24/2023.

> **API Server URL** : http(s)://IP address of NetBrain Web API Server/ServicesAPI/API/V1/CMDB/NetworkSettings/{type}

> **Authentication** : 

|**Type**|**In**|**Name**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|Bearer Authentication| Headers | Authentication token | 

## Path Parameters(****required***)  
|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|type|string|The type of Network Settings:<br>telnetInfo |

## Parameters 
|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|alias|string|The alias name of telnet/SSH login credentials. |
|userName|string|The user name of the non-privilege login. |

> **Note** : If provided both of "alias" and "userName", userName has higher priority. 

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

## Response

|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|alias | string  | The alias name of telnet/SSH login credentials.  |
|userName | string  | The user name of the non-privilege login. |
|cliMode  | integer  | The authentication method. <br>options:<br>0, Telnet/SSH Password<br>2: SSH public key |
|keyName  | string  | The name of the SSH public key. This field is only available when the current cliMode is 2 in system. |
|deviceCount | integer  | The total number of devices that using the current credential. |
|statusCode| integer | Code issued by NetBrain server indicating the execution result.  |
|statusDescription| string | The explanation of the status code. |

## Response Codes 
|**Code**|**Message**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|790200|ok| Success |
|793404|NotFound|Not found |

> ***Example***

```python
{
    "telnetInfo"[
        {
            "alias":"Test1",
            "userName":"netbrain",
            "cliMode":2,
            "KeyName":"testKey",
            "deviceCount":25
        },
        {
            "alias":"Test2",
            "userName":"netbrain",
            "cliMode":0,
            "deviceCount":15
        }

    ]
    'statusCode': 790200, 
    'statusDescription': 'Success.'
}
```

# Full Example:
    

# cURL Code from Postman


# User API Design

## ***POST*** /V1/CMDB/Users
Call this API to synchronize customer AD/LDAP user accounts into NetBrain system.

## Detail Information

> **Title** : Synchronize with LADP/AD server users<br>

> **Version** : 01/08/2023.

> **API Server URL** : http(s)://IP address of NetBrain Web API Server/ServicesAPI/API/V1/CMDB/Users/SyncExternalUsers

> **Authentication** : 

|**Type**|**In**|**Name**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|Bearer Authentication| Headers | Authentication token | 

> **User Privilage Requirement:** user management


## Request body(****required***)

|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
| externalServerType  | list    | The authentication type for the user account. |
|            ***      |  ***    | ▪ 1 - AD     |
|            ***      |  ***    | ▪ 2 - LDAP   |

> ***Example***


```python
# sync AD and LDAP accounts
{
    "externalServerType": [1, 2]
}

# sync AD accounts only
{
    "externalServerType": [1]
}
```

## Parameters(****required***)

>No parameters required.

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
|statusCode| integer | The returned status code of executing the API.  |
|statusDescription| string | The explanation of the status code.  |

> ***Example***


```python
{
    'statusCode': 794011,
    'statusDescription': 'Operation failed. Reason: {0}'
}
```

# Full Example:


```python
# import python modules 
import requests
import time
import urllib3
import pprint
import json
urllib3.disable_warnings(urllib3.exceptions.InsecureRequestWarning)

# Set the request inputs
token = '684c4e42-833a-428d-a5c9-3f047f3d3a67'
nb_url = "http://192.168.28.79"
full_url = nb_url + "/ServicesAPI/API/V1/CMDB/Users/SyncExternalUsers"
headers = {'Content-Type': 'application/json', 'Accept': 'application/json'}
headers["Token"] = token

body = {
        "externalServerType": [1, 2]
        }

try:
    response = requests.post(full_url, data = json.dumps(body), headers = headers, verify = False)
    if response.status_code == 200:
        result = response.json()
        print (result)
    else:
        print ("Sync AD/LDAP Users failed! - " + str(response.text))

except Exception as e:
    print (str(e)) 

```

    {'statusCode': 790200, 'statusDescription': 'Success.'}
    

# cURL Code from Postman:


```python
curl --location 'https://nextgen-training.netbrain.com/ServicesAPI/API/V1/CMDB/Users/SyncExternalUsers' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'token: 684c4e42-833a-428d-a5c9-3f047f3d3a67' \
--data '{
    "externalServerType": [1, 2]
}'
```


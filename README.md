---
description: iWine API
---

# iWine

iWine device have web interface. Using http request available get information about iWine, change temperature and shake. All requests must have `Authorization` header with basic http authorization. User name is always `admin`. Password is PIN code typed on iWine bottom label.

For example for pin code 12345. 

```http
GET /getinfo HTTP/ 1.1
Authorization: Basic YWRtaW46MTIzNDU=
```

Returned results and post parameters encoded in `utf-8.`

{% api-method method="get" host="https://iwinehost" path="/getinfo/" %}
{% api-method-summary %}
Get wine info
{% endapi-method-summary %}

{% api-method-description %}
Gets iWine info.    
Returns JSON with information.   
In `volume` field returned integer in iWine wine volume in ml. If decanter is empty returned 0 . Maximum value depends from decanter model.   
In `shugar` field returned shugar concentration in grams to litre. Value is float number with one digit after point. Minimum value is 0.0 and maximum 2000.0. `temperature` field indicate current vine temperature. Minimum value is 0.0 maximum 100.0. If decanter is empty - temperature will show incorrect value.  
   
`color` color of wine. Can be "red", "white", "rose", "orange". Color measured by mashine learning and it reliability shown  by `color_reliability` field.  Color reliability can be from 0.00 \(no chance to be true\) to 1.00 \(absolutely true\). 
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Basic authorization string. Base64 encoded string with user name and password.  
User name is **admin** password is pincode typed on device bottom label.  
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Success info retreive. Return JSON object.  
{% endapi-method-response-example-description %}

```javascript
{
    "volume": "1200",
    "shugar": "5.0",
    "temerature": "17.5",
    "color":"red",
    "color_reliability":"0.90" 
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=401 %}
{% api-method-response-example-description %}
No authorization header or user name and pin incorrect.
{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="https://decanterhost" path="/setnewtemp/" %}
{% api-method-summary %}
 Set new temperature
{% endapi-method-summary %}

{% api-method-description %}
Set the new temperature for  decanter. On accept returns location to progress info.  If previous set request not completed and temp param equal to previous setting request returns prevoius progress location path, else previous location will be deleted and created new path. 
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
See "get wine info".
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-form-data-parameters %}
{% api-method-parameter name="temp" type="string" required=true %}
new temperature. Must be float with one digit after point precision. Value must be from "0.0" to "100.0". 
{% endapi-method-parameter %}
{% endapi-method-form-data-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=202 %}
{% api-method-response-example-description %}
Temperature set begins. In response returned path to progress of operation.
{% endapi-method-response-example-description %}

```
HTTP/1.1 202 Accepted
Location: /tempsetting<token>
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=400 %}
{% api-method-response-example-description %}
Request  data not contain **`temp`** parameter or it value incorrect. 
{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=401 %}
{% api-method-response-example-description %}
No authoriztion header or incorrent user or password.
{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=405 %}
{% api-method-response-example-description %}
iWine is empty and temperature change not available.
{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://decanterhost" path="/tempsetting<token>" %}
{% api-method-summary %}
Get the temperature set progress
{% endapi-method-summary %}

{% api-method-description %}
Returns progress of temperature change by `/setnewtemp`  request. 
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
See getinfo.
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Return JSON object with current and destination temperature.  
{% endapi-method-response-example-description %}

```
{
    "current": "12.0",
    "destination": "5.0",
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=401 %}
{% api-method-response-example-description %}
No authorization header. User name or password is incorrect. 
{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
Resource name with this name no more exists. This may be if temperature change request not started, or another temperature change request maked and this path deleted.
{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="https://decanterhost/" path="shake" %}
{% api-method-summary %}
Shake
{% endapi-method-summary %}

{% api-method-description %}
Starts shaking wine. 
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}

{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=202 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
HTTP/1.1 202 Accepted
Location: /shaking<token>
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=401 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=405 %}
{% api-method-response-example-description %}
iWine is empty and shaking not allowed.
{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}



{% api-method method="get" host="https://iwinehost" path="/shaking<token>" %}
{% api-method-summary %}
Get shaking progress
{% endapi-method-summary %}

{% api-method-description %}
Returns shaking progress.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="Authorization" type="string" required=true %}

{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Shaking in progress.
{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=302 %}
{% api-method-response-example-description %}
Shaking complete.
{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=401 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
Shaking never started or new shaking request started.
{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://iwinehost" path="/stop<token>" %}
{% api-method-summary %}
Stop process
{% endapi-method-summary %}

{% api-method-description %}
Stops shaking or temperature setting process.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}

{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Process with &lt;token&gt; stopped success.
{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=401 %}
{% api-method-response-example-description %}
No authorization or invalid user or password.
{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
No process with this token.
{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}


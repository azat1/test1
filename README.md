---
description: Vine decanter API
---

# Wine decanter

{% api-method method="get" host="https://decanterhost" path="/getinfo/:pass" %}
{% api-method-summary %}
Get wine info
{% endapi-method-summary %}

{% api-method-description %}
Gets decanter info.  Decanter measurements take a time - total approximately 100 ms. This is minimum response time.   
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="pass" type="string" required=true %}
Six digit pin code for device. Pin code is fixed and printed on decanter bottom. 
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Success info retreive.   
Returns JSON with decanter info.  
In `volume` field returned integer in decanter vine volume in ml. If decanter is empty returned `0`  . Maximum value depends from decanter model.  
In `shugar`  field returned shugar concentration in grams to litre. Value is float number with one digit after point. Minimum value is 0.0 and maximum 2000.0.  
`temperature` field indicate current vine temperature. Minimum value is 0.0 maximum 100.0. Temperature measuring take a time approx. 0.1 ms. I   
{% endapi-method-response-example-description %}

```javascript
{
    "volume": "1200",
    "shugar": "5.0",
    "temerature": "17.5",
    "color":"red",
    "color_reliability":"90" 
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=401 %}
{% api-method-response-example-description %}
Pin code is incorrect.
{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
Pin code not specified.
{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="put" host="https://api.vinegr.com" path="/setnewtemp/:pass/:temp" %}
{% api-method-summary %}
 Set new temperature
{% endapi-method-summary %}

{% api-method-description %}
Sets the new temperature for  decanter.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="pass" type="string" required=true %}
Pin code.
{% endapi-method-parameter %}

{% api-method-parameter name="temp" type="string" required=true %}
new temperature.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Temperature set ok.
{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=401 %}
{% api-method-response-example-description %}
Incorrent pin.
{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}


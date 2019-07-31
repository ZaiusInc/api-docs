# Objects

{% api-method method="post" host="https://api.zaius.com/v3" path="/objects/{object\_name}" %}
{% api-method-summary %}
Update Object
{% endapi-method-summary %}

{% api-method-description %}
Update an object \(e.g. Concert Tickets or Reviews\)
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="{object\_field}" type="string" required=false %}
any other field within the object that you wish to update associated with the primary key
{% endapi-method-parameter %}

{% api-method-parameter name="{primary\_key}" type="string" required=true %}
the primary key of the object
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=202 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "title": "Accepted",
  "status": 202,
  "timestamp": "2018-09-10T21:07:10-05:00"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=400 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "title": "Bad Request",
  "status": 400,
  "timestamp": "2018-09-10T21:07:10-05:00",
  "detail": {
    "invalids": [
      {
        "event": 0,
        "message": "Missing required field `product_id`"
      }
    ]
  }
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=403 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "message": "Forbidden"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% code-tabs %}
{% code-tabs-item title="Example Payload" %}
```javascript
[{
  "primary_key": "123",
  "field_example": true
},{
  "primary_key": "456",
  "field_example": false
}]
```
{% endcode-tabs-item %}
{% endcode-tabs %}


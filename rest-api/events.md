# Events

For examples of typical events and their associated fields, review the Zaius Event reference:

{% api-method method="post" host="https://api.zaius.com/v3" path="/events" %}
{% api-method-summary %}
Upload Event\(s\)
{% endapi-method-summary %}

{% api-method-description %}
Upload events to Zaius
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="type" type="string" required=true %}
the event type \(e.g. product\)
{% endapi-method-parameter %}

{% api-method-parameter name="action" type="string" required=true %}
the event action associated with the type \(e.g. add\_to\_cart\)
{% endapi-method-parameter %}

{% api-method-parameter name="identifiers" type="object" required=true %}
any known identifiers associated with the customer that performed the event
{% endapi-method-parameter %}

{% api-method-parameter name="data" type="object" required=false %}
any additional fields you want to include on the event \(e.g. product\_id\)
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
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
        "invalids": []
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
[
  {
    "type": "product",
    "action": "add_to_cart",
    "identifiers": {
      "email": "tyler@zaius.com"
    },
    "data": {
      "product_id": "123"
    }
  },
  {
    "type": "product",
    "action": "remove_from_cart",
    "identifiers": {
      "email": "tyler@zaius.com"
    },
    "data": {
      "product_id": "123"
    }
  }
]
```
{% endcode-tabs-item %}
{% endcode-tabs %}


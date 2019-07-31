# Orders

For more information about Orders in Zaius, please refer to our Orders reference:

{% api-method method="post" host="https://api.zaius.com/v3" path="/events" %}
{% api-method-summary %}
Order Purchase
{% endapi-method-summary %}

{% api-method-description %}
Upload an order purchase event to Zaius
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
    "type": "order",
    "action": "purchase",
    "identifiers": {
      "email": "bob@gmail.com"
    },
    "data": {
      "ts": 123456789, // (optional) the time of the order purchase
      "order": {
        "order_id": "OR345",
        "total": 109.65,
        "discount": 5.00,
        "subtotal": 103.00,
        "tax": 5.15,
        "shipping": 6.50,
        "coupon_code": "5OFF",
        "items": [
          {
            "product_id": "2045",
            "price": 19.00,
            "quantity": 5,
            "discount": 0.00,
            "subtotal": 95.00
          },
          {
            "product_id": "2091",
            "price": 10.00,
            "quantity": 1,
            "discount": 2.00,
            "subtotal": 8.00
          }
        ]
      }
    }
  }
]
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% api-method method="post" host="https://api.zaius.com/v3" path="/events" %}
{% api-method-summary %}
Order Return / Refund
{% endapi-method-summary %}

{% api-method-description %}
Upload an order purchase event to Zaius
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
    "type": "order",
    "action": "return", // or refund
    "identifiers": {
      "email": "bob@gmail.com",
    },
    "data": {
      "ts": 123456789, // (optional) the time of the order return | refund | cancel
      "order": {
        "order_id": "OR345",
        "total": -100.00
        "items": [
          {
            "product_id": "2045",
            "price": -10.00,
            "quantity": 10,
            "subtotal": -100.00
          }
        ]
      }
    }
  }
]
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% api-method method="post" host="https://api.zaius.com/v3" path="/events" %}
{% api-method-summary %}
Order Cancellation
{% endapi-method-summary %}

{% api-method-description %}
Upload an order purchase event to Zaius
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
    "type": "order",
    "action": "cancel", 
    "identifiers": {
      "email": "bob@gmail.com",
    },
    "data": {
      "ts": 123456789, // (optional) the time of the order return | refund | cancel
      "order": {
        "order_id": "OR345",
        "total": -100.00
        "items": [
          {
            "product_id": "2045",
            "price": -10.00,
            "quantity": 10,
            "subtotal": -100.00
          }
        ]
      }
    }
  }
]
```
{% endcode-tabs-item %}
{% endcode-tabs %}


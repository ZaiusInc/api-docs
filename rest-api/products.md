# Products

For additional information about Products within Zaius, please visit the Product reference.

{% api-method method="post" host="https://api.zaius.com/v3" path="/objects/products" %}
{% api-method-summary %}
Update Product\(s\)
{% endapi-method-summary %}

{% api-method-description %}
Update products with new metadata as your inventory updates
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="{product\_field}" type="string" required=false %}
any other product field. refer to the product reference above for the full list of available fields.
{% endapi-method-parameter %}

{% api-method-parameter name="product\_id" type="string" required=true %}
the product\_id associated with the product
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
  "product_id": "123",
  "name": "Red Shirt"
},{
  "product_id": "456",
  "name": "Blue Shirt"
}]
```
{% endcode-tabs-item %}
{% endcode-tabs %}


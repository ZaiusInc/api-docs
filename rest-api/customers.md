# Customers

{% api-method method="post" host="https://api.zaius.com/v3" path="/profiles" %}
{% api-method-summary %}
Create & Update Customer\(s\)
{% endapi-method-summary %}

{% api-method-description %}
Update the attributes and identifiers of a customer.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="attributes" type="object" required=true %}
Attributes like gender and first\_name associated with this customer.
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
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% code-tabs %}
{% code-tabs-item title="Example Payload" %}
```javascript
[{
    "attributes": {
      "first_name": "Johnny",
      "last_name": "Zaius",
      "email": "sample@test.com",
      "phone": "555-867-5309",
      "street1": "123 Fake St",
      "street2": "Apt 101",
      "city": "Boston",
      "state": "MA",
      "zip": "02101",
      "country": "USA",
      "timezone": "America/New_York",
      "gender": "M"
    }
  },
  {
    "attributes": {
      "first_name": "Jenny",
      "last_name": "Example",
      "email": "example@notreal.com",
      "phone": "555-555-5555",
      "street1": "456 Imaginary Ln",
      "city": "Leesburg",
      "state": "Virginia",
      "zip": "20175",
      "country": "United States",
      "timezone": "America/New_York",
      "gender": "F"
    }
}]
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% api-method method="get" host="https://api.zaius.com/v3" path="/profiles" %}
{% api-method-summary %}
Get Customer Information
{% endapi-method-summary %}

{% api-method-description %}
Get the attributes and identifiers associated with a customer.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-query-parameters %}
{% api-method-parameter name="example\_identifier" type="string" required=false %}
Replace this value with any valid identifier \(e.g. vuid\). If provided, email is not required as a query parameter.
{% endapi-method-parameter %}

{% api-method-parameter name="email" type="string" required=true %}
The name and value for any single identifier \(e.g. email, vuid, etc.\) 
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
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

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
    "title": "Accepted",
    "status": 202,
    "timestamp": "2018-09-10T21:07:10-05:00",
    "detail": {
        "message": "Unable to find profile for email = sample_bad@test.com"
    }
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% tabs %}
{% tab title="Example Request" %}
```bash
curl -iX GET \
'https://api.zaius.com/v3/profiles?email=sample@test.com' \
-H 'x-api-key: example.apiKey'
```
{% endtab %}
{% endtabs %}




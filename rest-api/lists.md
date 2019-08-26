# Lists

{% api-method method="get" host="https://api.zaius.com/v3" path="/lists/subscriptions?{identifier}={identifier\_value}" %}
{% api-method-summary %}
Get Subscription Status
{% endapi-method-summary %}

{% api-method-description %}
Get the subscription status of a customer identifier to a Zaius list.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-query-parameters %}
{% api-method-parameter name="{identifier}" type="string" required=true %}
The identifier type, for example "email".
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=202 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "customer": {
    "email": "sample@test.com"
  },
  "opted_in": true,
  "subscriptions": [
    {
      "name": "True List Name",
      "list_id": "sample_list",
      "subscribed": true
    }
  ]
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

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
    "title": "Not Found",
    "status": 404,
    "timestamp": "2018-09-10T21:07:10-05:00",
    "detail": {
        "message": "Customer with email sample@zaius.com was not found"
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
'https://api.zaius.com/v3/lists/subscriptions?email=sample@test.com' \
-H 'x-api-key: example.apiKey'
```
{% endtab %}
{% endtabs %}

{% api-method method="post" host="https://api.zaius.com/v3" path="/lists/subscriptions" %}
{% api-method-summary %}
Subscribe / Unsubscribe
{% endapi-method-summary %}

{% api-method-description %}
Subscribe or unsubscribe a customer identifier to or from a Zaius list.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="subscribed" type="boolean" required=false %}
whether or not the messaging identifier is subscribed or not to the list
{% endapi-method-parameter %}

{% api-method-parameter name="{identifier}" type="string" required=true %}
the messaging identifier to act upon \(e.g. email\)
{% endapi-method-parameter %}

{% api-method-parameter name="list\_id" type="string" required=true %}
the name of the list
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=202 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "updates": [
    {
      "list_id": "sample_list",
      "email": "sample@test.com",
      "subscribed": true
    }
  ]
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
  "title": "Not Found",
  "status": 404,
  "timestamp": "2018-09-10T21:07:10-05:00",
  "detail": {
    "message": "Customer with email sample@zaius.com was not found"
  }
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% code-tabs %}
{% code-tabs-item title="Example Payload" %}
```javascript
{
  "list_id": "sample_list",
  "email": "sample@test.com",
  "subscribed": false
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% api-method method="get" host="https://api.zaius.com/v3" path="/lists" %}
{% api-method-summary %}
Get Lists
{% endapi-method-summary %}

{% api-method-description %}
Get all lists associated with a Zaius account.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=202 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "lists": [
    {
      "name": "Example List",
      "created_at": "2018-09-10T21:07:10+00:00",
      "list_id": "example_list"
    },
    {
      "name": "Example List 2",
      "created_at": "2018-10-15T13:43:46+00:00",
      "list_id": "example_list_2"
    }
  ]
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=403 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
    "title": "Forbidden",
    "status": 403,
    "timestamp": "2018-09-10T21:07:10-05:00",
    "detail": {
        "message": "Insufficient privileges to access this resource."
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
'https://api.zaius.com/v3/lists' \
-H 'x-api-key: example.apiKey'
```
{% endtab %}
{% endtabs %}

{% api-method method="post" host="https://api.zaius.com/v3" path="/lists" %}
{% api-method-summary %}
Create List
{% endapi-method-summary %}

{% api-method-description %}
Create a new list within a Zaius account.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="name" type="string" required=true %}
The name of the list to create.
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=202 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "created": {
    "list_id": "sample_list",
    "name": "Example List"
  }
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% code-tabs %}
{% code-tabs-item title="Example Payload" %}
```javascript
{
    "name": "My List"
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}




# Consent

{% hint style="danger" %}
Customers that have not given marketing consent **cannot receive marketing messages.**
{% endhint %}

{% api-method method="post" host="https://api.zaius.com/v3" path="/lists/subscriptions" %}
{% api-method-summary %}
Update Consent
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows you to update consent for a customer.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="email" type="string" required=true %}
The customer's email
{% endapi-method-parameter %}

{% api-method-parameter name="opted\_in" type="boolean" required=true %}
The user's subscription status. The first time a contactable email is received by Zaius, it is opted in unless otherwise noted.
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
    "timestamp": "2019-07-30T23:55:00.519Z"
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
    "timestamp": "2019-07-30T23:53:48.615Z",
    "detail": {
        "message": "Unable to parse request body."
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
[
  {
    "email": "sample@test.com",
    "opted_in": false
  }
]
```
{% endcode-tabs-item %}
{% endcode-tabs %}


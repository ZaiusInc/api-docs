---
description: Manage a Customer's marketing consent.
---

# Consent

{% hint style="danger" %}
Customers that have not given marketing consent **cannot receive marketing messages.**
{% endhint %}

{% api-method method="post" host="https://api.zaius.com/v3" path="/consent" %}
{% api-method-summary %}
Update Consent
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows you to update consent for a customer.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="event\_data" type="object" required=false %}
object of key/value pairs that get added to a consent event
{% endapi-method-parameter %}

{% api-method-parameter name="consent\_update\_ts" type="number" required=false %}
the time of the event, if blank set to current time
{% endapi-method-parameter %}

{% api-method-parameter name="consent\_update\_reason" type="string" required=false %}
a reason for updating consent, can be any text value, for audit purposes
{% endapi-method-parameter %}

{% api-method-parameter name="consent" type="boolean" required=true %}
true or false, whether or not this identifier has provided consent to receive marketing messages
{% endapi-method-parameter %}

{% api-method-parameter name="identifier\_field\_name" type="string" required=true %}
the value for the identifier field type \(e.g. email\)
{% endapi-method-parameter %}

{% api-method-parameter name="identifier\_value" type="string" required=true %}
any valid marketing identifier type \(e.g. tyler@zaius.com\)
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
[{
	"identifier_value": "tyler@zaius.com",
	"identifier_field_name": "email",
	"consent": true, 
	"consent_update_reason": "reason", //optional
	"consent_update_ts": ts, //optional
	"event_data": {} //optional
},{
	"identifier_value": "email",
	"identifier_field_name": "tyler@zaius.com",
	"consent": true,
	"consent_update_reason": "reason", //optional
	"consent_update_ts": ts, //optional
	"event_data": {} //optional
}]
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% api-method method="get" host="https://api.zaius.com/v3" path="/consent/{field\_name}?id={id}" %}
{% api-method-summary %}
Get Consent
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows you to get marketing consent information about a customer.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="field\_name" type="string" required=true %}
the type of identifier you're request consent for \(e.g. email\)
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-query-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
the identifier value you're requesting consent information on
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
	"identifier_value": "id",
	"identifier_field_name": "field_name",
	"zaius_id": "id",
	"consent": {true/false},
	"consent_update_reason": "reason", //optional
	"consent_update_ts": ts
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% code-tabs %}
{% code-tabs-item title="Example Request" %}
```javascript
curl -iX GET \
'https://api.zaius.com/v3/consent/{field_name}?id={id}' \
-H 'x-api-key: example.apiKey'
```
{% endcode-tabs-item %}
{% endcode-tabs %}


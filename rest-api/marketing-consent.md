---
description: Update a customer's consent to receive marketing messages.
---

# Consent

{% api-method method="post" host="https://api.zaius.com/v3" path="/consent" %}
{% api-method-summary %}
Update Consent
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows you to get free cakes.
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
Cake successfully retrieved.
{% endapi-method-response-example-description %}

```javascript
{
    "name": "Cake's name",
    "recipe": "Cake's recipe name",
    "cake": "Binary cake"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
Could not find a cake matching this query.
{% endapi-method-response-example-description %}

```javascript
{
    "message": "Ain't no cake like that."
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

{% api-method method="get" host="https://api.zaius.com/v3" path="/consent/{field\_name}" %}
{% api-method-summary %}
Get Consent
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows you to get free cakes.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="field\_name" type="string" required=true %}
the type of identifier you're request consent for \(e.g. email\)
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

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
Cake successfully retrieved.
{% endapi-method-response-example-description %}

```javascript
{
    "name": "Cake's name",
    "recipe": "Cake's recipe name",
    "cake": "Binary cake"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
Could not find a cake matching this query.
{% endapi-method-response-example-description %}

```javascript
{
    "message": "Ain't no cake like that."
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


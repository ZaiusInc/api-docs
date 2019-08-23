# Reachability

{% api-method method="post" host="https://api.zaius.com/v3" path="/reachability" %}
{% api-method-summary %}
Update Reachability
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows you to update reachability for a messaging identifier.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="reachable\_update\_reason" type="string" required=false %}
additional details about the reachability type \(e.g. error message / code\)
{% endapi-method-parameter %}

{% api-method-parameter name="event\_data" type="object" required=false %}
object of key/value pairs that get added to a reachability event
{% endapi-method-parameter %}

{% api-method-parameter name="reachable\_update\_ts" type="number" required=false %}
the time of the event, if blank set to current time
{% endapi-method-parameter %}

{% api-method-parameter name="reachable\_update\_type" type="string" required=true %}
the reason the identifier is unreachable \(e.g. hard bounce\)
{% endapi-method-parameter %}

{% api-method-parameter name="reachable" type="boolean" required=true %}
true or false, whether or not this identifier is reachable
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
	"identifier_value": "id",
	"identifier_field_name": "field_name",
	"reachable": false,
	"reachable_update_type": "string", //generic type, eg “hard bounce”
	"reachable_update_reason": "string", //optional; specific error
	"reachable_update_ts": ts, //optional; if blank, set to current ts
	"event_data": {} //optional; array of key-value pairs
},{
	"identifier_value": "id",
	"identifier_field_name": "field_name",
	"reachable": true,
	"reachable_update_type": "string", //generic type, eg “hard bounce”
	"reachable_update_reason": "string", //optional; specific error
	"reachable_update_ts": ts, //optional; if blank, set to current ts
	"event_data": {} //optional; array of key-value pairs
}]
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% api-method method="get" host="https://api.zaius.com/v3" path="/consent/{field\_name}?id={id}" %}
{% api-method-summary %}
Get Consent
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows you to get reachability information about an identifier.
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
	"reachable": true,
	"reachable_update_type": "string", //generic type, eg “hard bounce”
	"reachable_update_reason": "string", //optional; specific error
	"reachable_update_ts": ts, //optional; if blank, set to current ts
	"event_data": {} //optional; array of key-value pairs
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
'https://api.zaius.com/v3/reachability/{field_name}?id={id}' \
-H 'x-api-key: example.apiKey'
```
{% endcode-tabs-item %}
{% endcode-tabs %}


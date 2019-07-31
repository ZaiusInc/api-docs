# Compliance

The Compliance API takes all identifiers provided to it, finds other identifiers that we know that are associated with the same user and adds them to our "opt-out" pool. Then we redact the customer record for that user. All new events and object updates that come in associated with that user will persist, but will be associated with the redacted profile.

{% hint style="danger" %}
#### If you're trying to opt-out users from a list or a specific channel, do not use this API.

Utilize the Consent API for managing a typical marketing based opt-outs.

Utilize this API for compliance based opt-outs \(e.g. GDPR\).
{% endhint %}

{% api-method method="post" host="https://api.zaius.com/v3" path="/compliance/opt\_out" %}
{% api-method-summary %}
Compliance Opt-out
{% endapi-method-summary %}

{% api-method-description %}
For a given identifier, find all known associated identifiers, redact relevant profiles, stop new updates to user's profile and don't send messages in the future to the user.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="requester" type="string" required=true %}
information about the requester of the opt-out for audit purposes
{% endapi-method-parameter %}

{% api-method-parameter name="identifier\_value" type="string" required=true %}
the value of the identifier to opt-out \(e.g. tyler@zaius.com\)
{% endapi-method-parameter %}

{% api-method-parameter name="identifier\_field\_name" type="string" required=true %}
the type of identifier that you are opting out \(e.g. email\)
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
  [{
    "requester": "tyler@example.com",
    "identifier_field_name": "email",
    "identifier_value": "tyler@zaius.com"
  },{
    "requester": "tyler@example.com",
    "identifier_field_name": "email",
    "identifier_value": "tyler@zaius.com"
  }]
```
{% endcode-tabs-item %}
{% endcode-tabs %}


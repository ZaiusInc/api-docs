# Identifiers

{% api-method method="post" host="https://api.zaius.com/v3" path="/schema/identifiers" %}
{% api-method-summary %}
Create Identifier
{% endapi-method-summary %}

{% api-method-description %}
Create a new identifier within Zaius that will be used for user resolution.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="name" type="string" required=true %}
the field name of the identifier, ending with one of the known suffixes: id, hash, number, token, alias, address, key
{% endapi-method-parameter %}

{% api-method-parameter name="display\_name" type="string" required=true %}
the human-readable name, ending with title-case version of the name suffix: ID, Hash, Number, Token, Alias, Address, Key
{% endapi-method-parameter %}

{% api-method-parameter name="merge\_confidence" type="string" required=true %}
the level of confidence \("high" or "low"\) that this identifier can be used to merge customer profiles together and is NOT shared between individuals \(eg, a shared device token\)
{% endapi-method-parameter %}

{% api-method-parameter name="messaging" type="boolean" required=false %}
whether this identifier can be used to message customers within campaigns
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "events": [
    {
      "name": "event_facebook_messenger_id",
      "display_name": "Event Facebook Messenger ID",
      "type": "identifier"
    }
  ],
  "customers": [
    {
      "name": "facebook_messenger_id",
      "display_name": "Last Seen Facebook Messenger ID",
      "type": "identifier"
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
  "timestamp": "2018-08-07T13:44:17.659Z",
  "detail": {
    "invalids": [
      {
        "field": "customers.name",
        "reason": "already used by another object"
      },
      {
        "field": "customers.display_name",
        "reason": "already used by another object"
      }
    ]
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
  "name": "facebook_messenger_id",
  "display_name": "Facebook Messenger ID"
  "merge_confidence": "high",
  "messaging": true
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}




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
{% api-method-parameter name="merge\_confidence" type="string" required=true %}
how confident are you that this identifier is not commonly on a shared device and can be used to merge customer records together? options are "high" and "low"
{% endapi-method-parameter %}

{% api-method-parameter name="name" type="string" required=true %}
the name of the identifier \(e.g. Shopify\)
{% endapi-method-parameter %}

{% api-method-parameter name="suffix" type="string" required=true %}
the suffix of the identifier \(id, hash, number, token, alias, address, key\)
{% endapi-method-parameter %}

{% api-method-parameter name="namespace" type="string" required=false %}
used to create multiple identifiers of the same name and type and prevent collisions
{% endapi-method-parameter %}

{% api-method-parameter name="messaging" type="boolean" required=false %}
can this identifier be used to message customers and within campaigns?
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
      "name": "event_my_name_my_namespace_id",
      "display_name": "Event My Name ID (My Namespace)",
      "type": "identifier"
    }
  ],
  "customers": [
    {
      "name": "my_name_my_namespace_id",
      "display_name": "Last Seen My Name ID (My Namespace)",
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
[{
  "name": "Facebook Messenger",
  "suffix": "id", // valid options: id, hash, number, token, alias, address, key
  "namespace": "My Facebook Page",
  "merge_confidence": "low",
  "messaging": true
}] // array optional
```
{% endcode-tabs-item %}
{% endcode-tabs %}




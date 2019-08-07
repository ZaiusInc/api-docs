# Metadata

{% api-method method="post" host="https://api.zaius.com/v3" path="/identifiers" %}
{% api-method-summary %}
Update Identifier Metadata
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows you to update metadata for an identifier.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="metadata" type="object" required=true %}
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
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% code-tabs %}
{% code-tabs-item title="Example Payload" %}
```javascript
[
    {
        "identifier_value": "{id}",
        "identifier_field_name": "{singular field_name}", 
        "metadata" : {
            "field1": "",
            "field2": ""
        }
    }
]
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% api-method method="get" host="https://api.zaius.com/v3" path="/identifiers/{field\_name}?id={id}" %}
{% api-method-summary %}
Get Identifier Metadata
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows you to get identifier metadata.
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
    "identifier_value": "john@example.com",
    "identifier_field_name": "email",
    "zaius_id": "abcd", //response only
    "metadata" : {
        "mailbox_provider": "google",
        "primary_mailbox": true
    },
    "metadata_update_ts": 1556582935
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
'https://api.zaius.com/v3/identifiers/{field_name}?id={id}' \
-H 'x-api-key: example.apiKey'
```
{% endcode-tabs-item %}
{% endcode-tabs %}


# Authentication

## Public vs. Private API Keys

Zaius provides two forms of authentication: Public and Private.

{% hint style="info" %}
Keys are scoped at the account level
{% endhint %}

If you have multiple accounts within Zaius, the data within one account is not accessible to the others, you must utilize the appropriate API key.

* **Public API Keys** \(sometimes referred to as a Tracker ID\) are used for most API calls that send data to Zaius and for a limited number of API calls that request data from Zaius and may be exposed publicly on the Internet.
* **Private API Keys** can be used for querying data from Zaius for backend services and integrations.

{% hint style="warning" %}
When you revoke a private API key, your existing key is available for 12 hours as a grace period to ease any transitions.
{% endhint %}

## Locate API Keys

To view your API Keys, go to _Account Settings_ -&gt; _APIs_. The screen displays a table of all available APIs:

| Table Column | Description |
| :--- | :--- |
| API Name | The name of the API |
| Usage Plan | The usage plan for the API will be `Default`, `No Access` or the name of a Custom Plan / Package that your company has access to. |
| Limits | The limits placed upon the API including rate limits and quotas \(if applicable\) |

{% hint style="info" %}
Public API Key and Tracker ID are synonymous within Zaius
{% endhint %}

## Using API Keys

To use your API key, include it in the headers of your REST API request. For example:

{% tabs %}
{% tab title="Example Request" %}
```bash
curl -iX GET \
'https://api.zaius.com/v3/profiles?email=sample@test.com' \
-H 'x-api-key: example.apiKey'
```
{% endtab %}
{% endtabs %}


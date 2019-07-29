# Rate Limits

{% hint style="warning" %}
If you are loading large amounts of data in bulk, ensure every request is done as a batch. Every request can include up to 500 distinct objects \(e.g. 500 customers per request at 10 requests per second = 5,000 customer updates per second\)
{% endhint %}

{% page-ref page="batch-requests.md" %}

| API | Default Rate Limit |
| :--- | :--- |
| Profile | 10 requests / second |
| Event | 10 requests / second |
| Object | 10 requests / second |
| Recommendation | 10 requests / second |
| Export | 10 requests / second |
| Compliance | 1 request / second |
| Identifier Metadata | 10 requests / second |
| Identifier Reachability | 10 requests / second |

{% hint style="info" %}
If you require higher rate limits for your use case, please contact the Zaius support team for more information.
{% endhint %}


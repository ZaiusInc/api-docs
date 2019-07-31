# Recommendations

## Overview

Fetch production recommendations for a single customer. Customer can be identified using one of `vuid`, `email`, `zaius_alias_*`, or `customer_id`.

Product records that are returned will include all the base Zaius product fields in addition to any custom fields defined in your product schema:

{% hint style="info" %}
Product recommendation results can be filtered using rules based on fields found on the products in your catalog, for example to exclude products which have no defined `image_url` or which have prices below \(and/or above\) some threshold. 

Speak with your customer service representative if you have a requirement to set up such filtering.
{% endhint %}

{% api-method method="get" host="https://api.zaius.com/v3" path="/recommendations/products?{identifier}={identifier\_value}" %}
{% api-method-summary %}
Get Recommended Products
{% endapi-method-summary %}

{% api-method-description %}
Get the subscription status of a customer identifier to a Zaius list.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-query-parameters %}
{% api-method-parameter name="sort\_by" type="string" required=false %}
Product field to sort by, which can be any base or custom field defined in your Product schema. Default sort is highest to lowest recommendation rank. Changing this will not change which products are returned, only the order in which they appear in the array.
{% endapi-method-parameter %}

{% api-method-parameter name="order" type="string" required=false %}
Default: "asc"   
Options: "asc", "desc"   
  
Order in which to sort the resulting products. Changing this will not change which products are returned, only the order in which they appear in the array. This will not change the order of products if there is no sort specified.
{% endapi-method-parameter %}

{% api-method-parameter name="limit" type="string" required=false %}
Integer \[ 1 .. 100 \]   
Default: 10  
Number of products to return
{% endapi-method-parameter %}

{% api-method-parameter name="{identifier}" type="string" required=true %}
The identifier type, for example "email".
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
[
  {
    "product_id": "1234BLK",
    "name": "Basics - Black",
    "brand": "Jungle James Basics",
    "sku": "1234BLK",
    "upc": "042100005264",
    "image_url": "https://http.cat/404",
    "price": 25.99,
    "parent_product_id": "1234"
  },
  {
    "product_id": "1234BLU",
    "name": "Basics - Blue",
    "brand": "Jungle James Basics",
    "sku": "1234BLU",
    "upc": "042100005265",
    "image_url": "https://http.cat/404",
    "price": 25.99,
    "parent_product_id": "1234"
  }
]
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=400 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "title": "Bad Request",
  "status": 400,
  "timestamp": "2019-01-02T15:53:51.522Z",
  "detail": {
    "message": "expected one of [vuid|customer_id|user_id|email|zaius_alias_*]."
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

{% tabs %}
{% tab title="Example Request" %}
```bash
curl -iX GET \
'https://api.zaius.com/v3/recommendations/products?email=sample@test.com&limit=10' \
-H 'x-api-key: example.apiKey'
```
{% endtab %}
{% endtabs %}


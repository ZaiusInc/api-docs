# Exports

## Overview

The Export API is an asynchronous API which enables you to export your data to s3 buckets.

The exports endpoint has two distinct behaviors, depending on whether the `objects` field or the `select` field has been used.

| field used | behavior |
| :--- | :--- |
| `select` | Filtered export of the object against which this filter is applied. |
| `objects` | Full export of the objects named in this array. |

Select provides a simple JSON syntax for selecting certain fields and filtering that can span several related Objects. Filters support conjunctions \(and & or\) to any depth and field comparisons include all the operators necessary for simple sql-like "where" clause filtering.

#### Completion <a id="completion"></a>

After triggering your export by calling the POST exports endpoint, you can determine when your job has been completed in two ways:

1. Check the bucket specified in your export response for a file called `complete.json`, which will be written upon completion.
2. Poll the [GET exports/{export\_id}](https://api.developer.zaius.com/#operation/getExportStatus) endpoint with the export id returned from the export response and look for state `completed`.

## Accessing Amazon S3

To learn how to access your exports within Amazon S3, please visit our Exports reference:

{% api-method method="post" host="https://api.zaius.com/v3" path="/exports" %}
{% api-method-summary %}
Start Export Job \(Filtered\)
{% endapi-method-summary %}

{% api-method-description %}
Export all filtered set of data from Zaius to Amazon S3.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="format" type="string" required=true %}
The format of the export. Valid values are "csv" and "parquet".
{% endapi-method-parameter %}

{% api-method-parameter name="delimiter" type="string" required=false %}
Defaults to 'comma'. Valid options are `comma`, `tab`, and `pipe`. **Not applicable to parquet exports.**
{% endapi-method-parameter %}

{% api-method-parameter name="select" type="object" required=true %}
The filtering rules to apply to this export.
{% endapi-method-parameter %}

{% api-method-parameter name="select.object" type="string" required=false %}
The object this selection filter applies to.
{% endapi-method-parameter %}

{% api-method-parameter name="select.fields" type="array" required=false %}
An array of fields to export. The array `['*']` captures all fields from `select.object`, but will not follow any relations.
{% endapi-method-parameter %}

{% api-method-parameter name="select.filter" type="object" required=false %}
Refer to ****"Filtering" section below
{% endapi-method-parameter %}

{% api-method-parameter name="select.filter.field" type="string" required=true %}
The field path to retrieve, following relations via the name of the relation and starting at the containing select's object.  
  
 For example, if select.object = 'event' and field = 'product.name', this would use the value of name on the Product table where the product\_id is the same as the product\_id on the Event.   
  
The string \* can be used as a wildcard to select all fields, but will not follow any relations.
{% endapi-method-parameter %}

{% api-method-parameter name="select.filter.operator" type="string" required=true %}
Available options include:  
"=" "!=" "&gt;" "&gt;=" "&lt;" "&lt;=" "like" "not like" "ilike" "not ilike" "is" "is not"  
  
The evaluation to apply to the field's value. For null comparisons, use = or != with a value of null.
{% endapi-method-parameter %}

{% api-method-parameter name="select.filter.value" type="string" required=true %}
The value to evaluate the field against using operator. Use % to indicate a wildcard in string \[not\] \[i\]like comparisons.
{% endapi-method-parameter %}

{% api-method-parameter name="select.sorts" type="array" required=false %}
Sort by specification applied for each export file \(a single table export will cross multiple files\).
{% endapi-method-parameter %}

{% api-method-parameter name="selects.sorts.field" type="string" required=true %}
The field path to retrieve, following relations via the relation name and starting at the containing select's object.   
  
For example, if select.object = 'event' and field = 'product.name', this would use the value of name on the Product table where the product\_id is the same as the product\_id on the Event.   
  
The string \* can be used as a wildcard to select all fields, but will not follow any relations.
{% endapi-method-parameter %}

{% api-method-parameter name="select.sorts.order" type="string" required=false %}
Default: "asc"  
  
Options:"asc" "desc"   
  
Order in which to sort the coupled field value by in the result set.
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "id": "3aab9524-5248-45f9-8102-0399872a921e",
  "path": "s3://zaius-outgoing/kIFB_X1VG2gf6caBn8LHtg/data-exports/3aab9524-5248-45f9-8102-0399872a921e",
  "state": "pending",
  "requested_at": "2018-09-10T21:07:10-05:00",
  "detail": {
    "id": "3aab9524-5248-45f9-8102-0399872a921e",
    "format": "csv",
    "delimiter": "comma",
    "select": {
      "object": "events",
      "fields": [
        "product.name"
      ],
      "filter": {
        "field": "product.name",
        "operator": "=",
        "value": "%shoe%"
      },
      "sorts": [
        {
          "field": "product.name",
          "order": "asc"
        }
      ]
    },
    "objects": [
      "string"
    ]
  }
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
    "invalids": [
      {
        "field": "delimiter",
        "reason": "Unrecognized delimiter, valid options are comma, tab or pipe"
      }
    ]
  }
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=403 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "title": "Forbidden",
  "status": 403,
  "timestamp": "2018-09-10T21:07:10-05:00",
  "detail": {
    "message": "Insufficient privileges to access this resource."
  }
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "title": "Not Found",
  "status": 404,
  "timestamp": "2018-09-10T21:07:10-05:00",
  "detail": {
    "message": "Unable to locate field products.unknown_field"
  }
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=422 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "title": "Unprocessable Entity",
  "status": 422,
  "timestamp": "2018-09-10T21:07:10-05:00",
  "detail": {
    "message": "Unable to process request.  The following object(s) are currently being exported: events"
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
  "format": "csv",
  "delimiter": "comma",
  "select": {
    "object": "events",
    "fields": [
      "product.name"
    ],
    "filter": {
      "field": "product.name",
      "operator": "=",
      "value": "%shoe%"
    },
    "sorts": [
      {
        "field": "product.name",
        "order": "asc"
      }
    ]
  }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% api-method method="post" host="https://api.zaius.com/v3" path="/exports" %}
{% api-method-summary %}
Start Export Job \(Unfiltered\)
{% endapi-method-summary %}

{% api-method-description %}
Export all filtered set of data from Zaius to Amazon S3.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="format" type="string" required=true %}
The format of the export. Valid values are "csv" and "parquet".
{% endapi-method-parameter %}

{% api-method-parameter name="delimiter" type="string" required=false %}
Defaults to 'comma'. Valid options are `comma`, `tab`, and `pipe`. **Not applicable to parquet exports.**
{% endapi-method-parameter %}

{% api-method-parameter name="objects" type="array" required=true %}
The objects to export in full.
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "id": "3aab9524-5248-45f9-8102-0399872a921e",
  "path": "s3://zaius-outgoing/kIFB_X1VG2gf6caBn8LHtg/data-exports/3aab9524-5248-45f9-8102-0399872a921e",
  "state": "pending",
  "requested_at": "2018-09-10T21:07:10-05:00",
  "detail": {
    "id": "3aab9524-5248-45f9-8102-0399872a921e",
    "format": "csv",
    "delimiter": "comma",
    "select": {
      "object": "events",
      "fields": [
        "product.name"
      ],
      "filter": {
        "field": "product.name",
        "operator": "=",
        "value": "%shoe%"
      },
      "sorts": [
        {
          "field": "product.name",
          "order": "asc"
        }
      ]
    },
    "objects": [
      "string"
    ]
  }
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
    "invalids": [
      {
        "field": "delimiter",
        "reason": "Unrecognized delimiter, valid options are comma, tab or pipe"
      }
    ]
  }
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=403 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "title": "Forbidden",
  "status": 403,
  "timestamp": "2018-09-10T21:07:10-05:00",
  "detail": {
    "message": "Insufficient privileges to access this resource."
  }
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "title": "Not Found",
  "status": 404,
  "timestamp": "2018-09-10T21:07:10-05:00",
  "detail": {
    "message": "Unable to locate field products.unknown_field"
  }
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=422 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "title": "Unprocessable Entity",
  "status": 422,
  "timestamp": "2018-09-10T21:07:10-05:00",
  "detail": {
    "message": "Unable to process request.  The following object(s) are currently being exported: events"
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
  "objects": [
    "string"
  ],
  "format": "csv",
  "delimiter": "comma"
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## More on Filtering

The filtering section in the payload may contain one of the following:

* `Clause`: A standalone clause for defining a filter on Zaius data elements.
* `AND (all sub-clauses)`: A combination of clauses - if all of the contained clauses \(which may include nested `AND`/`OR` clauses\) evaluate to true, this data element may pass the overall filter. If any one \(or more\) of them do not, the data element will not pass the filter.
* `OR (at least one sub-clause)`: A combination of clauses - if any one \(or more\) of the contained clauses \(which may include nested `AND`/`OR` clauses\) evaluates to true, this data element may pass the overall filter. If none do, the data element will not pass the filter.

Note that the nature of AND and OR clauses enables arbitrarily many criteria to be combined.


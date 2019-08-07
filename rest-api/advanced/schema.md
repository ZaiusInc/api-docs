# Schema

All data in Zaius is stored within collections called Objects \(what many think of as a database table\). 

Objects are composed of Fields. 

Fields link objects together via Relations.

## Objects

{% code-tabs %}
{% code-tabs-item title="Object Definition" %}
```javascript
{
  "name": "object_name",
  "display_name": "Display Name",
  "alias": "object_alias",
  "fields": [],
  "relations": []
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

| property | description |
| :--- | :--- |
| name | plural name for the object |
| display\_name | user-friendly name shown within Zaius |
| alias | singular name for the object |
| fields | collection of `Field` objects constituting the `Object` |
| relations | collection of `Relation` objects |

{% api-method method="post" host="https://api.zaius.com/v3" path="/schema/objects" %}
{% api-method-summary %}
Create Object
{% endapi-method-summary %}

{% api-method-description %}
Create a new Object within Zaius, define its fields, and how it relates to other objects
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="name" type="string" required=true %}
the plural name of the object \(e.g. tickets\)
{% endapi-method-parameter %}

{% api-method-parameter name="display\_name" type="string" required=true %}
the human-readable name of the object \(e.g. Tickets\)
{% endapi-method-parameter %}

{% api-method-parameter name="alias" type="string" required=false %}
the singular name of the object \(e.g. ticket\)
{% endapi-method-parameter %}

{% api-method-parameter name="fields" type="array" required=true %}
an array of fields objects \(see definition above\)
{% endapi-method-parameter %}

{% api-method-parameter name="relations" type="array" required=false %}
an array of relations objects \(see definition above\)
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "name": "objects",
  "display_name": "Object",
  "alias": "object",
  "fields": [
    {
      "name": "object_id",
      "display_name": "New Object Identifier",
      "type": "string",
      "primary": true
    },{
      "name": "another_field",
      "display_name": "Another Fields",
      "type": "string"
    },{
      "name": "child_id",
      "display_name": "Child Identifier",
      "type": "number"
    }
  ],
  "relations": [
    {
      "name": "my_relation",
      "display_name": "My Relationship",
      "child_object": "child",
      "join_fields": [{
        "parent": "child_id",
        "child": "child_id"
      }]
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
        "field": "name",
        "reason": "already used by another object"
      },
      {
        "field": "alias",
        "reason": "already used by another object"
      },
      {
        "field": "display_name",
        "reason": "already used by another object"
      },
      {
        "field": "fields",
        "reason": "at least one primary key field required"
      },
      {
        "field": "relations[0].child_object",
        "reason": "does not exist"
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
  "name": "objects",
  "display_name": "Object",
  "alias": "object",
  "fields": [
    {
      "name": "object_id",
      "display_name": "New Object Identifier",
      "type": "string",
      "primary": true
    },{
      "name": "another_field",
      "display_name": "Another Fields",
      "type": "string"
    },{
      "name": "child_id",
      "display_name": "Child Identifier",
      "type": "number"
    }
  ],
  "relations": [
    {
      "name": "my_relation",
      "display_name": "My Relationship",
      "child_object": "child",
      "join_fields": [{
        "parent": "child_id",
        "child": "child_id"
      }]
    }
  ]
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% api-method method="get" host="https://api.zaius.com/v3" path="/schema/objects" %}
{% api-method-summary %}
List Objects
{% endapi-method-summary %}

{% api-method-description %}
List the details of all objects within a Zaius account.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
[
  {
    "name": "tickets",
    "display_name": "Tickets",
    "alias": "ticket",
    "fields": [
      {
        "name": "field_name",
        "type": "number",
        "display_name": "Display Name",
        "primary": true
      }
    ],
    "relations": [
      {
        "name": "my_relation",
        "display_name": "My Relationship",
        "child_object": "target_object_name",
        "join_fields": [
          {
            "parent": "child_id",
            "child": "child_id"
          }
        ]
      }
    ]
  },
  {
    "name": "concerts",
    "display_name": "Concerts",
    "alias": "concert",
    "fields": [
      {
        "name": "field_name",
        "type": "number",
        "display_name": "Display Name",
        "primary": true
      }
    ],
    "relations": [
      {
        "name": "my_relation",
        "display_name": "My Relationship",
        "child_object": "target_object_name",
        "join_fields": [
          {
            "parent": "child_id",
            "child": "child_id"
          }
        ]
      }
    ]
  }
]
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% tabs %}
{% tab title="Example Request" %}
```bash
curl -iX GET \
'https://api.zaius.com/v3/schema/objects' \
-H 'x-api-key: example.apiKey'
```
{% endtab %}
{% endtabs %}

{% api-method method="get" host="https://api.zaius.com/v3" path="/schema/objects/{object\_name}" %}
{% api-method-summary %}
Get Object
{% endapi-method-summary %}

{% api-method-description %}
List all objects with a Zaius account.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="{object\_name}" type="string" required=true %}
List the details of a specific object.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "name": "tickets",
  "display_name": "Tickets",
  "alias": "ticket",
  "fields": [
    {
      "name": "field_name",
      "type": "number",
      "display_name": "Display Name",
      "primary": true
    }
  ],
  "relations": [
    {
      "name": "my_relation",
      "display_name": "My Relationship",
      "child_object": "target_object_name",
      "join_fields": [
        {
          "parent": "child_id",
          "child": "child_id"
        }
      ]
    }
  ]
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
'https://api.zaius.com/v3/schema/objects/myobject' \
-H 'x-api-key: example.apiKey'
```
{% endtab %}
{% endtabs %}

## Fields

```javascript
{
  "name": "field_name",
  "type": "number",
  "auto": true,
  "display_name": "Display Name",
  "description": "Description of field",
  "created_by": "zaius",
  "primary_key": true
}
```

| property | description |
| :--- | :--- |
| name | name of the field |
| type | field data type. options are `number`, `timestamp`, `text`, `boolean` |
| auto | \(read only\) marks the field as one that is auto populated by Zaius |
| display\_name | the user-friendly name used within Zaius |
| description | description of the field |
| created\_by | \(read only\) specifies what/who created the field. current values as `zaius` and `account` |
| primary\_key | marks the field as identifying for the containing object. only allowed during object creation. |

{% api-method method="post" host="https://api.zaius.com/v3" path="/schema/objects/{object\_name}/fields" %}
{% api-method-summary %}
Create Field
{% endapi-method-summary %}

{% api-method-description %}
Create a new field on an Object within Zaius
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="{object\_name}" type="string" required=true %}
the name of the object where the field will be created
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-body-parameters %}
{% api-method-parameter name="name" type="string" required=true %}
the name of the field \(e.g. ticket\_id\)
{% endapi-method-parameter %}

{% api-method-parameter name="display\_name" type="string" required=true %}
the human-readable name of the field \(e.g. Ticket ID\)
{% endapi-method-parameter %}

{% api-method-parameter name="description" type="array" required=false %}
detailed description of what the field's purpose is
{% endapi-method-parameter %}

{% api-method-parameter name="type" type="array" required=true %}
an array of relations field data type. options are `number`, `timestamp`, `string`, `boolean`
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
    "name": "field_name",
    "display_name": "Display Name",
    "description": "Description of field",
    "type": "number"
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
        "field": "name",
        "reason": "already exists"
      }
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
  "name": "field_name",
  "type": "number",
  "display_name": "Display Name",
  "description": "Description of field"
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### Identifier Fields

{% hint style="warning" %}
If you are attempting to create an identifier \(e.g. an address for messaging or an internal reference to a customer record similar to an email, phone number or token\), refer to the Identifier API documentation:
{% endhint %}

{% api-method method="get" host="https://api.zaius.com/v3" path="/schema/objects/{object\_name}/fields" %}
{% api-method-summary %}
List Fields
{% endapi-method-summary %}

{% api-method-description %}
List the details of all fields of an object.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="{object\_name}" type="string" required=true %}
The name of the object.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
[
  {
    "name": "object_id",
    "display_name": "New Object Identifier",
    "type": "string",
    "created_by" "account",
    "primary": true
  },
  {
    "name": "another_field",
    "display_name": "Another Fields",
    "type": "string",
    "created_by" "account"
  },
  {
    "name": "child_id",
    "display_name": "Child Identifier",
    "type": "number",
    "created_by" "account"
  }
]
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% page-ref page="identifiers/" %}

{% code-tabs %}
{% code-tabs-item title="Example Payload" %}
```javascript
{
  "name": "my_relation",
  "display_name": "My Relationship",
  "child_object": "child",
  "join_fields": [{
    "parent": "child_id",
    "child": "child_id"
  }]
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% tabs %}
{% tab title="Example Request" %}
```bash
curl -iX GET \
'https://api.zaius.com/v3/schema/objects/{object_name}/fields' \
-H 'x-api-key: example.apiKey'
```
{% endtab %}
{% endtabs %}

{% api-method method="get" host="https://api.zaius.com/v3" path="/schema/objects/{object\_name}/fields/{field\_name}" %}
{% api-method-summary %}
Get Field
{% endapi-method-summary %}

{% api-method-description %}
List the details of a single field of an object.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="{field\_name}" type="string" required=true %}
The name of the field.
{% endapi-method-parameter %}

{% api-method-parameter name="{object\_name}" type="string" required=true %}
The name of the object.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  	"name": "field_name",
  	"type": "number",
  	"display_name": "Display Name",
  	"auto": true,
  	"description": "The venue that the user visisted.",
    "created_by" "zaius",
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
'https://api.zaius.com/v3/schema/objects/{object_name}/fields/{field_name}' \
-H 'x-api-key: example.apiKey'
```
{% endtab %}
{% endtabs %}

## Relationships

Representation describing a relationship between two objects. The `Object` containing the `Relation` definition is the `parent` object.

```javascript
{
  "name": "relation_name",
  "display_name": "Relation Display Name",
  "child_object": "child_object_name",
  "join_fields": [{
    "parent": "child_id",
    "child": "child_id"
  }]
}
```

| property | description |
| :--- | :--- |
| name | name for the relation |
| display\_name | user-friendly name shown within Zaius |
| child\_object | child `Object` name |
| join\_fields | collection of `parent` `child` pairs. `parent` is the field name \(foreign key\) on the owning `Object` and `child` is the related `Object`s primary key. Multiple are allowed to support objects with compound primary keys. |

{% api-method method="post" host="https://api.zaius.com/v3" path="/schema/objects/{object\_name}/relations" %}
{% api-method-summary %}
Create Relationship
{% endapi-method-summary %}

{% api-method-description %}
Create a new relation between Objects within Zaius
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="{object\_name}" type="string" required=true %}
the name of the object where the field will be created
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-body-parameters %}
{% api-method-parameter name="child\_object" type="boolean" required=true %}
the name of the child object
{% endapi-method-parameter %}

{% api-method-parameter name="name" type="string" required=true %}
the name of the relationship \(e.g. ticket\)
{% endapi-method-parameter %}

{% api-method-parameter name="display\_name" type="string" required=true %}
the -readable name of the field \(e.g. Ticket\)
{% endapi-method-parameter %}

{% api-method-parameter name="join\_fields.parent" type="array" required=true %}
the name on this object that will link to the child object \(e.g. id\)
{% endapi-method-parameter %}

{% api-method-parameter name="join\_fields.child" type="array" required=true %}
the name on the child object that will link to this object \(e.g. ticket\_id\)
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "name": "my_relation",
  "display_name": "My Relationship",
  "child_object": "child",
  "join_fields": [{
    "parent": "child_id",
    "child": "child_id"
  }]
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
  "timestamp": "2018-08-14T12:23:04.500Z",
  "detail": {
    "invalids": [
      {
        "field": "join_fields[0].parent",
        "reason": "does not match child data type"
      }
    ]
  }
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://api.zaius.com/v3" path="/schema/objects/{object\_name}/relations" %}
{% api-method-summary %}
List Relations
{% endapi-method-summary %}

{% api-method-description %}
List the details of all relationships of an object.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="{object\_name}" type="string" required=true %}
The name of the object.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
[
  {
    "name": "my_relation",
    "display_name": "My Relationship",
    "child_object": "child",
    "join_fields": [{
      "parent": "child_id",
      "child": "child_id"
    }]
  },
  {
    "name": "my_relation2",
    "display_name": "My Relationship 2",
    "child_object": "child",
    "join_fields": [{
      "parent": "child_id",
      "child": "child_id"
    }]
  }
]
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% tabs %}
{% tab title="Example Request" %}
```bash
curl -iX GET \
'https://api.zaius.com/v3/schema/objects/{object_name}/relations' \
-H 'x-api-key: example.apiKey'
```
{% endtab %}
{% endtabs %}

{% api-method method="get" host="https://api.zaius.com/v3" path="/schema/objects/{object\_name}/relations/{relation\_name}" %}
{% api-method-summary %}
Get Relation
{% endapi-method-summary %}

{% api-method-description %}
List the details of a single relationship of an object.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="{relation\_name}" type="string" required=true %}
The name of the relationship.
{% endapi-method-parameter %}

{% api-method-parameter name="{object\_name}" type="string" required=true %}
The name of the object.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "name": "my_relation",
  "display_name": "My Relationship",
  "child_object": "target_object_name",
  "join_fields": [{
    "parent": "child_id",
    "child": "child_id"
  }]
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
'https://api.zaius.com/v3/schema/objects/{object_name}/relations/{relation_name}' \
-H 'x-api-key: example.apiKey'
```
{% endtab %}
{% endtabs %}


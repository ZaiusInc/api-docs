# Schema

## Overview

All data in Zaius is stored within collections called Objects \(what many think of as a database table\). 

Objects are composed of Fields. 

Fields link objects together via Relations.

## Objects

```javascript
{
  "name": "object_name",
  "display_name": "Display Name",
  "alias": "object_alias",
  "fields": [],
  "relations": []
}
```

| property | description |
| :--- | :--- |
| name | plural name for the object |
| display\_name | user-friendly name shown within Zaius |
| alias | singular name for the object |
| fields | collection of `Field` objects constituting the `Object` |
| relations | collection of `Relation` objects |

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
{% api-method-parameter name="primary\_key" type="boolean" required=true %}
whether or not the field is the object's primary key
{% endapi-method-parameter %}

{% api-method-parameter name="name" type="string" required=true %}
the plural name of the object \(e.g. ticket\_id\)
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
  "auto": true,
  "display_name": "Display Name",
  "description": "Description of field",
  "primary_key": true
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

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


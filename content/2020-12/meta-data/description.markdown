---
keyword: "description"
signature: "String"
value: This keyword must be set to a string
summary: "An explanation about the purpose of the instance described by the schema."
kind: [ "annotation" ]
instance: [ "any" ]
specification: "https://json-schema.org/draft/2020-12/json-schema-validation.html#section-9.1"
metaschema: "https://json-schema.org/draft/2020-12/meta/meta-data"
index: -999
introduced_in: draft1
annotation:
   description: The description set by this keyword
   kind: [ "string" ]
related:
  - vocabulary: meta-data
    keyword: title
  - vocabulary: meta-data
    keyword: examples
  - vocabulary: meta-data
    keyword: default
  - vocabulary: meta-data
    keyword: readOnly
  - vocabulary: meta-data
    keyword: writeOnly
  - vocabulary: meta-data
    keyword: deprecated
---

The `description` keyword in JSON Schema is used to provide a human readable description for the schema. It does not affect data validation but serves as an informative annotation.

## Examples

{{<schema `Schema with 'description' keyword`>}}
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "description": "The age of a person",
  "type": "number"
}
{{</schema>}}

{{<instance-pass `An instance with a numeric value is valid`>}}
45
{{</instance-pass>}}

{{<instance-annotation>}}
{ "keyword": "/description", "instance": "", "value": "The age of a person" }
{{</instance-annotation>}}

{{<schema `Schema with logical operators`>}}
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "description": "Personal information of a user",
  "properties": {
    "name": { "type": "string" },
    "age": { "type": "number" }
  },
  "if": {
    "description": "if block",
    "properties": {
      "age": { "description": "Age", "minimum": 18 }
    }
  },
  "then": {
    "description": "then block",
    "properties": {
      "eligible": { "description": "Eligible", "const": true }
    }
  },
  "else": {
    "description": "else block",
    "properties": {
      "eligible": { "description": "Not eligible", "const": false }
    }
  }
}
{{</schema>}}

{{<instance-pass>}}
{
  "name": "John Doe",
  "age": 25,
  "eligible": true
}
{{</instance-pass>}}

{{<instance-annotation>}}
{ "keyword": "/description", "instance": "", "value": "Personal information of a user" }
{ "keyword": "/if/description", "instance": "", "value": "if block" }
{ "keyword": "/if/properties/age/description", "instance": "/age", "value": "Age" }
{ "keyword": "/then/description", "instance": "", "value": "then block", }
{ "keyword": "/then/properties/eligible/description", "instance": "/eligible", "value": "Eligible" }
{{</instance-annotation>}}

{{<schema `Schema with multiple annotations for the same instance`>}}
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "description": "A person name",
  "$ref": "#/$defs/name",
  "$defs": {
    "name": {
      "description": "A person name",
      "type": "string"
    }
  }
}
{{</schema>}}

{{<instance-pass>}}
"John Doe"
{{</instance-pass>}}

{{<instance-annotation>}}
{ "keyword": "/description", "instance": "", "value": "A person name" }
{ "keyword": "/$ref/description", "instance": "", "value": "A person name" }
{{</instance-annotation>}}

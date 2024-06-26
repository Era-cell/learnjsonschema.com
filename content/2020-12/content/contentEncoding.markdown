---
keyword: "contentEncoding"
signature: "String"
value: This keyword should be set to a standard (to increase interoperability) encoding name such as those defined in [RFC 4648](https://www.rfc-editor.org/info/rfc4686)
summary: "The string instance should be interpreted as encoded binary data and decoded using the encoding named by this property."
kind: [ "annotation" ]
instance: [ "string" ]
specification: "https://json-schema.org/draft/2020-12/json-schema-validation.html#section-8.3"
metaschema: "https://json-schema.org/draft/2020-12/meta/content"
tests:
  - draft2020-12/content.json
introduced_in: draft7
annotation:
   description: The content encoding name set by this keyword
   kind: [ "string" ]
related:
  - vocabulary: content
    keyword: contentMediaType
  - vocabulary: content
    keyword: contentSchema
---

The `contentEncoding` keyword is an annotation used to specify the encoding used to store the contents of a string, particularly when it represents binary data. It indicates how the string value should be interpreted and decoded. This keyword is not directly involved in the validation process but provides metadata about the content.

* `contentEncoding` doesn't enforce strict validation. However, it's recommended to use it correctly to ensure compatibility with applications that might interpret the encoding.
* It represents the type of binary encoding used for the string under question. Some of the common encodings are listed [here](#common-encodings).
* The JSON Schema specification doesn't publish a predefined list of possible encodings

## Common Encodings

| Encoding   | Description                                                                                     | Reference |
|------------|-------------------------------------------------------------------------------------------------|-----------|
| `"base16"` | Encoding scheme for binary data using a 16-character hexadecimal alphabet                       | [RFC 4648 §8](https://datatracker.ietf.org/doc/html/rfc4648#section-8) |
| `"base32"` | Encoding scheme for binary data using a 32-character hexadecimal alphabet                                   | [RFC 4648 §6](https://datatracker.ietf.org/doc/html/rfc4648#section-6) |
| `"base64"` | Encoding scheme for binary data using a 64-character hexadecimal alphabet | [RFC 4648 §4](https://datatracker.ietf.org/doc/html/rfc4648#section-4) |

## Examples

{{<schema `Schema with 'contentEncoding' keyword`>}}
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "contentEncoding": "base64"
}
{{</schema>}}

{{<instance-pass `A properly encoded base64 string is valid`>}}
"SGVsbG8gV29ybGQ="    // --> Hello World (base64 encoded)
{{</instance-pass>}}

{{<instance-pass `An incorrectly encoded base64 string is also valid`>}}
"This is not base64 encoded!"
{{</instance-pass>}}

{{<instance-pass `'contentEncoding' is irrelevant for instances with values other than strings`>}}
[ "foo", "bar" ]
{{</instance-pass>}}

{{<instance-annotation>}}
{ "keyword": "/contentEncoding", "instance": "", "value": "base64" }
{{</instance-annotation>}}

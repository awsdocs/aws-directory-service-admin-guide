# Format Specification<a name="jsonformat"></a>

A Cloud Directory schema adds structure to the data in your data directories\. Cloud Directory provides two mechanisms for you to define your schema\. Developers can use specific API operations to construct a schema or they can upload a schema entirely using schema upload capabilities\. Schema documents can be uploaded via API calls or through the console\. This section describes the format to use when you upload entire schema documents\.

## JSON Schema Format<a name="json"></a>

A schema document is a JSON document in the following overall format\. 

```
{
     “facets”: {
            “facet name”: {
		“facetAttributes”: {
			“attribute name”: Attribute JSON Subsection
              }
      }
   }
}
```

A schema document contains a map of facet names to facets\. Each facet in turn contains a map containing attributes\. All facet names within a schema must be unique\. All attribute names within a facet must be unique\.

### Attribute JSON Subsection<a name="attributejsonsub"></a>

Facets contain attributes\. Each attribute defines the type of value that can be stored on an attribute\. The following JSON format describes an attribute\.

```
{
     “attributeDefinition”: Attribute Definition Subsection,
     “attributeReference”: Attribute Reference Subsection,
     “requiredBehavior”: “REQUIRED_ALWAYS or NOT_REQUIRED”
}
```

You must provide either an attribute definition or an attribute reference\. See related subsections for more information about each\. 

The required behavior field indicates whether this attribute is required or not\. You must provide this field\. Possible values are as follows:

+ `REQUIRED_ALWAYS`: This attribute must be provided when the object is created or a facet is added to the object\. You cannot remove this attribute\.

+ `NOT_REQUIRED`: This attribute may or may not be present\.

### Attribute Definition Subsection<a name="attributedefinitionsub"></a>

An attribute defines the type and the rules associated with an attribute value\. The following JSON layout describes the format\.

```
{ 
	“attributeType”: “One of STRING, NUMBER, BINARY, BOOLEAN, DATETIME”
	“defaultValue”: Default Value Subsection
       “isImmutable”: true or false
	“attributeRules”: Attribute Rules Subsection
}
```

### Default Value Subsection<a name="defaultvaluesub"></a>

Specify exactly one of the following default values\. Long values and Boolean values should be provided outside of quotes \(as their respective Javascript types instead of strings\)\. Binary values are provided using a URL\-safe Base64 encoded string \(as described in RFC 4648\)\. Datetimes are provided in the number of milliseconds since the epoch \(00:00:00 UTC on Jan 1, 1970\)\.

```
{ 
	“stringValue”: “a string value”,
	“longValue”: an integer value,
	“booleanValue”: a boolean value,
	“binaryValue”: a URL-safe Base64 encoded string,
	“datetimeValue”: an integer value representing milliseconds since epoch
}
```

### Attribute Rules Subsection<a name="attributerulessub"></a>

Attributes rules define constraints on attribute values\. You can define multiple rules for each attribute\. Attribute rules contain a rule type and a set of parameters for the rule\. You can find more details in the [Attribute Rules](attributerules.md) section\. 

```
{
	“rule name”: {
		“parameters”: {
			“rule parameter key 1”: “value”,
			“rule parameter key 2”: “value”
		},
		“ruleType”: “rule type value”
	}
}
```

### Attribute Reference Subsection<a name="attributerefsub"></a>

Attribute references are an advanced feature\. They allow multiple facets to share an attribute definition and stored value\. See the [Attribute References](attributereferences.md) section for more information\. You can define an attribute reference in JSON schema with the following template\.

```
{
	“targetSchemaArn”: “schema ARN”
	“targetFacetName”: “facet name”
	“targetAttributeName”: “attribute name”
}
```
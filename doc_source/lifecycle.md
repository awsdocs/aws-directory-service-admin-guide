# Schema Lifecycle<a name="lifecycle"></a>

Cloud Directory offers a schema lifecycle to help with the development of schemas\. This lifecycle consists of three states: Development, Published, and Applied\. These states are designed to facilitate construction and distribution of schemas\. Each of these states has different features aiding this effort\. 

The following diagram depicts possible transitions and verbiage\. All schema transitions are copy\-on\-write\. For example, publishing a development schema does not alter or remove the development schema\. 

![\[Image NOT FOUND\]](http://alpha-docs-aws.amazon.com/directoryservice/latest/admin-guide/images/cd_schema_lifecycle.png)

You can delete a schema when it is in either the Development or Published state\. Deleting a schema cannot be undone nor can it be restored once it has been deleted\.

Schemas in Development, Published and Applied states have ARNs that represent them\. These ARNs are used in API operations to describe the schema that the API operates on\. It is easy to discern the state of a schema by looking at a schema ARN\.

+ Development: `arn:aws:clouddirectory:us-east-1:1234567890:schema/development/SchemaName`

+ Published: `arn:aws:clouddirectory:us-east-1:1234567890:schema/published/SchemaName/Version`

+ Applied: `arn:aws:clouddirectory:us-east-1:1234567890:directory/directoryid/schema/SchemaName/Version`

## Development State<a name="devstate"></a>

Schemas are initially created in the development state\. Schemas in this state are fully mutable\. You can freely add or remove facets and attributes\. The majority of schema design occurs in this state\. Schemas in this state have a name but no version\.

## Published State<a name="pubstate"></a>

The published schema state stores schemas that are ready to be applied to data directories\. Schemas are published from the development state into the published state\. You cannot change schemas in the published state\. You can apply published schemas to any number of data directories\. 

Published and applied schemas must have a version associated with them\. For more information about versions, see [Schema Versioning](inplaceschemaupgrade.md#cdschemaversion)\.

## Applied State<a name="appliedstate"></a>

A published schema can be applied to data directories\. A schema that has been applied to a data directory is said to be applied\. Once you apply a schema to a data directory, you can use the schema's facets when creating objects\. You can apply multiple schemas to the same data directory\. Only the following changes are permitted on an applied schema\.

+  Add a facet to an applied schema

+  Add a non\-required attribute to an applied schema
# Attribute References<a name="attributereferences"></a>

Amazon Cloud Directory facets contain attributes\. Attributes can be either an attribute definition or an attribute reference\. Attribute definitions are attributes that declare their name and primitive type \(string, binary, Boolean, DateTime, or number\)\. They can also optionally declare their required behavior, default value, immutable flag, and attribute rules \(such as min/max length\)\.

Attribute references are attributes that derive their primitive type, default value, immutable flag and attribute rules from another preexisting attribute definition\. Attribute references do not have their own primitive type, default values, immutable flag or rules, since those properties come from the target attribute definition\.

Attribute references may override the required behavior of a target definition \(more details about this below\)\.

When you create an attribute reference, you provide only an attribute name and the target attribute definition \(which includes the facet name and attribute name of the target attribute definition\)\. Attribute references may not refer to other attribute references\. Also, at this time, attribute references may not target attribute definitions from a different schema\.

You can use an attribute reference when you want two or more attributes on an object to refer to the same storage location\. For example, imagine an object that has a User facet and an EnterpriseUser facet applied\. The User facet has a FirstName attribute definition, while the EnterpriseUser facet has an attribute reference pointing at User\.FirstName\. Since both FirstName attributes refer to the same storage location on the object, any change to either the User\.FirstName or the EnterpriseUser\.FirstName has the same effect\. 

## API Example<a name="referenceapiexample"></a>

The following example demonstrates the use of attribute references using the Cloud Directory API\. In this example, a base facet contains an attribute definition, and another facet contains an attribute referring to an attribute in the base facet\. Note that the reference attribute can be marked Required while the base facet is Not Required\. 

```
    // create base facet
    CreateFacetRequest req1 = new CreateFacetRequest()
      .withSchemaArn(devSchemaArn)
      .withName("baseFacet")
      .withAttributes(List(
        new FacetAttribute()
          .withName("baseAttr")
          .withRequiredBehavior(RequiredAttributeBehavior.NOT_REQUIRED)
          .withAttributeDefinition(new FacetAttributeDefinition().withType(FacetAttributeType.STRING))))
      .withObjectType(ObjectType.DIRECTORY)
    cloudDirectoryClient.createFacet(req1)

    // create another facet that refers to the base facet
    CreateFacetRequest req2 = new CreateFacetRequest()
      .withSchemaArn(devSchemaArn)
      .withName("facetA")
      .withAttributes(List(
        new FacetAttribute()
          .withName("ref")
          .withRequiredBehavior(RequiredAttributeBehavior.REQUIRED_ALWAYS)
          .withAttributeReference(new FacetAttributeReference()
            .withTargetFacetName("baseFacet")
            .withTargetAttributeName("baseAttr"))))
      .withObjectType(ObjectType.DIRECTORY)
    cloudDirectoryClient.createFacet(req2)
```

## JSON Example:<a name="referencejsonexample"></a>

The following example demonstrates the use of attribute references in a JSON model\. The schema represented by this model is identical to the model above\. 

```
 {
  "facets" : {
    "baseFacet" : {
      "facetAttributes" : {
        "baseAttr" : {
          "attributeDefinition" : {
            "attributeType" : "STRING"
          },
          "requiredBehavior" : "NOT_REQUIRED"
        }
      },
      "objectType" : "DIRECTORY"
    },
    "facetA" : {
      "facetAttributes" : {
        "ref" : {
          "attributeReference" : {
            "targetFacetName" : "baseFacet",
            "targetAttributeName" : "baseAttr"
          },
          "requiredBehavior" : "REQUIRED_ALWAYS"
        }
      },
      " objectType" : "DIRECTORY"
    }
}
```

### Attribute reference considerations<a name="attributerefconsiderations"></a>

Attribute references must target a preexisting attribute definition in the same schema\.
+ Attribute references may target a preexisting attribute definition in the same facet or a different facet\.
+ Attribute references may not target other attribute references\.
+ Facets containing attribute definitions that are the target of another facet's attribute reference cannot be deleted until all references have been deleted\.

You can use attribute references the same way that you use traditional attribute definitions, by creating objects or applying facets to existing objects\.

**Note**  
You can apply facets with references to other facets but are not required to apply the target facets directly\. When the target facet is not applied, there is no change to the behavior of the attribute reference\. \(You need to apply target facets only when you want the other attributes on that facet to exist on the object\.\)

### Setting Attribute Reference Values<a name="settingattributerefvalues"></a>

You can call the [UpdateObjectAttributes](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_UpdateObjectAttributes.html) API action when you want to change the value of an attribute\. Updating \(or deleting\) either the definition or any other reference to that same definition on that object has the same effect\. 

### Getting Attribute Reference Values<a name="gettingattributerefvalues"></a>

You can call the [ListObjectAttributes](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_ListObjectAttributes.html) API action to retrieve storage aliases\. This call returns a list of tuples, each of which contains an attribute key and its associated value\. The attribute keys correspond to the list of storage aliases present on that object\.

**Note**  
It is possible for an attribute key to be returned for a facet that was not explicitly applied to an object\. This can happen when attribute references target facets that are not applied to the object\.

For example, imagine that you have a User facet and an EnterpriseUser facet\. The EnterpriseUser\.FirstName attribute refers to User\.FirstName\. You then apply both the User and EnterpriseUser facets to an object, set User\.FirstName to Robert, and later set EnterpriseUser\.FirstName to Bob\. When you call ListObjectAttributes you see only "User\.FirstName = Bob" since there is only one storage alias for both FirstName attributes\.

### Using Indexes with Attribute References<a name="usingindexeswithattributeref"></a>

You can can create indexes with an attribute definition only, not a reference\. Listing an index does not return attribute keys for attribute references\. But it does return attribute keys for any attribute definitions that are targeted by references existing on the indexed object\. In other words, at the index layer, attribute references are treated merely as an alternative identifier for an attribute, which gets resolved to the correct attribute definition identifier at runtime\.

For example, imagine you have an Index for facet User attribute FirstName\. You attach an object with only the EnterpriseUser facet applied\. You then set the value for that object's EnterpriseUser\.FirstName attribute to Bob\. Finally, you call ListIndex action\. The results contain only "User\.FirstName = Bob"\.

### Required Behavior for Attribute References<a name="requiredbehaviorattributeref"></a>

An attribute references can have a required behavior that is different from its target attribute definition\. This allows a base definition to be optional, while a reference to that same definition can be required\. When an object has a base definition and one or more references to the same base definition, the base definition and all references must adhere to the strongest required behavior present across all related attributes\.
+ As with attribute definitions, you must provide values for any required attribute definitions when you create the object or when you add a facet to an existing object\.
+ As a convenience, when more than one attribute on an object refers to the same storage location, you only need to provide a value for one of the attributes for that storage location\.
+ Similarly, if you do provide multiple values for the same storage location, the values must be equal\.
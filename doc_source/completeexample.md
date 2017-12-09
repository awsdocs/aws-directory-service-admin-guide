# Schema Document Examples<a name="completeexample"></a>

The following are samples of schema documents that show valid JSON formatting\.

**Note**  
All values expressed in the `allowedValues` string must be comma separated and be without spaces\. For example, `"SENSITIVE,CONFIDENTIAL,PUBLIC"`\.

## Basic Schema Document<a name="basicschema"></a>

```
{
  "facets" : {
    "Employee" : {
      "facetAttributes" : {
        "Name" : {
          "attributeDefinition" : {
            "attributeType" : "STRING",
            "isImmutable" : false,
            "attributeRules" : {
              "NameLengthRule" : {
                "parameters" : {
                  "min" : "3",
                  "max" : "100"
                },
                "ruleType": "STRING_LENGTH"
              }
            }
          },
          "requiredBehavior" : "REQUIRED_ALWAYS"
        },
        "EmailAddress" : {
          "attributeDefinition" : {
            "attributeType" : "STRING",
            "isImmutable" : true,
            "attributeRules" : {
              "EmailAddressLengthRule" : {
                "parameters" : {
                  "min" : "3",
                  "max" : "100"
                },
                "ruleType": "STRING_LENGTH"
              }
            }
          },
          "requiredBehavior" : "REQUIRED_ALWAYS"
        },
        "Status" : {
          "attributeDefinition" : {
            "attributeType" : "STRING",
            "isImmutable" : false,
            "attributeRules" : {
              "rule1" : {
                "parameters" : {
                  "allowedValues" : "ACTIVE,INACTIVE,TERMINATED"
                },
                "ruleType": "STRING_FROM_SET"
              }
            }
          },
          "requiredBehavior" : "REQUIRED_ALWAYS"
        }
      },
      "objectType" : "LEAF_NODE"
    },
    "DataAccessPolicy" : {
      "facetAttributes" : {
        "AccessLevel" : {
          "attributeDefinition" : {
            "attributeType" : "STRING",
            "isImmutable" : true,
            "attributeRules" : {
              "rule1" : {
                "parameters" : {
                  "allowedValues" : "SENSITIVE,CONFIDENTIAL,PUBLIC"
                },
                "ruleType": "STRING_FROM_SET"
              }
            }
          },
          "requiredBehavior" : "REQUIRED_ALWAYS"
        }
      },
      "objectType" : "POLICY"
    },
    "Group" : {
      "facetAttributes" : {
        "Name" : {
          "attributeDefinition" : {
            "attributeType" : "STRING",
            "isImmutable" : true
          },
          "requiredBehavior" : "REQUIRED_ALWAYS"
        }
      },
      "objectType" : "NODE"
    }
  }
}
```

## Schema Document with Typed Links<a name="schematyped"></a>

```
{
	"sourceSchemaArn": "",
	"facets": {
		"employee_facet": {
			"facetAttributes": {
				"employee_login": {
					"attributeDefinition": {
						"attributeType": "STRING",
						"isImmutable": true,
						"attributeRules": {}
					},
					"requiredBehavior": "REQUIRED_ALWAYS"
				},
				"employee_id": {
					"attributeDefinition": {
						"attributeType": "STRING",
						"isImmutable": true,
						"attributeRules": {}
					},
					"requiredBehavior": "REQUIRED_ALWAYS"
				},
				"employee_name": {
					"attributeDefinition": {
						"attributeType": "STRING",
						"isImmutable": true,
						"attributeRules": {}
					},
					"requiredBehavior": "REQUIRED_ALWAYS"
				},
				"employee_role": {
					"attributeDefinition": {
						"attributeType": "STRING",
						"isImmutable": true,
						"attributeRules": {}
					},
					"requiredBehavior": "REQUIRED_ALWAYS"
				}
			},
			"objectType": "LEAF_NODE"
		},
		"device_facet": {
			"facetAttributes": {
				"device_id": {
					"attributeDefinition": {
						"attributeType": "STRING",
						"isImmutable": true,
						"attributeRules": {}
					},
					"requiredBehavior": "REQUIRED_ALWAYS"
				},
				"device_type": {
					"attributeDefinition": {
						"attributeType": "STRING",
						"isImmutable": true,
						"attributeRules": {}
					},
					"requiredBehavior": "REQUIRED_ALWAYS"
				}
			},
			"objectType": "NODE"
		},
		"region_facet": {
			"facetAttributes": {},
			"objectType": "NODE"
		},
		"group_facet": {
			"facetAttributes": {
				"group_type": {
					"attributeDefinition": {
						"attributeType": "STRING",
						"isImmutable": true,
						"attributeRules": {}
					},
					"requiredBehavior": "REQUIRED_ALWAYS"
				}
			},
			"objectType": "NODE"
		},
		"office_facet": {
			"facetAttributes": {
				"office_id": {
					"attributeDefinition": {
						"attributeType": "STRING",
						"isImmutable": true,
						"attributeRules": {}
					},
					"requiredBehavior": "REQUIRED_ALWAYS"
				},
				"office_type": {
					"attributeDefinition": {
						"attributeType": "STRING",
						"isImmutable": true,
						"attributeRules": {}
					},
					"requiredBehavior": "REQUIRED_ALWAYS"
				},
				"office_location": {
					"attributeDefinition": {
						"attributeType": "STRING",
						"isImmutable": true,
						"attributeRules": {}
					},
					"requiredBehavior": "REQUIRED_ALWAYS"
				}
			},
			"objectType": "NODE"
		}
	},
	"typedLinkFacets": {
		"device_association": {
			"facetAttributes": {
				"device_type": {
					"attributeDefinition": {
						"attributeType": "STRING",
						"isImmutable": false,
						"attributeRules": {}
					},
					"requiredBehavior": "REQUIRED_ALWAYS"
				},
				"device_label": {
					"attributeDefinition": {
						"attributeType": "STRING",
						"isImmutable": false,
						"attributeRules": {}
					},
					"requiredBehavior": "REQUIRED_ALWAYS"
				}
			},
			"identityAttributeOrder": ["device_label", "device_type"]
		}
	}
}
```
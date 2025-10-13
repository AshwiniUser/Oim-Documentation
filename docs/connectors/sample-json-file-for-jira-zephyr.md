* Below is the sample JSON for Jira Zephyr entities. Based on your use case and Jira Zephyr instance configuration, the JSON needs to be modified.
  
```json
{
	"entities": [
		{
			"internalName": "testcase-zephyr",
			"displayName": "Zephyr Scale Test Case",
			"readMechanism": "NON_HISTORY",
			"hasReadSupport": true,
			"hasWriteSupport": true,
			"entityScope": "Global",
			"fields": {
				"system": [
					{
						"internalName": "name",
						"displayName": "Name",
						"dataType": "text",
						"mandatory": true,
						"historyEnabled": false
					},
					{
						"internalName": "id",
						"displayName": "Id",
						"dataType": "text",
						"mandatory": true,
						"historyEnabled": false,
						"readOnly": true
					},
					{
						"internalName": "key",
						"displayName": "Key",
						"dataType": "text",
						"mandatory": true,
						"historyEnabled": false,
						"readOnly": true
					},
					{
						"internalName": "project",
						"displayName": "Project",
						"dataType": "text",
						"mandatory": true,
						"historyEnabled": false
					},
					{
						"internalName": "createdOn",
						"displayName": "Created Date",
						"dataType": "date_string",
						"readOnly": true,
						"mandatory": false,
						"dateFormat": "yyyy-MM-dd'T'HH:mm:ss'Z'",
						"historyEnabled": false
					},
					{
						"internalName": "component",
						"displayName": "Component",
						"dataType": "lookup",
						"mandatory": false,
						"multiselect": false,
						"historyEnabled": false
					},
					{
						"internalName": "objective",
						"displayName": "Objective",
						"dataType": "html",
						"mandatory": false,
						"historyEnabled": false
					},
					{
						"internalName": "precondition",
						"displayName": "Precondition",
						"dataType": "html",
						"mandatory": false,
						"historyEnabled": false
					},
					{
						"internalName": "estimatedTime",
						"displayName": "Estimated run time",
						"dataType": "numeric",
						"mandatory": false,
						"historyEnabled": false
					},
					{
						"internalName": "labels",
						"displayName": "Labels",
						"dataType": "text",
						"multiselect": true,
						"mandatory": false,
						"historyEnabled": false
					},
					{
						"internalName": "priority",
						"displayName": "Priority",
						"dataType": "lookup",
						"mandatory": true,
						"multiselect": false,
						"historyEnabled": false
					},
					{
						"internalName": "status",
						"displayName": "Status",
						"dataType": "lookup",
						"mandatory": true,
						"multiselect": false,
						"historyEnabled": false
					},
					{
						"internalName": "owner",
						"displayName": "Owner",
						"dataType": "user",
						"mandatory": false,
						"historyEnabled": false
					},
					{
						"internalName": "folder",
						"displayName": "Folder",
						"dataType": "reference",
						"systemSpecific": {
							"referencedEntityType": "folder-zephyr"
						}
					},
					{
						"internalName": "OH_Folder_Path",
						"displayName": "OH_Folder_Path",
						"dataType": "text"
					},
					{
						"internalName": "OH_Test_Steps",
						"displayName": "Test Steps",
						"dataType": "test-step",
						"mandatory": false,
						"historyEnabled": false
					}
				],
				"custom": [
                		    {
                                "internalName": "CustomText",
                            	"displayName": "CustomText",
                            	"dataType": "text",
                            	"mandatory": true
                            }
                		]
			}
		},
		{
			"internalName": "folder-zephyr",
			"displayName": "Zephyr Scale Test Folder",
			"readMechanism": "NON_HISTORY",
			"hasReadSupport": true,
			"hasWriteSupport": true,
			"entityScope": "Global",
			"fields": {
				"system": [
					{
						"internalName": "name",
						"displayName": "Name",
						"dataType": "text",
						"mandatory": true,
						"historyEnabled": false
					},
					{
						"internalName": "id",
						"displayName": "Id",
						"dataType": "text",
						"mandatory": true,
						"historyEnabled": false,
						"readOnly": true
					},
					{
						"internalName": "project",
						"displayName": "Project",
						"dataType": "text",
						"mandatory": true,
						"historyEnabled": false
					},
					{
						"internalName": "folderType",
						"displayName": "Folder Type",
						"dataType": "lookup",
						"mandatory": true,
						"multiselect": false,
						"historyEnabled": false,
						"lookUpValues": {
							"TEST_CASE": "TEST_CASE",
							"TEST_CYCLE": "TEST_CYCLE",
							"TEST_PLAN": "TEST_PLAN"
						}
					},
					{
						"internalName": "index",
						"displayName": "Index",
						"dataType": "text",
						"mandatory": true,
						"historyEnabled": false
					}
				]
			}
		},
		{
			"internalName": "testcycle-zephyr",
			"displayName": "Zephyr Scale Test Cycle",
			"readMechanism": "NON_HISTORY",
			"hasReadSupport": true,
			"hasWriteSupport": true,
			"entityScope": "Global",
			"fields": {
				"system": [
					{
						"internalName": "name",
						"displayName": "Name",
						"dataType": "text",
						"mandatory": true,
						"historyEnabled": false
					},
					{
						"internalName": "id",
						"displayName": "Id",
						"dataType": "text",
						"mandatory": true,
						"historyEnabled": false,
						"readOnly": true
					},
					{
						"internalName": "key",
						"displayName": "Key",
						"dataType": "text",
						"mandatory": true,
						"historyEnabled": false,
						"readOnly": true
					},
					{
						"internalName": "project",
						"displayName": "Project",
						"dataType": "text",
						"mandatory": true,
						"historyEnabled": false
					},
					{
						"internalName": "plannedStartDate",
						"displayName": "Planned start date",
						"dataType": "date_string",
						"mandatory": true,
						"dateFormat": "yyyy-MM-dd'T'HH:mm:ss'Z'",
						"historyEnabled": false
					},
					{
						"internalName": "plannedEndDate",
						"displayName": "Planned end date",
						"dataType": "date_string",
						"mandatory": true,
						"dateFormat": "yyyy-MM-dd'T'HH:mm:ss'Z'",
						"historyEnabled": false
					},
					{
						"internalName": "description",
						"displayName": "Description",
						"dataType": "html",
						"mandatory": false,
						"historyEnabled": false
					},
					{
						"internalName": "folder",
						"displayName": "Folder",
						"dataType": "reference",
						"systemSpecific": {
							"referencedEntityType": "folder-zephyr"
						}
					},
					{
						"internalName": "jiraProjectVersion",
						"displayName": "Jira Project Version",
						"dataType": "lookup",
						"mandatory": false,
						"multiselect": false,
						"historyEnabled": false
					},
					{
						"internalName": "status",
						"displayName": "Status",
						"dataType": "lookup",
						"mandatory": true,
						"multiselect": false,
						"historyEnabled": false
					},
					{
						"internalName": "owner",
						"displayName": "Owner",
						"dataType": "user",
						"mandatory": false,
						"historyEnabled": false
					},
					{
						"internalName": "OH_Folder_Path",
						"displayName": "OH_Folder_Path",
						"dataType": "text"
					}
				]
			}
		},
		{
			"internalName": "testplan-zephyr",
			"displayName": "Zephyr Scale Test Plan",
			"readMechanism": "NON_HISTORY",
			"hasReadSupport": true,
			"hasWriteSupport": true,
			"systemSpecific": {
				"readCustomFieldsMeta": true
			},
			"entityScope": "Global",
			"fields": {
				"system": [
					{
						"internalName": "name",
						"displayName": "Name",
						"dataType": "text",
						"mandatory": true,
						"historyEnabled": false
					},
					{
						"internalName": "id",
						"displayName": "Id",
						"dataType": "text",
						"mandatory": true,
						"historyEnabled": false,
						"readOnly": true
					},
					{
						"internalName": "key",
						"displayName": "Key",
						"dataType": "text",
						"mandatory": true,
						"historyEnabled": false,
						"readOnly": true
					},
					{
						"internalName": "project",
						"displayName": "Project",
						"dataType": "text",
						"mandatory": true,
						"historyEnabled": false
					},
					{
						"internalName": "objective",
						"displayName": "Objective",
						"dataType": "html",
						"mandatory": false,
						"historyEnabled": false
					},
					{
						"internalName": "labels",
						"displayName": "Labels",
						"dataType": "text",
						"multiselect": true,
						"mandatory": false,
						"historyEnabled": false
					},
					{
						"internalName": "status",
						"displayName": "Status",
						"dataType": "lookup",
						"mandatory": true,
						"multiselect": false,
						"historyEnabled": false
					},
					{
						"internalName": "folder",
						"displayName": "Folder",
						"dataType": "reference",
						"systemSpecific": {
							"referencedEntityType": "folder-zephyr"
						}
					},
					{
						"internalName": "owner",
						"displayName": "Owner",
						"dataType": "user",
						"mandatory": false,
						"historyEnabled": false
					},
					{
						"internalName": "OH_Folder_Path",
						"displayName": "OH_Folder_Path",
						"dataType": "text"
					}
				]
			}
		},
		{
			"internalName": "testexecution-zephyr",
			"displayName": "Zephyr Scale Test Execution",
			"readMechanism": "NON_HISTORY",
			"hasReadSupport": true,
			"hasWriteSupport": true,
			"entityScope": "Global",
			"fields": {
				"system": [
					{
						"internalName": "id",
						"displayName": "Id",
						"dataType": "text",
						"mandatory": true,
						"historyEnabled": false,
						"readOnly": true
					},
					{
						"internalName": "key",
						"displayName": "Key",
						"dataType": "text",
						"mandatory": true,
						"historyEnabled": false,
						"readOnly": true
					},
					{
						"internalName": "project",
						"displayName": "Project",
						"dataType": "text",
						"mandatory": true,
						"historyEnabled": false
					},
					{
						"internalName": "jiraProjectVersion",
						"displayName": "Jira Project Version",
						"dataType": "lookup",
						"mandatory": false,
						"multiselect": false,
						"historyEnabled": false
					},
					{
						"internalName": "testExecutionStatus",
						"displayName": "Execution Status ",
						"dataType": "lookup",
						"mandatory": true,
						"multiselect": false,
						"historyEnabled": false
					},
					{
						"internalName": "actualEndDate",
						"displayName": "Actual End Date",
						"dataType": "date_string",
						"mandatory": true,
						"dateFormat": "yyyy-MM-dd'T'HH:mm:ss'Z'",
						"historyEnabled": false
					},
					{
						"internalName": "estimatedTime",
						"displayName": "Estimated Time",
						"dataType": "numeric",
						"mandatory": false,
						"historyEnabled": false
					},
					{
						"internalName": "executionTime",
						"displayName": "Execution Time",
						"dataType": "numeric",
						"mandatory": false,
						"historyEnabled": false
					},
					{
						"internalName": "executedById",
						"displayName": "Executed by",
						"dataType": "user",
						"mandatory": false,
						"historyEnabled": false
					},
					{
						"internalName": "assignedToId",
						"displayName": "Assigned To",
						"dataType": "user",
						"mandatory": false,
						"historyEnabled": false
					},
					{
						"internalName": "comment",
						"displayName": "Comment",
						"dataType": "html",
						"multiselect": false,
						"mandatory": false,
						"historyEnabled": false
					},
					{
						"internalName": "automated",
						"displayName": "Automated",
						"dataType": "boolean",
						"multiselect": false,
						"mandatory": true,
						"historyEnabled": false
					},
					{
						"internalName": "environment",
						"displayName": "Environment",
						"dataType": "reference",
						"systemSpecific": {
							"referencedEntityType": "environment-zephyr"
						}
					},
					{
						"internalName": "testCase",
						"displayName": "Test Case",
						"dataType": "reference",
						"systemSpecific": {
							"referencedEntityType": "testcase-zephyr"
						}
					},
					{
						"internalName": "testCycle",
						"displayName": "Test Cycle",
						"dataType": "reference",
						"systemSpecific": {
							"referencedEntityType": "testcycle-zephyr"
						}
					}
				]
			}
		},
		{
			"internalName": "environment-zephyr",
			"displayName": "Test Environment",
			"readMechanism": "NON_HISTORY",
			"hasReadSupport": true,
			"hasWriteSupport": true,
			"entityScope": "Global",
			"fields": {
				"system": [
					{
						"internalName": "id",
						"displayName": "Id",
						"dataType": "text",
						"mandatory": true,
						"historyEnabled": false,
						"readOnly": true
					},
					{
						"internalName": "project",
						"displayName": "Project",
						"dataType": "text",
						"mandatory": true,
						"historyEnabled": false
					},
					{
						"internalName": "name",
						"displayName": "Name",
						"dataType": "text",
						"multiselect": false,
						"mandatory": true,
						"historyEnabled": false
					},
					{
						"internalName": "description",
						"displayName": "Description",
						"dataType": "text",
						"multiselect": false,
						"mandatory": false,
						"historyEnabled": false
					},
					{
						"internalName": "archived",
						"displayName": "Archived",
						"dataType": "boolean",
						"multiselect": false,
						"mandatory": true,
						"historyEnabled": false
					},
					{
						"internalName": "index",
						"displayName": "Index",
						"dataType": "numeric",
						"mandatory": true,
						"historyEnabled": false
					}
				]
			}
		}
	]
}
```

* This template lists the system fields for each entity supported by the Zephyr plugin.
* Users can add custom field metadata after the system field metadata.
* The final JSON for an entity with custom fields will appear as follows:

```json
{
	"internalName": "Entity Internal ID",
	"displayName": "Entity Display ID",
	"readMechanism": "NON_HISTORY",
	"hasReadSupport": true,
	"hasWriteSupport": true,
	"entityScope": "Global",
	"fields": {
		"system": [
			{
				"internalName": "field1",
				"displayName": "Field1",
				"dataType": "text",
				"mandatory": true,
				"historyEnabled": false,
				"readOnly": true
			},
			{
				"internalName": "field2",
				"displayName": "Field2",
				"dataType": "text",
				"mandatory": true,
				"historyEnabled": false
			}
		],
		"custom": [
		    {
                "internalName": "field1",
            	"displayName": "Field1",
            	"dataType": "text",
            	"mandatory": true
            },
            {
            	"internalName": "field2",
       			"displayName": "Field2",
       			"dataType": "text",
            	"mandatory": true
            }
		]
	}
}
```

# Test Plan Specific JSON Input
* Additional fields need to be included in the JSON for Test Plans:
  * At the field level: Add the system-specific field requestFieldKey in the system-specific map for all custom fields.
      * This is used by OpsHub Integration Manager to update Test Plan custom fields via a private API.
      * The value of requestFieldKey can be obtained by inspecting the private update API of the Test Plan from the browser for each field.
* At the entity level: Add the system-specific field readCustomFieldsMeta in the metadata to define whether OpsHub Integration Manager can use the private API to load custom field information.
  * Default value: true (can be explicitly set to false).
  * If set to false, the custom field ID must be provided manually.
  * Since updates for Test Plans use a private API (which requires the custom field ID), the value of readCustomFieldsMeta determines whether this ID is auto-fetched or must be provided manually.
  * Example JSON for a Test Plan with readCustomFieldsMeta set to true:
    
  ```json
  {
	"internalName": "testplan-zephyr",
	"displayName": "Zephyr Scale Test Plan",
	"readMechanism": "NON_HISTORY",
	"hasReadSupport": true,
	"hasWriteSupport": true,
	"systemSpecific": {
	"readCustomFieldsMeta": true
	},
	"entityScope": "Global",
	"fields": {
	    "system": [...System Fields Meta as mentioned in the template...],
	    "custom": [
	        {
                "internalName": "customNumber",
            	"displayName": "customNumber",
            	"dataType": "numeric",
            	"multiselect": false,
            	"mandatory": false,
            	"historyEnabled": false,
            	"systemSpecific": {
            	    "requestFieldKey": "intValue"
                }
            }
	    ]
	}
}
```

* The JSON for a Test Plan when readCustomFieldsMeta is false will be as follows:
```json
{
	"internalName": "testplan-zephyr",
	"displayName": "Zephyr Scale Test Plan",
	"readMechanism": "NON_HISTORY",
	"hasReadSupport": true,
	"hasWriteSupport": true,
	"systemSpecific": {
		"readCustomFieldsMeta": false
	},
	"entityScope": "Global",
	"fields": {
		"system": (...System Fields Meta as mentioned in the template...),
		"custom": [
			{
				"internalName": "customSelect",
				"displayName": "customSelect",
				"dataType": "lookup",
				"mandatory": false,
				"multiselect": false,
				"historyEnabled": false,
				"lookUpValues": {
					"s1": "2331664",
					"s2": "2331665"
				},
				"systemSpecific": {
					"customFieldId": "508083",
					"requestFieldKey": "intValue"
				}
			},
			{
				"internalName": "customText",
				"displayName": "customText",
				"dataType": "text",
				"multiselect": false,
				"mandatory": false,
				"historyEnabled": false,
				"systemSpecific": {
					"customFieldId": "508081",
					"requestFieldKey": "stringValue"
				}
			}
		]
	}
}
```

* In the above JSON, the custom ID for each custom field should be specified in the systemSpecific map.
* Users must also provide the internal IDs for the lookup field values.

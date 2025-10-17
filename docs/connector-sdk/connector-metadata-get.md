# Overview
Returns connector metadata information using which OpsHub will register this connector in OpsHub. The features and fields provided here are what users will see on OpsHub UI when configuring integration with this connector.

# API URI
This is the URI, OpsHub will execute to call this API:
```bash
GET: /connector-metadata
```

# Response Payload
```json
{ 

  "enableFeatures": [ 

    "CURRENT_STATE_SYNC_FLAG", 

    "REMOTE_ID_LINK", 

    "TARGET_LOOKUP", 

    "CRITERIA",

    "MAPPED_DATA_RETRIEVAL"

  ],

  "additionalMetadata":

      {

        "userSearchOnUserNameSupported": "<Does the connector support searching for users by username>",

        "userSearchOnEmailSupported": "<Does the connector support searching for users by email>"

      }

    ,


  "fields": [

    {

      "internalName": "<user input field internal name>",

      "displayName": "<user input field display name>",

      "tooltip": "<tool tip>",

      "required": true,

      "fieldType": "ENUM",

      "lookup": {

        "staticValues": [

          {

            "internalName": "<internal name or id of lookup value>",

            "displayName": "<display name>"

          }

        ],

        "dynamicLookupKey": null

      },

      "defaultValue": null,

      "validation": null,

      "fieldOrder": 1,

      "parent": null,

      "screens": [

        "SYSTEM_CONFIG",

        "INTEGRATION_SOURCE_CONFIG",

        "INTEGRATION_TARGET_CONFIG"

      ]

    }

  ]

}
```

# Response Parameters

| Parent Parameter       | Name                           | Required | Type             | Description |
|------------------------|--------------------------------|---------|-----------------|-------------|
|  | enableFeatures   | True    | ENUM   | List of features to be enabled in OIM:<br><br>**CURRENT_STATE_SYNC_FLAG**: A flag to enable integration sync only latest entity state. Applies only for entity types with `"pollerType": "ENTITY_WISE_HISTORY"`. Refer to [Sync only current state](../Integration_Configuration#Sync_Only_Current_State) for details.<br>**REMOTE_ID_LINK**: Stores id and link of an entity of other system. To form the link using a URL other than connector's server URL, enter in "Base URL for Remote Link" field. See [Remote Id and Link](../Integration_Configuration#Tracking_Id_and_Link_of_Entities_Across_Systems).<br>**TARGET_LOOKUP**: Search entity in target system before sync. See [Target Lookup](../Integration_Configuration#Search_in_Target_Before_Sync).<br>**CRITERIA**: Sync only subset of entities meeting criteria/condition. See [Criteria Configuration](../Integration_Configuration#Criteria_Configuration).<br>**MAPPED_DATA_RETRIEVAL**: Enables "fetch mapped data only" feature if end system supports fetching specific fields. |
| additionalMetadata     | | False | | |
| | userSearchOnUserNameSupported  | False   | boolean          | Does the connector support user search based on userName?<br>Default is false. If connector allows search by username, provide as true. |
| | userSearchOnEmailSupported     | False   | boolean          | Does the connector support user search based on email?<br>Default is false. If connector allows search by email, provide as true. |
| fields                 | | True | | |
|  | internalName                   | True    | string           | Internal name of the user input. Must be unique. E.g., `authType`, `userName`. |
|  | displayName                    | True    | string           | Display name shown in OpsHub UI. E.g., `Authentication Type`, `User Name`. |
|  | tooltip                        | False   | string           | Help text for the field. E.g., “Provide a URL to connect to end system. Format: https://host/ Example: https://www.example.com/”. |
|  | required                       | True    | boolean          | Is the user input mandatory? `true` / `false`. |
|  | fieldType                      | True    | ENUM             | Input types:<br>- TEXT_BOX<br>- TEXT_AREA<br>- DROP_DOWN<br>- PASSWORD<br>- RADIO_BUTTON<br>- CHECKBOX<br>- URL<br>- EMAIL<br>- NUMERIC<br>- MULTI_SELECT_DROP_DOWN_WITH_CHECKBOX<br>- JSON<br>- XML |
| Fields.lookup | | False | | For any DROP_DOWN type inputs. The user needs to provide lookup values to show the options in drop down |
|  | staticValues                   | Conditional | List of Objects | Static values for dropdown. E.g., “1=Basic,2=Token Based”. Order determines UI display order. |
|  | staticValues.internalName      |         | string           | Internal id of lookup. E.g., 1, 2, 3. |
|  | staticValues.displayName       |         | string           | Display name in dropdown. E.g., Basic, Token Based. |
|  | dynamicLookupKey               | Conditional | ENUM            | Dynamic lookup options:<br>- ALL_SYSTEM: List of all the systems that exists in OIM<br>- ALM_SYSTEM: List of all the ALM systems created by user in OIM. This will not fetch any SCM system <br>- TIME_ZONE: Pre-defined list of available time zones<br>- ENTITY_FIELDS:  Dynamically displays the list of available fields of an entity from end system API. This type of dynamic lookup is used when list of available fields for an entity is to be displayed.<br>- DATABASE_TYPE: List of all database types supported in Database System. |
| Fields. validation| | False | | Validation to be applied on any textual field|
|  | name                           | False   | string           | Name of validation. E.g., “System Version Validation”. |
|  | regex                          | False   | string           | Regex to validate field value. E.g., `[1-9]{1,2}\.[0-9]{1,2}\.[0-9]{1,2}`. |
|  | failureMessage                 | False   | string           | Message shown if validation fails. E.g., “Please provide valid version in form of x.y.z”. |
| fields | | | | 
| fields                 | fieldOrder                     | True    | number           | UI order of field. |
| parent | | False | | It’s to support hierarchy of the fields. <br>E.g., ‘authType’ can be parent of ‘userName’, ‘password’ and ‘token’ |
|  | internalName                   | False   | string           | Internal name of the parent field.<br>E.g., `'issueType'` is a built-in field. There is no need to provide metadata configuration for `'issueType'` field in JSON.<br>E.g., For username or password field, `auth_type` can be the internalName for parent field. |
|  | fieldValues                    | False   | string           | Internal value of the parent field. Current field will only be loaded if parent field’s value matches the given value.<br>E.g., If `authType` has values “1=Basic,2=Token Based”, provide `1` to select Basic as parent field value.<br><br>Some fields can be loaded only if a particular parent field value is selected.<br>E.g., If `authType` is parent of `userName`, `password`, and `token` fields:<br>- `password` will only be loaded if `authType` value is `Basic`.<br>- `token` will only be loaded if `authType` value is `Token Based`. |
|  | fieldRegex                     | False   | string           | Regex controlling visibility of current field based on parent field value. |
| fields | | | |  
|                  | screens  | True    | ENUM  | List of screens where this field should be visible:<br>- SYSTEM_CONFIG: System configuration screen <br>- INTEGRATION_SOURCE_CONFIG: Advanced integration config when connector is source
<br>- INTEGRATION_TARGET_CONFIG: Advanced integration config when connector is target |



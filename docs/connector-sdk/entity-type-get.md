## Overview
This API describes the entity type in detail for OpsHub to be able to integrate various basic and complex data for a given entity type.  
>**Note**: It is important to return a correct response for this API as OpsHub relies heavily on these inputs to handle multiple connector tasks automatically.

## API URI
This is the URI OpsHub will execute to call this API:

```bash
GET: /entity-types/{entityTypeId}?projectId=<projectId>
```

## URI Parameters

| Name | In | Required | Type | Description |
|------|----|----------|------|-------------|
| entityTypeId | path | True | String | ‘id’ of entity type returned as response of Entity Type – List API |
| projectId | query | True | String | Project id for which entity type details need to be returned. ProjectId here will be the same as ‘id’ sent as part of `/projects` |

## Response Payload
```json

{

  "multiStepUpdate": "NO_SUB_STEPS, STATIC_SUB_STEPS, DYNAMIC_SUB_STEPS",

  "recovery": {

    "type": "FIELD_BASED, COMPARISON_BASED, HISTORY_BASED",

    "fieldName": "// If FIELD_BASED, then id of the field to store last update date"

  },

  "history": {

    "type": "FIELD_BASED, FULL_STATE_BASED",

    "revisionDateFormat": "dd/MM/YYYY’T’hh:mm:ss.SSSz",

    "isRevisionIdNumeric": "true/false | datatype: boolean",

    "revisionUserDataType": "USERNAME_AS_USER, EMAIL_AS_USER",

    "separateHistoryApis": "ATTACHMENTS, COMMENTS, LINKS",

    "sortableFields":"CREATED_UPDATED_TIME, ENTITY_ID, REVISION_ID"

  },

  "enitytScope": {

    "additionalScopeFieldName": "field id used as additional scope"

  },

  "entityWebUrl": {

    "baseUrl": "https://example.com/",

    "trailingTemplate": "browse/{0}/{1}",

    "substitutes": {

      "0": "field id of the field whose value need to be first replacement",

      "1": "field name of second replacement field"

    }

  },

  "isFieldIdConstantAcrossProjects": "true/false | datatype: boolean",

  "isInternalValueExistForLookupField": "true/false | datatype: boolean",

  "isUpdateAvailable": "true/false | datatype: boolean",

  "waitTimeInMillisIfApiResponseDelayed": "Max delay in API response in milli seconds. | datatype: number",

  "searchEntityInfo": {

    "sortableFields": "CREATED_UPDATED_TIME, ENTITY_ID, REVISION_ID",

    "isGroupingSupported": "true / false",

    "isSearchPossibleOnAnyField": "true / false",

    "isCriteriaInSystemNativeFormat": "true / false",

    "dateTimeFormat": "dd/MM/YYYY’T’hh:mm:ss.SSSz",

    "queryFieldNameInfo": {

      "entityIdFieldName": "entity id field id",

      "entityTypeIdFieldName": "entity type field id",

      "projectIdFieldName": "project id’s field id",

      "createdDateFieldName": "created date’s field id",

      "updatedDateFieldName": "updated date’s field id",

      "createdByFieldName": "created By’s field id"

    },

    "batchSizeForInQuery": "number of entities that can be passed in 'IN' or 'OR' query"

  },

  "fieldNameInfo": {

    "entityIdFieldName": "field id of unique and uneditable entity primary id field",

    "entityTitleFieldName": "field id for entity title",

    "entityDisplayIdFieldName": "field id of field that has entity display id (id any)",

    "entityTypeIdFieldName": "field id for entity type",

    "projectIdFieldName": "field id of field that contains project info for entity",

    "createdDateFieldName": "field id of Created date field",

    "updatedDateFieldName": "field id of updated date field",

    "createdByFieldName": "field id of created By field",

    "updatedByFieldName": "field id of updated By field",

    "archiveMetadata" : {
	
	"archivedByFieldName": "field id of archived By field",

	"isArchivedFieldName": "field id of is Archived field"

     }
	

  },

  "fields": [

    {

      "id": "unique id or key for each field",

      "name": "Field name",

      "dataType": "TEXT, HTML, WIKI, LOOKUP, DATE, DATE_TIME, DATE_STRING, BOOLEAN, NUMBER, USERNAME_AS_USER, TIME_UNIT, EMAIL_AS_USER, RTF, HYPERLINK, TEST_STEP, PARAMETER, REFERENCE, IMAGE, HIERARCHY",

      "isMandatory": "true/false | datatype: boolean",

      "isMultiSelect": "true/false | datatype: boolean",

      "isReadOnly": "true/false | datatype: boolean",

      "isHistorySupported": "true/false | datatype: boolean",

      "userMentionSupported": "true/false | datatype: boolean",

      "entityMentionSupported": "true/false | datatype: boolean",

      "timeUnit": "MILLISECOND, SECOND, MINUTE, HOUR, DAY",

      "dateFormat": " yyyy-MM-dd or yyyy-MM-dd’T’HH:mm:ss.SSSz",

      "canBeSetAtEntityCreateTime": "true/false | datatype:boolean",

      "updateStepNumber": "// Number starting with 1,2,3",
  
      "referenceFieldMetadata": {
	
		"referencedEntityTypeId: "id of the entity type which is referenced through field"

		"idFieldName": "id field name which stores id or URL of the referenced entity in Entity - GET API and History - List API for base entity"

		"referenceUrl": {

			 "baseUrl": "https://example.com/",

			 "trailingTemplate": "browse/{0}/{1}",

   			 "substitutes": {

     	 			"0": "field id of the field whose value need to be first replacement",

      				"1": "field id of the field whose value need to be second replacement"

    			}

		}

		"titleFieldName": "title field name which stores title or equivalent field of the referenced entity in the Entity - GET API and History - List API for base entity"        

       }

    },

    {

      "id": "unique id or key for each field",

      "name": "Field name",

      "dataType": "TEXT, HTML, WIKI, LOOKUP, DATE, DATE_TIME, DATE_STRING, BOOLEAN, NUMBER, USERNAME_AS_USER, TIME_UNIT, EMAIL_AS_USER, RTF, HYPERLINK, TEST_STEP, PARAMETER, REFERENCE, IMAGE, HIERARCHY",

      "isMandatory": "true/false | datatype: boolean",

      "isMultiSelect": "true/false | datatype: boolean",

      "isReadOnly": "true/false | datatype: boolean",

      "isHistorySupported": "true/false | datatype: boolean",

      "userMentionSupported": "true/false | datatype: boolean",

      "timeUnit": "MILLISECOND, SECOND, MINUTE, HOUR, DAY",

      "dateFormat": "yyyy-MM-dd or yyyy-MM-dd’T’HH:mm:ss.SSSz",

      "canBeSetAtEntityCreateTime": "true/false | datatype:boolean",

      "updateStepNumber": "// Number starting with 1,2,3",
  
      "referenceFieldMetadata": {
	
		"referencedEntityTypeId: "id of the entity type which is referenced through field"

		"idFieldName": "id field name which stores id or URL of the referenced entity in Entity - GET API and History - List API for base entity"

		"referenceUrl": {

			 "baseUrl": "https://example.com/"

			 "trailingTemplate": "browse/{0}/{1}",

   			 "substitutes": {

     	 			"0": "field id of the field whose value need to be first replacement",

      				"1": "field id of the field whose value need to be second replacement"

    			}

		}

		"titleFieldName": "title field name which stores title or equivalent field of the referenced entity in the Entity - GET API and History - List API for base entity"        

       }


    }

  ],

  "comments": {

    "userMentionSupported": "true/false | datatype: boolean",

    "entityMentionSupported": "true/false | datatype: boolean",

    "commentBodyDataType": "TEXT, HTML, WIKI",

    "commentIdDataType": "NUMBER, TEXT",

    "createdUpdatedByFieldDataType": "USERNAME_AS_USER, EMAIL_AS_USER"

    "htmlReplacementForNewLine": "<br/> or \n or null",

    "delayInCommentUpdateTimeInMillis": 2000,

    "createUpdateDateFormat": "yyyy-MM-dd'T'HH:mm:ss.SSSZ",

    "typesOfComments": [

      "Private",

      "Public",

      "etc."

    ],

    "fieldNameInfo": {

      "idFieldName": "Field name of comment id as it is received in API by end system",

      "titleFieldName": " Field name of comment title as it is received in API by end system ",

      "bodyFieldName": " Field name of comment body as it is received in API by end system ",

      "createdDateFieldName": " Field name of comment created date as it is received in API by end system ",

      "updatedDateFieldName": " Field name of comment updated date as it is received in API by end system ",

      "createdByFieldName": " Field name of comment created by as it is received in API by end system ",

      "updatedByFieldName": " Field name of comment updated by as it is received in API by end system ",

      "commentTypeFieldName": " Field name of comment type as it is received in API by end system "

    }

  },

  "attachments": {

    "updateSupported": "true/false | datatype: boolean",

    "deleteSupported": "true/false | datatype: boolean",

    "historySupported": "true/false | datatype: boolean",

    "createUpdateDateFormat": "yyyy-MM-dd'T'HH:mm:ss.SSSZ",

    "typesOfAttachments": [

      "Internal",

      "External",

      "etc."

    ],

    "fieldNameInfo": {

      "idFieldName": " Field name of attachment id as it is received in API by end system ",

      "contentUriFieldName": " Field name of attachment content URI as it is received in API by end system ",

      "renderUriFieldName": " Field name of attachment render URI as it is received in API by end system ",

      "fileNameFieldName": " Field name of attachment file name as it is received in API by end system ",

      "contentTypeFieldName": " Field name of attachment content type as it is received in API by end system ",

      "contentLengthFieldName": " Field name of attachment length as it is received in API by end system ",

      "createdOrUpdatedDateFieldName": " Field name of attachment updated as it is received in API by end system ",

      "createdByFieldName": " Field name of attachment created by as it is received in API by end system ",

      "attachmentTypeFieldName": " Field name of attachment type as it is received in API by end system ",

      "fileCommentFieldName": " Field name of the attachment file comment as it is received in API by end system "

    }

  },

  "inlineFiles": {

    "deleteSupported": "true/false | datatype: boolean",

    "inlineFileStorageType": "ENTITY_LEVEL_STORAGE | EXTERNAL_STORAGE",

    "inlineFileUrlPrefix": ""

  },

  "links": {

    "deleteSupported": "true/false | datatype: boolean",

    "historySupported": "true/false | datatype: boolean",

    "createUpdateDateFormat": "yyyy-MM-dd'T'HH:mm:ss.SSSZ",

    "rank": {

        "rankType": "FLAT_SINGLE | FLAT_MULTIPLE | HIERARCHY_SINGLE | HIERARCHY_MULTIPLE",

        "supportedRankOperations": [

            "MOVE_BEFORE",

            "MOVE_AFTER",

            "LAST_IN_LIST",

            "MOVE_BULK_AFTER"
        ],

        "rankFieldName": "If entity stores the rank info in a field, provide that field name.",

        "rankScope": {

            "template": "{0}::{1}",

            "substitutes": {

                "0": "field name of the field whose value needs to be replacement for 0",

                "1": "field name of the field whose value needs to be replacement for 1"

            }

        }

    },

    "linkTypes": [

      {

        "linkType": "",

        "reverseLinkType": "",

        "isMultiLinkAllowed": "true/false | datatype: boolean",

        "isLinkMandatory": "true/false | datatype: boolean",

        "isBulkLinkingSupported": "true/false | datatype: boolean",

        "isExternalLink": "true/false | datatype: boolean"

      }

    ],

    "fieldNameinfo": {

      "linkTypeFieldName": " Field name of link type (parent, child, related etc.) as it is received in API by end system ",

      "linkedEntityIdFieldName": " Field name of linked entity id as it is received in API by end system ",

      "linkedEntityTypeFieldName": " Field name of linked entity type as it is received in API by end system ",

      "linkedEntityScopeIdFieldName": "linkedEntityScopeId | TODO: Revisit this",

      "createdDateFieldName": " Field name of link created date as it is received in API by end system ",

      "createdByFieldName": " Field name of link created by user as it is received in API by end system ",

      "linkCommentFieldName": " Field name of link comment as it is received in API by end system ",

      "externalLinkUrlFieldName": " Field name of link external URL as it is received in API by end system ",

      "isExternalLinkFieldName": " Field name of field which says if it’s an external link or not, as it is received in API by end system "

    }

  },

"userMention": {

    "userMentionDataType": "USERNAME_AS_USER / EMAIL_AS_USER",

    "mentionDetails": [

      {

        "fieldDataType": "HTML",

        "selectorOrRegex": ["Example: a[href]"],

        "mentionTemplate": "Example: <a href=\"https://example.com/users/${username}\" rel=\"${username}\"> ${displayName} </a>",

        "userDataRegex": "",

        "userDataAttributeName": "Example: href / rel / data-mention"

      },

      {

        "fieldDataType": "WIKI",

        "selectorOrRegex": "Example: [~ohusermention:(.*?)]",

        "mentionTemplate": "Example: [~accountId:${username}]"

      },

      {

        "fieldDataType": "TEXT",

        "selectorOrRegex": "Example: @OH_USER@ohusermention:(.*?)@OH_USER@",

        "mentionTemplate": "Example: ${username} <${email}>"

      }

    ]

  },

  "entityMention": {

      "mentionDetails": [

        {

          "fieldDataType": "HTML",

          "selectorOrRegex": ["Example: a[href]"],

          "mentionTemplate": "Example: <a href=\"https://example.com/users/${username}\" rel=\"${username}\"> ${displayName} </a>",

          "entityIdAttribute": {

            "dataAttributeName": "href",

            "dataRegEx": "/browse/([A-Z_a-z0-9-]+)"
          },

          "entityTypeAttribute": {

            "dataAttributeName": "href",

            "dataRegEx": ".*\\?detail=/(.*?)(?=/\\d+)"
          },

          "entityProjectAttribute": {

            "dataAttributeName": "href",

            "dataRegEx": ".*([a-f0-9]{8}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{12})/_workitems/edit/.*"
          }

        }

      ],
      "entityURLDetails": [

       {
          "entityWebURLMatcher": "a[href~=/browse/[A-Z_a-z0-9-]+-\\d+]",

          "entityIdDataSelector": ".*\\/browse/([A-Za-z0-9-]+-\\d+)]"
       }

      ]

    }

}
```
> **Internal note:** For attachment, comment, link: `readSupported`, `writeSupported` can be derived from sync direction of entityType.

# Response Parameters

| **Parent Parameters** | **Name** | **Required** | **Type** | **Description** |
|-----------------------|----------|--------------|----------|-----------------|
|              | multiStepUpdate | True | Enum | OpsHub uses this flag to identify if all fields can be updated in single update entity call or multiple update entity calls are required. For example: If all the fields under fields can be updated in single API call in end system, then pass NO_SUB_STEP. But let’s say, if the end system has a separate API to transition entity from one state to another, then connector can pass STATIC_SUB_STEPS or DYNAMIC_SUB_STEPS depending on need. If ‘DYNAMIC_SUB_STEPS ‘ is being passed, then /entities/{entityTypeId}/sub-steps-for-update API is mandatory to implement<br><br>*NO_SUB_STEP: All the fields of an entity can be updated in single update entity API call.<br><br>*STATIC_SUB_STEPS: Step number of the field to be updated is predefined. So, every time when multiple fields are updated in single update, based on updateStepNumber of field, the order of field can be decided for the update.<br><br>*DYNAMIC_SUB_STEPS: The order in which the fields can be passed to the end system for the update is dynamically decided based on field value. E.g., if the entity is getting closed along with few other fields getting updated. In this case, other fields must be updated first and then entity status should be updated to closed. |
| **recovery** |          | True |      |      |
|                        | Type | True | Enum | Helps OpsHub determine if the given transaction has already taken place in failure and recovery scenarios<br><br>*HISTORY_BASED: (Preferred) Entity History – Get (/entities/{entityTypeId}/history) must be implemented, if this is passed. OpsHub will use the entity revision to identify if a given transaction was completed or not<br><br>*FIELD_BASED: Add a custom field of type text to end system (E.g., oh_last_update) to perform recovery. Ensure this field is passed under ‘fields’ of this API<br><br>*COMPARISON_BASED: This is a less reliable recovery mechanism as compared to HISTORY_BASED or FIELD_BASED. OpsHub compares last entity state saved in its database with current state in end system, to determine if last transaction was completed or not.<br>**Select this recovery mechanism if the pollerType for entity type is NON_TIME_BASED. |
|                        | fieldName | True, if recovery type=FIELD_BASED | String | In case of FIELD_BASED recovery, the field id of the custom field can be used by OpsHub for storing recovery flags. (E.g., oh_last_update). Note: This field should not be updated by other users in the end system. |
| **History**            |          | **False** |      | Pass this parameter, if the pollerType for entity type is ENTITY_WISE_HISTORY |
|                        | Type | True | Enum | How the end system returns entity history?<br>*FIELD_BASED: In a given revision, the old and new values are obtained only for those fields of an entity that were changed in a given transaction<br>*FULL_STATE_BASED: For a given revision, the end system returns the entity field state for all fields as of that revision |
|                        | revisionDateFormat | True | String | Date format for the field, which contains revision date time |
|                        | isRevisionIdNumeric | True | Boolean | When true, all the revision sorting will happen considering numeric value of revision id<br>When false, all the revision sorting will happen considering string value of revision id<br>Default will be false |
|                        | revisionUserDataType | True | Enum | Data type of the revision user.<br>*EMAIL_AS_USER: When the user’s email is provided in the revision user field<br>*USERNAME_AS_USER: When the username is provided in the revision user field |
|                        | separateHistoryApis | False | String | This is an optional input. Provide only if the end system has a separate history API for attachments, comments and/or links.<br>If separate history APIs is available for attachments, comments and/or links, provide the following as per API availability:<br>*ATTACHMENTS: When separate history API for attachments is available<br>*COMMENTS: When separate history API for comments is available<br>*LINKS: When separate history API for links is available |
|                        | sortableFields | False | Set<Enum> | Send set of fields for which end system supports sorting on history API. The fields can be sent in any order in the list. Connector should sort all the fields provided in the set. E.g.<br> If end system supports sorting on ENTITY_ID, CREATED_UPDATED_TIME and REVISION_ID<br> sortableFields = {CREATED_UPDATED_TIME, ENTITY_ID, REVISION_ID}<br><br> If end system supports sorting only on CREATED_UPDATED_TIME<br> sortableField={CREATED_UPDATED_TIME}<br>In case of history, CREATED_UPDATED_TIME is same as REVISION_DATE_TIME |
| **entityScope**        |          | False |      | If entity scope is decided based on only entity type and any additionalScopeField (like a project) is not required, this field can be set to null |
|                        | additionalScopeFieldName | True, if entityScope is passed. | Boolean | If entity scope is decided based on only entity type, this field can be set to null.<br>If entity scope is dependent on entity type as well as any other field of the entity (E.g., projectId, workspaceId or domainId), provide that field name of the entity.<br>Ensure that this field name matches one of the field names in “entityFieldNameInfo”. |
| **entityWebUrl**       |          | False |      | Pass this if you want the Remote Entity Link feature enabled for the connector. Otherwise, do not include entityWebURL in response |
|                        | baseUrl | True | String | String containing the base URL of the end system. E.g., if the actual URL format is "https://example.com/browse/{0}/{1}" then set baseUrl as "https://example.com/" and trailingTemplate as "browse/{0}/{1}".<br>This URL is used to form the Remote Link. If value for the field "Base URL for Remote Link" is not given in the system configuration form, the baseUrl will be used by default to form Remote Link. |
|                        | trailingTemplate | True | String | String template containing the trailing part of the URL format.<br>Provide all the dynamic parts in the URL as substitute numeric variables. e.g., {0}, {1} etc. If the projectId is 101 and entity is 10001. In this example, any entity in the system has base URL as https://example.com/ and trailingTemplate as browse/<projectId>/<entityId>.<br>So, the actual web URL will be "https://example.com/browse/101/10001". |
|                        | substitutes | True | List | Map containing all the substitute numeric parameters to the replacement field name of the entity.<br>E.g., {"0": "projectIdFieldName", "1": "entityIdFieldName"}<br><br>In the “trailingTemplate":<br><br>*The value of parameter {0} will be replaced with actual value coming in field project id for the entity.<br><br>*The value of parameter {1} will be replaced with actual value coming in entity id for the entity.<br><br>Ensure that this field name matches one of the field names in “fieldNameInfo”. |
| **isFieldIdConstantAcrossProjects** | | True | Boolean | Set to 'True' if the field id for the same field is same in different projects; else, set to 'False'.<br>E.g. If for a field with the display name 'Priority', field id in Project A is '100' and for Project B is '101', then send 'False'.<br>On the other hand, if the field id is the same (say 'priority' or '100') for all projects, then send 'True'.<br><br>If this is 'True', in FieldsMeta, we will use Field Id; otherwise, we will use Field Name. |
| **isInternalValueExistForLookupField** | | | Boolean | Set to 'True' if the lookup fields have different internal and display values<br>Set to 'False' if the lookup fields have only one value, the display value<br>
<br>Example 1:<br><br>**Priority** as lookup field: |
| **isUpdateAvailable** | False | Boolean | Set to 'True' if update is possible on the entity.<br>Set to 'False' if entity is create only. |
| **waitTimeInMillisIfApiResponseDelayed** | False | Number | In some systems, there is a delay in API returning updated data in response.<br><br>e.g., If an entity is updated,<br>* If within next second we try to fetch list of entities, the system might not return the last updated entity,<br>But if we get the list of updated entities after 2 seconds, the system will start returning the entities.<br>This delay might be due to indexing in the end system.<br><br>* Similarly, for history based systems, if we update an entity,<br>The last revision might not be available in the audit API within a second or two.<br>But if we query the revisions after 3 seconds, the system will start returning the revision.<br>This delay might be due to system inserting audit records separately than the actual entity update.<br><br>OIM handles this type of delays for update upto 2 seconds (2000 milli seconds).<br>If the end system has delay of upto 2 seconds, the value can be kept null.<br>If the end system has delay of more than 2 seconds, provide the maximum delay value in milli seconds in this field. |
| **searchEntityInfo** | True |  | All the metadata for querying end system to search entities. |
| sortableFields | False | Set<Enum> | Send set of fields for which end system supports sorting. For searchEntityInfo no need to pass REVISION_ID in sortableFields set.<br>**E.g.** If end system supports sorting on both ENTITY_ID and CREATED_UPDATED_TIME,<br>`sortableFields = {ENTITY_ID, CREATED_UPDATED_TIME}` |
| isGroupingSupported | True | Boolean | True (Preferred) if end system support order by for both created/updated time and entity id fields, otherwise false. If it is false, OpsHub will sort the results. |
| isSearchPossibleOnAnyField | True | Boolean | If criteria storage needs to be in the end system, then only set the field to true.<br><br>* The field selected for end system criteria should be queryable. if that's true, pass true here.<br>To get more details on end system criteria storage, refer [Criteria Configuration](../integrate/integration-configuration.md#criteria-configuration). |
| isCriteriaInSystemNativeFormat | True | Boolean | Send 'True' if configured criteria in OIM will be in the end system native query format.<br>If 'Yes', the criteria can be the exact query that the end system supports.<br>If 'No', the criteria should be OpsHub standard JSON format query. |
| dateTimeFormat | True | String | Date time format supported within the query.<br>**E.g.** `(where updatedDate > ‘2021-12-31 00:00:00’)`. Here, dateTimeFormat should be set as `yyyy-MM-dd HH:mm:ss`. |
| queryFieldNameInfo | False |  | Query field names should be provided for entity id, entity type id, project id, created date, updated date and created by field.<br>If the query field name for the above fields is the same as their field id given in 'fieldNameInfo', then set this field as 'Null'. Otherwise, provide the end system field names used for querying. If these field names are provided, they will be used to generate queries.<br><br>Here is a sample format of data to be passed under this parameter:<br><pre>"entityIdFieldName": "entity id field id",<br>"entityTypeIdFieldName": "entity type field id",<br>"projectIdFieldName": "project id’s field id",<br>"createdDateFieldName": "created date’s field id",<br>"updatedDateFieldName": "updated date’s field id",<br>"createdByFieldName":</pre> |
| batchSizeForInQuery | False | Integer | Number of entities end system supports in "IN" or "OR" query. Default will be 250.<br>**E.g.** for IN query: `entityId IN (1, 2, 3)`<br>**E.g.** for OR query: `(entityId = 1) OR (entityId = 2) OR (entityId = 3)` |




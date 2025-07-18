# Prerequisites

## User Privileges

* Create one administrator user of ServiceNow Quick Connect system (please refer to [Add User](#add-user) section for creating a new user), dedicated to OpsHub Integration Manager. User should not be used to do any operations from ServiceNow Quick Connect User-Interface.  
![Note](../assets/Note.jpg) In case your ServiceNow Quick Connect is configured with SSO, you will have to create a normal service user account in ServiceNow Quick Connect and use that user in integration.

* In case if administrator user is not available, dedicated user should have access to tables mentioned below. Please note that Read, Write, Delete, etc mentioned in brackets beside table names, are the access permissions required on respective table. Refer to [Add user access for table](#add-user-access-for-table) for providing required permissions to the user.
  * sys_attachment (Read, Write, Delete)
  * sys_audit (Read, Read.*)
  * sys_db_object (Read, Read.*)
  * sys_dictionary (Read, Read.*)
  * sys_choice (Read, Read.*)
  * ecc_queue (Write)
  * sys_attachment_doc (Read)
  * sys_user (Read)
  * sys_journal_field (Read,Write,Delete)
  * sys_glide_object (Read)
  * task (Read, Read.*)
  * User should have Read and Write access to all the entity table that needs to be synchronized. Eg., for incident to be synchronized, the user will need Read and Write access to the incident entity table.

![Note](../assets/Note.jpg) In above permissions, Read.* means there an ACL with * selected in columns with Read permission is required. Please refer to [Add user access for table](#add-user-access-for-table) for providing Read.* permission on a table.

* In case you want to use fields of type 'Reference' (e.g. Assignment group, Category, etc), some extra permissions need to be provided. Please refer to [Syncing reference fields](#syncing-fields) section for providing the required permissions.

* Please note, in addition to **Read.*** ACL on a table (wherever applicable in the above list); to get access to all the fields, you must ensure that each field of the table meets the following conditions:
  * Field should be marked 'Active' (Active column of the field should be set to 'True').
  * If read ACL is applied on the field, you will get access to the field only when you meet all the below-mentioned criteria associated with the ACL:
    * The condition associated with ACL must evaluate to 'true'.
    * The script associated with ACL must evaluate to 'true' or return an answer variable with the value of 'true'.
    * You must have one of the roles in the required roles list associated with ACL. If the list is empty, this condition evaluates to 'true'.

## Syncing Fields

* Reference fields are the fields that refer to some other ServiceNow Quick Connect entity, i.e., fields whose values are the records of some other entity. E.g., Assignment Group field in Incident entity refers to Group entity.
* To sync such reference fields, the integration user must have 'read' permission for the columns sys_id and name or number (whichever is available) of the table/entity that is being referred by the field. The **Allow access to this table via web services** check-box should be checked for allowing the access via REST API to the table being referred by the field.

![Note](../assets/Note.jpg) The user must not change the field types of out of the box system fields.

## Turning on Auditing (History) for a Table

ServiceNow Quick Connect tracks incident, change, and problem history in the sys_audit table. Enabling auditing tracks the creation and update of audited records. Audit must be enabled on the entity table (for example, not to its import set table but to the actual entity table like incident, problem, etc). To enable audit for a table, please refer to [Turn on auditing (history) for a table](#turn-on-auditing-history-for-a-table).

## Enable OpsHub Integration Manager for ServiceNow Quick Connect Instance

* OpsHub Integration Manager must be enabled for the ServiceNow Express instance. You can get this app from ServiceNow appStore: [https://store.servicenow.com/sn_appstore_store.do#!/store/application/8e6f0b610f8ce6001f6fc3ace1050ebb](https://store.servicenow.com/sn_appstore_store.do#!/store/application/8e6f0b610f8ce6001f6fc3ace1050ebb)

![Snow_Store](../assets/Snow_Store.PNG)

* On the OpsHub Integration Manager App page, click on **Get** and provide your ServiceNow Quick Connect HI Credentials.

* You will see OpsHub Integration Manager for ServiceNow Quick Connect in Downloads tab by navigating **System Applications -> Applications** in your ServiceNow Quick Connect instance [The example below shows OpsHub Integration Manager for ServiceNow Quick Connect Enterprise]. Click on Install for OpsHub Integration Manager for ServiceNow Quick Connect applications.

![Snow2](../assets/Snow2.png)

* On successful installation, OpsHub Integration Manager for ServiceNow Quick Connect application will be available.

## Configure Attachment or HTML//Rich type field

If attachments or HTML//Rich type supported fields are mapped, then keep the attachment filename's length to the maximum characters possible in ServiceNow Quick Connect. For configuring the attachment filename (maximum characters), refer to [How to change attachment table configuration](#how-to-change-attachment-table-configuration).

# System Configuration

Before you continue with the integration, you must first configure ServiceNow Quick Connect system. Click [System Configuration](../integrate/system-configuration.md) to learn the step-by-step process to configure a system. Refer to the screenshot given below:

![Snow_Quick_Connect_system_config](../assets/Snow_Quick_Connect_system_config.png)

ServiceNow Quick Connect system can be configured using either Basic or OAuth authentication.

| **Field Name** | **When field is visible on the System form** | **Description** |
|----------------|----------------------------------------------|------------------|
| **System Name** | Always | Provide system name. |
| **Version** | Always | Provide instance version. |
| **Instance URL** | Always | Provide the instance URL. - e.g. https://<instance-url>.service-now.com |
| **Authentication Mode** | Always | Two types of authentications are supported - 'Basic' or 'OAuth':<br>- For configuring a system using Basic Authentication, user needs to provide a username and password.<br>- For configuring a system using OAuth, user needs to provide username, password, client id and client secret. |
| **User Name** | For all authentication modes | Provide the username. |
| **User Password** | For all authentication modes | Provide the user password. |
| **Client ID** | Only when 'OAuth' authentication is selected | Provide the Client ID. |
| **Client Secret** | Only when 'OAuth' authentication is selected. | Provide the Client Secret. |
| **Base Entities** | Always | A ',' separated list of internal names of tables are expected in this field. All the tables extending the tables in this list will be available as entity types for synchronization. |
| **Overwrite API Endpoints** | Always | Default value is empty. Provide JSON to overwrite default API endpoints. Refer to [Overwrite API Endpoints using JSON](#overwrite-api-endpoints-using-json) section for more details. |

# Mapping Configuration

Map the fields between ServiceNow Quick Connect and the other system to be integrated to ensure that the data between both the systems synchronize correctly.  
Click [Mapping Configuration](../integrate/mapping-configuration.md) to learn the step-by-step process to configure mapping between the systems.

## Mapping Reference fields

* All the fields of type reference i.e. the fields that refer to some other ServiceNow Quick Connect entity will be treated as look-ups in OpsHub Integration Manager.
* For such reference fields, you can define value mapping using either name or number.
* A maximum of 1000 lookup values will be loaded for a reference field. If you are not able to find your value in the look-up values loaded, you can map values using advanced mapping.
* Look-up values will be loaded only if the entity being referred by a field has a name or number columns.
* If lookups cannot be loaded due to any reason, you can still do advanced mapping to map the fields. 
* If you want to do a direct mapping, i.e., if values in ServiceNow Quick Connect and other systems are same, then you need to use utility. Currently, OIMCoreUtility getEntityFieldValue is being used, which will give the display name corresponding to the internal id of the look-up value.

**Known limitation**:  
* Multi-select type of fields that do not have reference to any other type of field (e.g., string type multi-select field) are not supported as the target fields in mapping.

## Affected CIs Field Configuration for the Change Request Entity Type

* The Affected CIs field in ServiceNow is a virtual field used to read and associate Configuration Items (CIs) with Change Request (CR).

**Known Behavior**:  
* When ServiceNow is the source endpoint, any CI associated with a Change Request will be synchronized to the target system during the next update of that Change Request.  
  **Reason**: When user associate CI with the Change Request **last updated** time will not be modified, so user need to update system or custom field of Change Request to reflect the changes.

# Integration Configuration

In this step, set a time to synchronize data between ServiceNow Quick Connect and the other system to be integrated. Also, define parameters and conditions, if any, for integration.  
Click [Integration Configuration](../integrate/integration-configuration.md) to learn the step-by-step process to configure integration between two systems.

## Integration Recommendations & Assumptions

For Issue Relationship configuration for a given entity type (e.g. incident), only those entity types (e.g. problem) will be shown to which any reference type of field exists in the given type (e.g. incident).  

*For example*, if you are generating mapping for **Incident** entity type then **Problem** will be available under the section system entity types in Issue Relationship because in **Incident**, there is a field of reference type which refers to **Problem**. But if you are generating mapping for **Problem** then **Incident** won't be available under the section system entity types in Issue Relationship, because in **Problem**, there is no field of reference type that refers to 'Incident'.  
*From UI related incidents. list will be visible for a given **Problem**, but that's not considered as field.*

For ServiceNow as a source system, any event pertaining to attachment (add/delete), it is imperative to update at least one field for that particular entity for it to reflect in the sys_audit (history) table and to ascertain event change.

*To overcome manual overhead of updating entity to reflect attachment changes immediately then, it is require to configure following business rule which will generate an audit(s) on the particular field whenever attachment being added or deleted.*

- Navigate to **System Definition > Business Rules** and click on new to define the business rule for attachment.
- **For Add Attachment Business Rule** Create a Business Rule on the "sys_attachment" table. This will update the particular field (custom field in this sample) in the record upon the attachment add.
  - Name: "Insert Attachment - Update Record"
  - When: After
  - Insert: true
  - Advance: enable advance setting to define the script to update the particular field upon add operation. Refer following sample business rule script.
- **For Delete Attachment Business Rule** Create a Business Rule on the "sys_attachment" table. This will update the particular field (custom field in this sample) in the record upon the attachment delete.
  - Name: "Delete Attachment - Update Record"
  - When: After
  - Delete: true
  - Advance: enable advance setting to define the script to update the particular field upon add operation. Refer following sample business rule script.

**Sample Business Rule Script**  
![snow_rule_audit_attachment](../assets/snow_rule_audit_attachment.PNG)

![Note](../assets/Note.jpg) Refer to [ServiceNow Business Rules Docs](https://docs.servicenow.com/bundle/quebec-application-development/page/script/business-rules/concept/c_BusinessRules.html) for more information about the ServiceNow's business rule configuration.  
![Note](../assets/Note.jpg) Refer to [Community Blog](https://community.servicenow.com/community?id=community_blog&sys_id=ee6e22eddbd0dbc01dcaf3231f96196c) for more information about how to generate audit on field/notes upon attachment operation.

## Target LookUp Configuration

Provide query in 'Target Search Query' such that it is possible to search the entity in the ServiceNow Quick Connect as destination system. General query Syntax:  
`[Target_System_Field_Referance_Name] operators( =, !=, starts with, contains, etc...) @Source_System_Field_name@`.

**Sample queries:**

- Target lookup query based on Description field  
  `Description=@description@`

- Target lookup query based on State field  
  `State!=@status@`

- Target lookup query based on Number field  
  `Number=@RemoteID@`

## Criteria Configuration

**Query**

* **Criteria to get entities whose state is Open**  
  Example:  
  `state=1`  
  *How to get value 1 for the state Open?*

![Snow4](../assets/Snow4.png)

Right click on state field and click on **Show Choice** List.

![Snow5](../assets/Snow5.png)

Here, we can see the internal value `1` for `Open` state.

* **An example of criteria with one 'Lookup field'**  
  `state=1^priority=1`  
  `state=1^ORstate=2`

* **An example of criteria with one 'Lookup field and one Date field'**  
  `state=1^date_time>2018-01-31 08:00:00`

* **An example of criteria with 'contains on text field or created by (or some other user field) = sys_id of some user'**  
  `sync=true^ORassigned_to=2a6e8a480fcee600fd4ec3ace1050e20`

## Entity Level Advance Configuration

### Audit Filter Query

* The filter query helps to selectively process audits when fetching **update revisions** from ServiceNow.
* This query will be used to filter audits from the `sys_audit` table in ServiceNow.
  - To understand the syntax, refer to [Criteria Configuration](#criteria-configuration).
  - Example : Below is the query to filter out delete audits and audits made by John.

```
record_checkpoint!=-1^sys_created_by!=John
```

* Here make sure field names used in this query are of sys_audit table.
* This field only filters update revisions.

# Known Limitations

* Only comments and work_notes type comments are supported.
* Only name or number would be supported as display values for the look-up values of a reference field, i.e., if any field is marked for display in reference table then instead of that field either Name or Number will be shown. Look-up values will be loaded only if the response contains name or number.
* Look-up values will be loaded only when the integration user has the requisite 'read' permission on the required fields (sys_id, name and number) of the reference table.
* Field of type 'Duration' is not supported.
* Catalog variable is not supported.
* During write operation, if attachment/Inlinefile's name is greater than configured attachment filename's length in ServiceNow Quick Connect, it will result in processing failure or sync duplicate attachments.
* Synchronization of any entity type created under a private application scope is not supported.
* For history based synchronization, auto purging should be disabled for the sys_audit table.
* If the image is copied from an entity to another entity's field, there should not be more than one copied image in the field with the same name to sync such inline images.  
  ![Note](../assets/Note.jpg) If ServiceNow Quick Connect is one of the systems in bidirectional integration and the user has more than one copied image with the same name in the field, it will be synchronized to the target system correctly. However, if the target system's field gets updated, those changes will replace all the images with the first copied image in the ServiceNow Quick Connect.

# Appendix

## Add User

* Open ServiceNow Quick Connect.
* Filter **Users** and click on **Users**.
* Click **New**.

<center>![snow6](../assets/snow6.png)</center>

* Fill the details in the form and make sure that active checkbox is enabled.

<center>![snow7](../assets/snow7.png)</center>

* Open created user and click **Edit Roles**.

<center>![snow8](../assets/snow8.png)</center>

* Add **admin** privileges from Collection and click **Save**. In case you cannot provide admin privileges, please refer to [User Privileges](#user-privileges) section for providing required permissions to the user.

<center>![snow9](../assets/snow9.png)</center>

## Add User Access for Table

In ServiceNow Quick Connect, permissions are provided to a role which is assigned to user. Create a new role for your user. Refer to [Create Role](#create-role) for creating a new role and assigning it to your user.  
For reference, we are taking example of sys_audit table. Below steps are applicable for all the tables for which access needs to be provided to a user role.

### Provide 'read' access to a table

* Navigate to **System Definition > Tables** and open the definition for sys_audit table.

![Snow_access](../assets/Snow_access.PNG)

* Click on 'add' button in the **Access Controls** section.
* Select 'read' option in the **Operation** field.
* Under **Requires role** section, add the role for which read access needs to be provided.

![Snow_read](../assets/Snow_read.PNG)

* Click **Submit** and then click **Update** to update the table access controls.

### Provide 'write' access to a table

* Repeat steps as above, select 'write' in the Operation field.

![Snow_write](../assets/Snow_write.PNG)

### Provide 'delete' access to a table

* Repeat steps as above, select 'delete' in the Operation field.

![Snow_delete](../assets/Snow_delete.PNG)

### Provide 'read.*' access to a table

* Repeat steps as above, but in the 'name' field, select table name in first input box and '*' in second input box.

![Snow_read_star](../assets/Snow_read_star.PNG)

## Create Role

* Navigate to **User administration > Roles**.

![Snow_role](../assets/Snow_role.PNG)

* Click **New**.
* Fill the required details and click **Submit**.

![Snow_role_create](../assets/Snow_role_create.PNG)

* Assign this role to user via **User Administration > Users > Edit Roles**.

![Snow_user_role](../assets/Snow_user_role.PNG)  
![Snow_role_assign](../assets/Snow_role_assign.png)

## Turn on Auditing (History) for a Table

* Navigate to **System Definition > Dictionary**.
* Select the table to audit.
* Select the dictionary entry for the table. The table name always has an empty column name and **Type** `Collection`.

![Snow_audit](../assets/Snow_audit.PNG)

* Set the value for the **Audit** column to **true**.

## How to change attachment table configuration

1. Click **Tables** from **System Definition** on left side panel.  
   ![snow_systemdef_panel](../assets/snow_systemdef_panel.png)
2. Click **Attachment** table from the displayed list.  
   ![snow_attachment_tablelist](../assets/snow_attachment_tablelist.png)
3. Double click **Max Length** cell of the **File Name** column.  
   ![snow_attachment_table_columnlist](../assets/snow_attachment_table_columnlist.png)
4. Change value to maximum possible length and click the save icon.  
   ![snow_attachment_filename_length](../assets/snow_attachment_filename_length.png)

## Overwrite API Endpoints using JSON

* By default, APIs used for performing operations use the namespace `now`.
* If an instance uses a custom namespace or API endpoints, default configurations can be overwritten using **Overwrite API Endpoints** input in the system form.
* Standard table names will be appended after the provided API namespace URLs.
* Provide a JSON for the operations whose API endpoint needs to be overwritten. Entity wise or comment type wise endpoints can also be overwritten.

### Template JSON

```json
{
  "ENTITY_META": {
    "default": {
      "apiUrl": "<api_url_to_be_appended_to_the_base_instance_url>",
      "methodType": "GET"
    }
  },
  "FIELDS_META": {
    "default": {
      "apiUrl": "<api_url_to_be_appended_to_the_base_instance_url>",
      "methodType": "GET"
    }
  },
  "USER_META": {
    "default": {
      "apiUrl": "<api_url_to_be_appended_to_the_base_instance_url>",
      "methodType": "GET"
    }
  },
  "READ_ENTITY_DETAILS": {
    "default": {
      "apiUrl": "<api_url_to_be_appended_to_the_base_instance_url>",
      "methodType": "GET"
    }
  },
  "READ_ENTITY_AUDITS": {
    "default": {
      "apiUrl": "<api_url_to_be_appended_to_the_base_instance_url>",
      "methodType": "GET"
    }
  },
  "CREATE_ENTITY": {
    "default": {
      "apiUrl": "<api_url_to_be_appended_to_the_base_instance_url>",
      "methodType": "POST"
    },
    "entityWise": [
      {
        "entityType": "<entityInternalName>",
        "apiCalls": [
          {
            "apiUrl": "<api_url_to_be_appended_to_the_base_instance_url>",
            "methodType": "POST",
            "executionOrder": 1,
            "queryParams": {}
          }
        ]
      }
    ]
  },
  "UPDATE_ENTITY": {
    "default": {
      "apiUrl": "<api_url_to_be_appended_to_the_base_instance_url>",
      "methodType": "PUT"
    }
  },
  "DELETE_ENTITY": {
    "default": {
      "apiUrl": "<api_url_to_be_appended_to_the_base_instance_url>",
      "methodType": "DELETE"
    }
  },
  "READ_ATTACHMENTS": {
    "default": {
      "apiUrl": "<api_url_to_be_appended_to_the_base_instance_url>",
      "methodType": "GET"
    }
  },
  "ADD_ATTACHMENTS": {
    "default": {
      "apiUrl": "<api_url_to_be_appended_to_the_base_instance_url>",
      "methodType": "POST"
    }
  },
  "DELETE_ATTACHMENT": {
    "default": {
      "apiUrl": "<api_url_to_be_appended_to_the_base_instance_url>",
      "methodType": "DELETE"
    }
  },
  "READ_COMMENTS": {
    "default": {
      "apiUrl": "<api_url_to_be_appended_to_the_base_instance_url>",
      "methodType": "GET"
    }
  },
  "ADD_COMMENT": {
    "default": {
      "apiUrl": "<api_url_to_be_appended_to_the_base_instance_url>",
      "methodType": "PUT"
    }
  }
}
```

### Sample JSON with default values

```json
{
  "ENTITY_META": {
    "default": {
      "apiUrl": "/api/now/v1/table",
      "methodType": "GET"
    }
  },
  "FIELDS_META": {
    "default": {
      "apiUrl": "/api/now/v1/table",
      "methodType": "GET"
    }
  },
  "USER_META": {
    "default": {
      "apiUrl": "/api/now/v1/table",
      "methodType": "GET"
    }
  },
  "READ_ENTITY_DETAILS": {
    "default": {
      "apiUrl": "/api/now/v1/table",
      "methodType": "GET"
    }
  },
  "READ_ENTITY_AUDITS": {
    "default": {
      "apiUrl": "/api/now/v1/table",
      "methodType": "GET"
    }
  },
  "READ_COMMENTS": {
    "default": {
      "apiUrl": "/api/now/v1/table",
      "methodType": "GET"
    }
  },
  "READ_ATTACHMENTS": {
    "default": {
      "apiUrl": "/api/now/attachment",
      "methodType": "GET"
    }
  },
  "CREATE_ENTITY": {
    "default": {
      "apiUrl": "/api/now/v1/table",
      "methodType": "POST"
    },
    "entityWise": []
  },
  "UPDATE_ENTITY": {
    "default": {
      "apiUrl": "/api/now/v1/table",
      "methodType": "PUT"
    }
  },
  "ADD_COMMENT": {
    "default": {
      "apiUrl": "/api/now/v1/table",
      "methodType": "PUT"
    }
  }
}
```

![Note](../assets/Note.jpg) If details for an operation are not provided in the JSON, then default API endpoints with namespace `now` are used.


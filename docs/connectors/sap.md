# Prerequisites

## Pre-loaded Dependency

* SAP connector depends on 'sapjco3.dll' (for Windows) and 'libsapjco.so' (for Linux).
* These files can be downloaded from [SAP Connector](https://support.sap.com/en/product/connectors/jco.html) by the user with a valid SAP license/subscription.
* Place the dependency in a path available in the machine's environment variables. Restart the OpsHub Integration Manager service after placing the dependency.
* The following table shows one of the paths available in the environment variables:

| OS Type | Dependency   | Path                   |
|---------|--------------|------------------------|
| Windows | sapjco3.dll  | C:\Windows\System32     |
| Linux   | libsapjco.so | \usr\lib               |

## User Privileges

* Create a technical ABAP user in the SAP ECC or SAP S/4HANA technical instance dedicated to OpsHub Integration Manager. This user shouldn't perform any other action from SAP GUI. This user is referred to as the 'Integration User' in this document.
* A SAP user can only be created by the SAP BASIS administrator.
* To integrate SAP entities using OpsHub Integration Manager, the user must be a technical ABAP user with:
  * RFC read and execute permissions.
  * SE80 read, write, and execute permissions.

## Enable API for 'Linkages'

* OpsHub Integration Manager uses the RFC 'CRMOST_WHERE_USED_LIST' to fetch the linkages for each entity type except the 'Transport Request' entity.
* After SAP ECC 6.0 and in SAP S/4HANA, this API is set to **normal-enabled** in the SAP end system.
* To sync any entity type other than 'Transport Request', it is mandatory to:
  * Ask the SAP BASIS administrator to make the API **RFC-enabled** in the end system.
  * Or plug in the custom API 'ZCRMOST_WHERE_USED_OPSHUB' in the end system. Refer to [Configure Custom Linkage API](#configure_custom_linkage_api) for details.

## Enable API for 'Usage Details'

* Due to the lack of available API in SAP, the user must configure the custom API in SAP end system to fetch the Usage Details entity for synchronization.
* Refer to [Configure Custom Linkage API](#configure_custom_linkage_api) for details.

# System Configuration

* To start the integration, configure the SAP system in OpsHub Integration Manager.
* Refer to [System Configuration](../integrate/system-configuration.md) page to learn the stepwise process. Refer to the following screenshot:

<p align="center">
  <img src="../assets/sap_system_form.png" />
</p>

**SAP System form details**

| Field Name                | Description                                                                                         |
|---------------------------|-----------------------------------------------------------------------------------------------------|
| **System Name**            | Provide the system's name.                                                                          |
| **Version**                | Provide the version of the SAP instance: ECC or HANA.                                              |
| **Host**                   | Specify the host where the SAP system is deployed. For example: 49.50.51.52                        |
| **Port**                   | Specify the port where the SAP system is deployed. Usually, it is 80XX, where XX is the instance number.|
| **Instance Number**        | Specify the instance number of the SAP system. It is a two-digit number indicating the Id of the SAP instance.|
| **Group**                  | Provide the Group IP for the SAP system. If there is no group, enter the same value as Host.         |
| **Client Id**              | Specify the SAP Client Id. It is a three-digit number to identify the SAP Client.                  |
| **User Id**                | Provide the user id of a dedicated user for communicating with the system API. This user should have the required privileges as mentioned in [User Privileges](#user-privileges) |
| **Password**               | Provide the password for the user.                                                                  |
| **Language Code**          | Specify the language code of the SAP system. For example: EN (for English). The language code must be only two characters. The default language code is EN. |
| **Additional Entity Type** | This is an optional field to specify the list of entity type(s), other than the supported ones for integration. Each additional entity type must be a valid Object Type of the TADIR table in SAP. Refer to [Additional Entity Type JSON](#additional-entity-type-json) to understand the input template. |

**Additional Entity Type JSON**

> **Note** :For the additional entity types, certain advanced features may not operate as intended. The purpose of this field is to offer users the flexibility to sync entity types beyond the default options.
* In SAP, all the objects' entries are available in the TADIR table, along with their Object Type. This document will use the word 'Entity Type' for Object Types in SAP. Out of the available entity types in TADIR, OpsHub Integration Manager supports limited entity types by default.
* If there are entity types present in the TADIR table but not included in the supported list of OpsHub Integration Manager, the user can integrate them by registering their details in the Additional Entity Type field in the SAP system form. This can be done using the following JSON template:

```json
[
    {
      "displayName": "Mention the display name of the entity type.",
      "objectTypeInTADIR":"Mention the entity type from 'OBJECT' column of the TADIR table in the SAP instance.",
      "relatedSapTables": [
        {
            "sapTableName":"Mention additional SAP table name (if any), having more details about the entity type.",
            "joinColumnName": "Mention the column name of the above table, having the identifier value same as 'OBJ_NAME' column of TADIR table."
        },
        ...
      ]
    },
    ...
]
```

Multiple additional entity types can be added in the same field. Refer to the below example:
```json
[
    {
      "displayName": "View Cluster",
      "objectTypeInTADIR":"VCLS",
      "relatedSapTables": [
        {
            "sapTableName":"VCLSTRUCT",
            "joinColumnName": "VCLNAME"
        }
      ]
    },
    {
      "displayName": "View Maintenance",
      "objectTypeInTADIR":"VDAT",
      "relatedSapTables": [
        {
            "sapTableName":"",
            "joinColumnName":""
        }
      ]
    }
]
```

# Mapping Configuration

> **Note** :In OpsHub Integration Manager, the SAP system supports only read-only functionality.

- Map the fields between SAP and the other system to be integrated to ensure data synchronization between both systems.
- Here is an example of SAP's Enhancement and Azure DevOps' User Story integration:

<p align="center">
  <img src="assets/sap_mapping_preview.png" />
</p>

Refer to the [Mapping Configuration](../integrate/mapping-configuration.md) page to learn the steps to configure mapping between the systems.

In SAP, there can be only one project representing the object repository of the instance.

# Integration Configuration

Set a time to synchronize data between SAP and the other system to be integrated. Also, define parameters and conditions (if any) for integration. Refer to the [Integration Configuration](../integrate/integration-configuration.md) page to learn the steps to configure the integration between two systems. Refer to the screenshot below:

<p align="center">
  <img src="assets/sap_integration.png"  />
</p>

## Criteria Configuration

If the user wants to specify conditions for synchronizing an entity from SAP as the source system to the other system (target system), criteria must be configured. Navigate to the [Criteria Configuration](../integrate/integration-configuration.md#criteria-configuration.md) section on the [Integration Configuration](../integrate/integration-configuration.md) page for more details.

- Set the **Query** as per the SAP native query format.
- Criteria configuration is not supported by the 'Usage Details' entity type.
- However, criteria can be applied to the below fields for the 'Transport Request' entity type:

<span style="color:blue"> **Criteria samples for 'Transport Request' entity:** </span>

{| class="wikitable" align="center"
|| **Field Internal Name** || **Field Display Name** || **Criteria snippet** || **Description**
|-
|| **TRKORR** || Request/Task || TRKORR LIKE 'EH%' || Query to get the results only for TRs starting with 'EH'.
|-
|| **TRFUNCTION** || Type of request/task || TRFUNCTION NE 'D' || Query to get the results only for TRs with function type D.
|-
|| **TRSTATUS** || Status of request/task || TRSTATUS EQ 'R' || Query to poll only released TRs.
|-
|| **TARSYSTEM** || Transport Target of Request || TARSYSTEM LIKE 'AB%' || Query to poll TRs meant for target system starting with 'AB'.
|-
|| **KORRDEV** || Request or task category || KORRDEV EQ 'ZTES' || Query to poll TRs of the 'ZTES' category.
|-
|| **AS4USER** || Owner of a Request or Task || AS4USER EQ 'USER1' || Query to poll TRs whose owner is 'USER1'.
|-
|| **AS4DATE** || Date of Last Change || AS4DATE GE '20240809' AND AS4DATE LE '20240909' || Query to poll TRs between given the time interval. Time is given in the 'yyyyMMdd' format.
|-
|| **STRKORR** || Higher-Level Request || STRKORR LIKE 'Z%' || Query to poll TRs with higher-level request names starting with Z.
|-
|}

- For all other entity types (including additional types), criteria can be applied to any of the fields corresponding to the columns in the TADIR table in SAP. Refer to the [TADIR Columns](#tadir-columns) section for more details.

# Known Behaviour

## Dynamically changing poller type of an entity

In SAP environments running versions below ECC 6.0 with NetWeaver 7.5, certain SAP tables used for polling do not contain date columns for entity creation. This limitation affects the ability of the poller to function based on timestamps.

### Behavior and Impact

- If the expected time field is unavailable in the SAP end system, the poller switches to a non-timestamp-based mode.
- In non-timestamp-based polling, the poller retrieves all entities, regardless of their creation time.
- Due to this, it is recommended to increase the 'Associate Schedule' available in 'Global level advance configurations' while configuring integration to optimize the performance and reduce unnecessary processing.
- By default, the poller operates as a current-state poller.

### API rate-limit in SAP

- The SAP system uses `sapjco3.dll` to communicate with the end system. Hence, there is no specific limitation in terms of calling APIs.
- However, if there is an idle wait time-out configured in the SAP GUI, the same is applicable for the system in OpsHub Integration Manager.
- The wait time-out can be changed/disabled only by the SAP BASIS administrator.

## Limitations

- Entities will be synced without history.
- Comments and Attachments are not supported for any entity type of SAP.

## Limitations specific to Usage Details entity

- Metadata of the system fields is not available for the 'Usage Details' entity type. However, static metadata is provided for the same.
- Recovery cannot be performed for the 'Usage Details' entity type, as the data for this entity expires every 48 hours in the end system. This expiration time is configurable in the end system and can only be done by the SAP BASIS administrator.
- Integration for syncing the 'Usage Details' entity type does not work in parallel with other entity types' integrations using the same SAP system. However, the use case can be achieved by configuring two separate systems for Usage Details and any other entity types. This behavior is because of the difference in time formats for the 'Usage Details' entity and other supported entity types.

# Appendix

## TADIR Columns

- TADIR is a master table in SAP storing the system and custom object types of the given SAP instance.
- Refer to the following list of the column names corresponding to the fields of entity types other than 'Transport Request' for SAP ECC:

<p align="center">
  <img src="assets/sap_tadir.png" />
</p>

> **Note** :Display names of the fields might vary in different versions of SAP. The above table is for reference only.

## Configure Custom Linkage API

1. Open 'Object Navigator' using SE80 TCode in SAP GUI.

<p align="center">
  <img src="assets/sap_link_step_1.png" />
</p>

2. Select 'Function Group' from the object drop-down.

<p align="center">
  <img src="assets/sap_link_step_2.png"  />
</p>

3. Type 'ZMYOPSHUB' and press Enter. If the Function Group exists, skip this step. Click 'Yes'.

<p align="center">
  <img src="assets/sap_link_step_4.png" />
</p>

4. Add a description and click 'Save'. Click 'Local Object' in the pop-up window.

<p align="center">
  <img src="assets/sap_link_step_3.png"  />
</p>

<p align="center">
  <img src="assets/sap_link_step_5.png"  />
</p>

5. Right-click 'ZMYOPSHUB' and select 'Function Module'.

<p align="center">
  <img src="assets/sap_link_step_6.png"  />
</p>

6. Enter the name as 'ZCRMOST_WHERE_USED_OPSHUB', add a short description and click 'Save'.

<p align="center">
  <img src="assets/sap_link_step_7.png"  />
</p>

7. Double-click the function module and go to Utilities->More Utilities->Upload/Download->Upload. Browse the API file and upload.

<p align="center">
  <img src="assets/sap_link_step_9.png"  />
</p>

8. If the upload option is not working, copy-paste the code in the IDE and add the following import and export variables.

<p align="center">
  <img src="assets/sap_link_step_10.png"  />
</p>

<p align="center">
  <img src="assets/sap_link_step_11.png" />
</p>

9. Go to 'Attributes' and select the Remote-Enabled Module radio button.

<p align="center">
  <img src="assets/sap_link_step_12.png"  />
</p>

10. Save and activate the Function Module. Click the green tick mark in the pop-up window.

<p align="center">
  <img src="assets/sap_link_step_13.png" />
</p>

## Configure Usage Details API

- Follow steps 1 to 7 from [Configure Custom Linkage API](#configure-custom-linkage-api) by replacing the name of the API with 'Z_MY_RSSTAT27_LATEST'.
- After step 7:
  - If the upload option is not working, copy-paste the code in the IDE and add the following import and export variables.

<p align="center">
  <img src="assets/sap_usage_step_1.png" />
</p>

<p align="center">
  <img src="assets/sap_usage_step_2.png" />
</p>

- Go to 'Attributes' and select the Remote-Enabled Module radio button.
- Save and activate the Function Module. Click the green tick mark in the pop-up window.

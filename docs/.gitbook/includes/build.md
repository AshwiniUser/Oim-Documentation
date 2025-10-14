# Build Entity

* Build data is supported for all cloud deployment (AzureDevOps) and version 2019 onwards for on-premise deployment(i.e. Team Foundation Server).
* Build entity does not have Attachments, Comments, and Inline images, hence these details are not supported.
* Build entity is only synchronized for finished, not started and in-progress states.
* Build entity does not have historical data, hence historical data are not supported.
* Stage update will be synchronized to target system.
*  If user wants to sync the Build only after particular stage of the pipeline, it can be achieved via the OpsHub Workflow changes and utility functions defined into com.opshub.eai.tfs.buildentity.TFSBuildUtility class \[for example getMatchedNodes function from the TFSBuildUtility can be called from the advanced integration workflow to get the builds that matches with particular stage mentioned into argument].
  > **Note** For Workflow changes and utility function, contact the OpsHub Sales team.
* Criteria configuration with Select criteria storage type as In End System not supported due to build entity does not have custom fields.
* **Shelveset name** and **drop location root** field details will not be available for synchronization.
  * Reason: ADO/TFS API Limitation.
* To sync the stages' approvals, the following points must be considered:
  * Three text types of the fields need to be created for stage identifier(in YML file of pipeline for particular stage), approval status, approval comments in source system, from which the data will be synced to Build entity.
  * To approve the build stage, user needs to give the above three values in the above fields.
  * Map the 'None' field of the source system to the OH_StageApproval field of build entity in <code class="expression">space.vars.SITENAME</code>. The following advance mapping should be utilized for mapping the 'None' field to OH_StageApproval:
    
```xml
<oh_stageApproval xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
  <xsl:variable name="sap" select="'SEPARATOR'"/>
  <xsl:variable name="stages" select="tokenize(normalize-space(SourceXML/updatedFields/Property/FIELD_INTERNAL_NAME_OF_STAGE_IDENTIFIER), $sap)"/>
  <xsl:variable name="status" select="tokenize(normalize-space(SourceXML/updatedFields/Property/FIELD_INTERNAL_NAME_OF_STATUS), $sap)"/>
  <xsl:variable name="comments" select="tokenize(normalize-space(SourceXML/updatedFields/Property/FIELD_INTERNAL_NAME_OF_COMMENTS), $sap)"/>
  <xsl:for-each select="$stages">
    <op_list>
      <xsl:variable name="vPosition" select="position()" />
      <stage><xsl:value-of select="$stages[$vPosition]"/></stage>
      <status><xsl:value-of select="$status[$vPosition]"/></status>
      <comment><xsl:value-of select="$comments[$vPosition]"/></comment>
    </op_list>
  </xsl:for-each>
</oh_stageApproval>
```

* Put the field's internal name of stage identifier, approval status, approval comments in the advanced mapping in place of FIELD_INTERNAL_NAME_OF_STAGE_IDENTIFIER, FIELD_INTERNAL_NAME_OF_STATUS, FIELD_INTERNAL_NAME_OF_COMMENTS respectively.
* Put any separator in place of SEPARATOR. In multiple stage approvals, user needs to give three fields' data with SEPARATOR separated value in the opposite entity.
* The approval sync requires the status and stage identifier to approve the stage. For example, if there is ',' as SEPARATOR in advanced mapping, to approve stage 1 and stage 2 at a time, the following values must be inserted:
* Put **stage1Identifier,stage2Identifier** value in FIELD_INTERNAL_NAME_OF_STAGE_IDENTIFIER
* Put **comment1,comment2** value in FIELD_INTERNAL_NAME_OF_COMMENTS (here comment1 is for stage 1 and comment2 is for stage 2 approval)
* Put **approved,rejected** value in FIELD_INTERNAL_NAME_OF_STATUS (here stage 1 will be approved and stage 2 will be rejected)
* The user needs to insert these three values at the time of stages' approval for the build.

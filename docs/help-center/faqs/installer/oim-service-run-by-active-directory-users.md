## Description

{% if "OpsHub Migrator for Microsoft Azure DevOps" === space.vars.SITENAME %}
Can the <code class="expression">space.vars.SITENAME</code> Service be run by Active Directory users? If yes, what are the permissions required to run it?
{% endif %}
{% if "OpsHub Integration Manager" === space.vars.SITENAME %}
Can the OpsHub Server Service be run by Active Directory users? If yes, what are the permissions required to run it?
{% endif %}

## Solution

{% if "OpsHub Migrator for Microsoft Azure DevOps" === space.vars.SITENAME %} OpsHub Migrator for Microsoft Azure DevOps {% endif %} {% if "OpsHub Integration Manager" === space.vars.SITENAME %} OpsHub Server {% endif %} Service can be run by a standard Windows login user as well as an Active Directory user with admin privileges.

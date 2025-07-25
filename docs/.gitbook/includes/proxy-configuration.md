{{#ifeq: {{SITENAME}} | OpsHub Migrator for Microsoft Azure DevOps |To start the {{SITENAME}} installer on a machine that is behind a proxy, please perform the following steps:<br>|}}

{{#ifeq: {{SITENAME}} |  OpsHub Migrator for Microsoft Azure DevOps |1. | 6.}} Open environment configuration from My Computer -> Properties -> Advanced System Settings -> Environment Variables 

<p align="center"><img src="../assets/Proxy 1.png" width="600"/></p>

<p align="center"><img src="../assets/Proxy2.png" width="600"/></p>

<p align="center"><img src="../assets/Proxy3.png" width="600"/></p>

{{#ifeq: {{SITENAME}} | OpsHub Migrator for Microsoft Azure DevOps |2. | 7. }} Create a new environment variable with the name **"_JAVA_OPTIONS"**.

<p align="center"><img src="../assets/Proxy4.png" width="600"/></p>

{{#ifeq: {{SITENAME}} | OpsHub Migrator for Microsoft Azure DevOps |3. | 8. }} Set the variable's value as per the format ->  
`-Dhttp.proxyHost= -Dhttp.proxyPort= -Dhttp.nonProxyHosts="localhost|127.0.0.1" -Dhttp.proxyUser= -Dhttp.proxyPassword= -Dhttps=`

| **Attribute**           | **Description**                                                                                                                                       |
|-------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| `-Dhttp.proxyHost`      | Proxy server host address                                                                                                                            |
| `-Dhttp.proxyPort`      | Proxy server host port number                                                                                                                        |
| `-Dhttp.nonProxyHosts`  | Hosts accessible without proxy server                                                                                                                |
| `-Dhttp.proxyUser`      | User name to access proxy server                                                                                                                     |
| `-Dhttp.proxyPassword`  | Password for the provided username to access proxy server                                                                                            |
| `-Dhttps`               | If proxy server is hosted over HTTPS, then set this parameter as `"true"` else `"false"`.<br>This attribute is not mandatory. Default is `"false"`  |

**For example:**  
`-Dhttp.proxyHost='00.00.00.00' -Dhttp.proxyPort='8080' -Dhttp.nonProxyHosts="localhost|127.0.0.1" -Dhttp.proxyUser='username' -Dhttp.proxyPassword='password' -Dhttps=false`

In the above example:  
ProxyIP → `00.00.00.00`, Proxy Port → `8080`, Proxy User Name → `username`, Proxy Password → `password`

<p align="center"><img src="../assets/Proxy5.png" width="600"/></p>

{{#ifeq: {{SITENAME}} | OpsHub Migrator for Microsoft Azure DevOps |4. Save all the changes. | 9. Save all the changes and restart the {{SITENAME}} Service. }} 

{{#ifeq: {{SITENAME}} | OpsHub Migrator for Microsoft Azure DevOps | | 10. Test the proxy by opening service URL **http://<service host>:<port>/TFSService** in browser. Now check the connection by trying to create mapping.}}

> **Note**:
> Even after performing all these steps, if you are still unable to connect, then please check the proxy credentials given in  
> {{#ifeq: {{SITENAME}} | OpsHub Migrator for Microsoft Azure DevOps | Step 3 | Step 8 }} and  
> {{#ifeq: {{SITENAME}} | OpsHub Migrator for Microsoft Azure DevOps | restart your installer. | restart the {{SITENAME}} Service.}}

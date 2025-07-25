# Launching Installer

The first screen when you launch the application will be this:

<p align="center">
  <img src="../assets/Launching_Installer_Image_1bbn.png" alt="Launching Installer Image 1bbn" />
</p>

## Launch the installer in different Operating Systems

- Unzip the OIM installer folder to find the executable(.exe) file.
- The steps to launch the installer in different Operating Systems (OS) are given below. Follow the steps given for the OS that you are using.

| Windows | Linux |
| --- | --- |
| Windows | Linux |
| - Double click the executable .exe file given in the application folder (It is advisable to run .exe file by right-clicking Run as administrator where * is replaced with the application version).<br> - If one instance of this release is already installed, then the user will be notified.<br> - Click yes to continue with the installation. It will then display the uninstallation key for the current installation. | Before Installation <br> - Extract the zip file. Make sure user who will run installer owns the files and has full access to extracted files.<br> - Create empty directory with full access (it should not be inside installation directory) and export its path to OPSHUB_TEMP_DATA variable as shown below: <br>     export OPSHUB_TEMP_DATA=/home/setup/temp <br> - If you are doing a silent installation, make sure you have provided the same path for OPSHUB_TEMP_DATA as provided during silent registration.<br> - If Linux has NFS (Network File System) based file system, add the following line in OIM user's .bashrc file:<br>     In /home/{OIM user}/.bashrc, add the line:<br>     export JAVA_OPTS="$JAVA_OPTS -XX:+StartAttachListener"<br> - Without the Java option, the server startup will fail. Error details are available here.<br> - See minimal access required to install {{SITENAME}} here if you do not have root access.<br><br> To Run sh File<br> - Open terminal and go to the folder containing the install.sh file.<br> - Run: sudo -E sh install.sh<br> - Linux UI access is required as installation needs user input via UI. Installation won't complete via remote terminal (e.g. PuTTY).<br><br> To Run sh File from External File (Silent Installation)<br> To install {{SITENAME}} through terminal (e.g. PuTTY):<br> - Complete user registration as described here.<br> - Download and modify OpsHubAutoInstall.xml as needed by clicking Here.<br> - Transfer modified file to the target instance.<br> - Set environment variable OPSHUB_AUTO_INSTALL pointing to the XML file:<br>     Example: export OPSHUB_AUTO_INSTALL=/home/Downloads/OpsHubAutoInstall.xml<br> - Run the installer: sudo -E sh install.sh<br> - See Possible Error section for troubleshooting.


### Recommended Installation Path for OpsHub Integration Manager Installer for Linux

- It is recommended to install or perform migration of the OpsHub Integration Manager in the /opt folder or /user/local folder.  
  - For OpsHub Integration Manager migration, if the OpsHub Integration Manager is not installed at the above places, then follow the steps mentioned [here](../faqs/general/how-to-move-application-server-from-one-machine-to-other.md).
  - Reason: SELinux prevents Linux users from running a OpsHub Integration Manager service in the user's home directory. Hence, the user needs to avoid installing OpsHub Integration Manager in the home directory.


### Minimal access required to run linux installer using external file

- OpsHub Integration Manager Installation Directory should be owned by user who run installer/migrator and has following permissions.

Here are the required permissions:

| **Permission** | **Directory** |
|----------------|---------------|
| --x            | /usr          |
| --x            | /proc         |
| r-x            | /usr/bin      |
| r-x            | /usr/bin/*    |
| --x            | /usr/lib64    |
| r-x            | /usr/lib64/*  |
| --x            | /usr/share (if user edits file using nano) |
| r-x            | /usr/share/*  |
| rw-            | /etc/systemd/system (if user needs OpsHub Integration Manager as a service for Ubuntu) |



- Note: For HSQLDB, root access is required when user needs to install/migrate OpsHub Integration Manager.

### Possible error during Silent Installation/Upgradation

\[ Starting automated installation \]

\[Timestamp\] java.util.prefs.FileSystemPreferences\$2 run

INFO: Created system preferences directory in java.home.

com.izforge.izpack.installer.InstallerException: Validating data for
panel UserInputPanel.EmailIdVerificationForExistingCode was not
successfull

com.izforge.izpack.installer.InstallerException: Validating data for
panel UserInputPanel.EmailIdVerificationForExistingCode was not
successfull

at com.izforge.izpack.installer.AutomatedInstaller.validatePanel(Unknown
Source)

at com.izforge.izpack.installer.AutomatedInstaller.installPanel(Unknown
Source)

at com.izforge.izpack.installer.AutomatedInstaller.doInstall(Unknown
Source)

at com.izforge.izpack.installer.Installer.main(Unknown Source)

\[ Automated installation FAILED! \]

**Solution**

Make sure you have performed the following steps correctly:

- You have registered as described [Registration – Silent Registration for Linux](registration.md#silent-registration-for-linux) before Installation/Upgradation.
- You have registered using the same path for which you install/upgrade OpsHub Integration Manager.
- You have used the correct verification code.
  - Verification Code is unique for each machine and installation path. The code generated on a different machine and for different path won't work.
- You have export same value for OPSHUB_TEMP_DATA during Registration and Installation/Upgradation.

## License Information

On launching the installer, you will see the license agreement window that contains all license-related terms and conditions.

If you agree with the license details, then only you can move to the next step i.e. Installation.  
  
<p align="center">
  <img src="../assets/Default_Installation_Image_1La.png" alt="Default Installation Image 1La" />
</p>

License Information window has the details of the trial license and the contact information to purchase the license.  
<p align="center">
  <img src="../assets/Default_Installation_Image_2LH.png" alt="Default Installation Image 2LH" />
</p>

### Possible exceptions

While uploading the license from license management tab, OpsHub Integration Manager throws exceptions as below:

- **Unable to install license**
`com.opshub.license.exception.LicenseException`: Failed to get license content because of If you are accessing OpsHub from different machine then change localhost to ip address of the machine where OpsHub installed.

- **The filename, directory name, or volume label syntax is incorrect**

com.opshub.license.install.OpsHubLicenseManager.getLicenseContent(OpsHubLicenseManager.java:60)
at
com.opshub.license.install.OpsHubLicenseOperationManager.getLicenseContent(OpsHubLicenseOperationManager.java:34)
at
com.opshub.license.install.LicenseInstaller.getOHLicenseContent(LicenseInstaller.java:128)
at
com.opshub.license.install.LicenseInstaller.installLicense(LicenseInstaller.java:57)
at
com.opshub.license.install.LicenseInstaller.installLicense(LicenseInstaller.java:51)
at
com.opshub.license.server.LicenseBO.validateAndInstallLicense(LicenseBO.java:329)
at
com.opshub.license.server.LicenseServer.validateAndInstallLicense(LicenseServer.java:96)
at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method) at
sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
at
sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
at java.lang.reflect.Method.invoke(Method.java:483) at
com.metaparadigm.jsonrpc.JSONRPCBridge.call(JSONRPCBridge.java:1122) at
com.opshub.JSON.JSONRPCServlet.service(JSONRPCServlet.java:349) at
javax.servlet.http.HttpServlet.service(HttpServlet.java:729) at
org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:230)
at
org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:165)
at
org.apache.tomcat.websocket.server.WsFilter.doFilter(WsFilter.java:53)
at
org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:192)
at
org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:165)
at
org.apache.catalina.filters.HttpHeaderSecurityFilter.doFilter(HttpHeaderSecurityFilter.java:120)
at
org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:192)
at
org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:165)
at
com.opshub.JSON.CacheControlFilter.doFilter(CacheControlFilter.java:27)
at
org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:192)
at
org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:165)
at
org.apache.catalina.core.StandardWrapperValve.invoke(StandardWrapperValve.java:199)
at
org.apache.catalina.core.StandardContextValve.invoke(StandardContextValve.java:96)
at
org.apache.catalina.authenticator.AuthenticatorBase.invoke(AuthenticatorBase.java:474)
at
org.apache.catalina.core.StandardHostValve.invoke(StandardHostValve.java:140)
at
org.apache.catalina.valves.ErrorReportValve.invoke(ErrorReportValve.java:79)
at
org.apache.catalina.valves.AbstractAccessLogValve.invoke(AbstractAccessLogValve.java:624)
at
org.apache.catalina.core.StandardEngineValve.invoke(StandardEngineValve.java:87)
at
org.apache.catalina.connector.CoyoteAdapter.service(CoyoteAdapter.java:349)
at
org.apache.coyote.http11.Http11Processor.service(Http11Processor.java:495)
at
org.apache.coyote.AbstractProcessorLight.process(AbstractProcessorLight.java:66)
at
org.apache.coyote.AbstractProtocol\$ConnectionHandler.process(AbstractProtocol.java:767)
at
org.apache.tomcat.util.net.NioEndpoint\$SocketProcessor.doRun(NioEndpoint.java:1347)
at
org.apache.tomcat.util.net.SocketProcessorBase.run(SocketProcessorBase.java:49)
at
java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1142)
at
java.util.concurrent.ThreadPoolExecutor\$Worker.run(ThreadPoolExecutor.java:617)
at
org.apache.tomcat.util.threads.TaskThread\$WrappingRunnable.run(TaskThread.java:61)
at java.lang.Thread.run(Thread.java:745) Caused by:
java.io.FileNotFoundException: If you are accessing OpsHub from
different machine then change localhost to ip address of the machine
where OpsHub installed.

- **The filename, directory name, or volume label syntax is incorrect**

at java.io.FileInputStream.open(Native Method) at
java.io.FileInputStream.(FileInputStream.java:138) at
de.schlichtherle.license.LicenseManager.loadLicenseKey(LicenseManager.java:741)
at
com.opshub.license.install.OpsHubLicenseManager.getLicenseContent(OpsHubLicenseManager.java:55)

# Installation

Here is a video on how to install OpsHub Integration Manager on the Windows machine:

{% embed url="https://www.youtube.com/watch?v=1a2b3c4d5e" %}


## Select Installation Path

- You now have to select the installation directory. Before you select a directory, make sure the directory is empty. All the log files, configuration files, and servers are placed in this directory. If the directory is not available, you can create a directory as per your own specifications.
<p align="center">
  <img src="../assets/Default_Installation_Image_P3.png" alt="Default Installation Image P3" />
</p>

## Registration

- Each installation must be registered with OpsHub. Registration can be done either in Online or Offline mode.  
  Please refer [Registration](registration.md) section for more details.

# Database Selection
{% include "../.gitbook/includes/database-selection.md" %}

# Advance Installation

- Go through this section if you want to configure Advance Installation. Else, proceed to the [Installation Progress](#installation-progress) section.

<p align="center">
  <img src="../assets/Advance_Step_Installtion_Panel.png" alt="Advance Step Installtion Panel" />
</p>

Let's now learn about the steps for advance installation.

## Connection Mode Configuration

- Select the type of connection protocol you want to use for running the server. If HTTPS is selected, you need to follow one more step [SSL Certificate Configuration](#ssl-certificate-configuration) for advance installation.

## OpsHub Database Custom Configuration

- If you want to create databases manually, mark the checkbox "Check this if you will be creating databases manually". The instructions to create databases have been mentioned in the section [Manual creation of databases](#manual-creation-of-databases).
- If the checkbox "check this if you are creating databases manually" is unchecked then enter the names of the databases that you want to configure and according to the database selection in the previous stage (MySql, MS SQL/Azure SQL, PostgreSQL or Oracle) databases/schemas will get created.
- Database name can contain $, _, #, alphabets, and numbers without any space.
- If there are more than one database, give different names for each one.

## Install OpsHub server as a service

- If the application is installed as a service, the server will automatically start on system boot. You need not to start and stop the server explicitly. In case, you want to stop the services, you can go to Services, find the service and stop it manually from there.

## Data Encryption Configuration

- Advanced Data Encryption: Enables user to generate a secret key and store it in a secured location, or select an existing secret key if available. This configuration also allows the user to select the desired encryption algorithm for ensuring security of the application.

**a) Configuration for secret key location**  
User can select either of two options:

- Generate a secret key: With this option, a secret key would be automatically generated, and user needs to select location, where he/she desires to store this key.
<p align="center">
  <img src="../assets/Advance_Configuration_Image_4c.png" alt="Advance Configuration Image 4c" />
</p>

- Use the existing secret key: If user already has secret key available,then user should select this option. User needs to select path where "opshub.key" file is available to use that key.
<p align="center">
  <img src="../assets/Advance_Configuration_Image_5c.png" alt="Advance Configuration Image 5c" />
</p>

**b) Configuration for algorithm to encrypt data**  
User can select his desired algorithm from the available list to ensure security of data in application.
<p align="center">
  <img src="../assets/Advance_Configuration_Image_6c.png" alt="Advance Configuration Image 6c" />
</p>

## Installation Progress

The image below shows the overall progress of installation.

<p align="center">
  <img src="../assets/Installer_Image_8b.png" alt="Installer Image 8b" />
</p>

- Setup Shortcuts: It will add the application to the Windows program list if the operating system is Windows and will add the application to the Linux program list if the operating system is Linux. It will also create the OpsHub Integration Manager launcher.

<p align="center">
  <img src="../assets/Installer_Image_9Seta.png" alt="Installer Image 9Seta" />
</p>

## Installation Success

The image below shows a successful installation.
<p align="center">
  <img src="../assets/Installer_Image_10aa.PNG" alt="Installer Image 10aa" />
</p>

Once you have installed the application, click [Logging In](logging-in.md) to see how to get started.

# SSL Certificate Configuration
<p align="center">
  <img src="../assets/Advance_Configuration_Image_3SSLCa.png" alt="Advance Configuration Image 3SSLCa" />
</p>

It is advisable to enter the server-host name in the given field, it might create problem with IP address in some cases. Alias of the certificate should be unique.

- Enter the name of your Organizational unit.
- Enter the Organization name.
- Enter the current City or Locality.
- Enter the current Country Code. It should be alphabetic code. For
  e.g., "IN" for India, "US" for America, "AU" for Australia, etc.
- Select the number of days till when the certificate should be valid.

>**Note** : Please note with the above steps OpsHub Integration Manager will be installed with SSL configuration. But the corresponding SSL certificate imported will be self-signed. In case you want to install certificate signed by your CA authority then follow the steps given in this section [How To Import a Certificate](how-to-import-a-certificate.md) in appendix.

# Manual creation of databases
{% include "../.gitbook/includes/manual-database-creation.md" %}

# Collation change of MS SQL/Azure SQL Databases
{% include "../.gitbook/includes/collation-change.md" %}


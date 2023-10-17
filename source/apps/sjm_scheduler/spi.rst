.. include:: nav.rst

Special Security Group Adminstration 
========================================
Prior to enabling automation within special security folders, SPI must configure the application to support that group. User must go through SPI to enable automation any that does not 
inherit the default security ACLs. 

Enable automation for a new Special Security Protocol (Performed by SPI)
------------------------------------------------------------------------------------------
#. Submit ServiceNow request to create a service account. Specify the account name in the format svc_SAS_[protocol identifier]_Automation.
#. Register the corresponding security group and the port on the IIS server that will host the site in the appsettings.json file in the SASJobManager.LaunchSecheduledJobs project.
#. Create a new site on the application server in IIS manager. The same source code location is for all the SJM automation sites.
#. Create a new app pool using the identity of the service account created by IT. The password for service accounts are stored in 1Password and are only available to SAS Adminstrators.
#. Deploy the updated appsettings files to the application server and start the site


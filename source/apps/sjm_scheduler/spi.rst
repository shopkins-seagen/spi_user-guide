.. include:: nav.rst

Special Security Group Adminstration 
========================================
Prior to enabling automation within special security folders, SPI must configure the application to support that group. User must go through SPI to enable automation any that does not 
inherit the default security ACLs. 

Enable automation for a new Special Security Protocol (SPI only)
---------------------------------------------------------------------
#. Submit ServiceNow request to create a service account. Specify the account name in the format svc_SAS_[protocol identifier]_Automation.
#. Register the corresponding security group and the port on the IIS server that will host the site in the appsettings.json file in the SASJobManager.LaunchSecheduledJobs project.
#. Create a new site on the application server in IIS manager. The same source code location is for all the SJM automation sites.
#. Create a new app pool using the identity of the service account created by IT. The password for service accounts are stored in 1Password and are only available to SAS Adminstrators.
#. Deploy the updated appsettings files to the application server and start the site

Support Protocols
---------------------
The table below details the currently supported protocols. All other requests orginating from locations with default security (SAS_ClinProg_GXP) are routed to port 9010.

.. list-table::
    :widths: 20 20 20 10
    :header-rows: 1

    * - Protocol
      - AD Group
      - Service account
      - Port
    * - Tuc-016
      - SAS_SGNTUC_016_SP_Write
      - svc_SAS_Tuc016_Automation
      - 9011
    * - Tuc-028
      - SAS_SGNTUC028_Blind_SP_Write
      - svc_SAS_Tuc028_Automation
      - 9012
    * - Tuc-029      
      - SAS_SGNTUC029_CSR_UNBLIND
      - svc_SAS_Tuc029_Automation
      - 9013
    * - EV302
      - SAS_EV302_Unblinded
      - svc_SAS_EV302Restricted_Automation
      - 9014



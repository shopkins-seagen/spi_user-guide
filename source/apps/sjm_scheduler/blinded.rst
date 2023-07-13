.. include:: nav.rst

Automation for Tasks Special Security(SS) Folders
======================================================
By default, scheduled tasks run in the context of a service account with default statistical programmer access. Users are not able to use the default context to 
schedule tasks inside of a SS folder. In order to create a scheduled task in a SS folder follow the steps outlined below

#. Check the box for 'Does the analysis have custom security ACLs?'
#. Select the AD group applied to the SS folder from the dropdown list. The user registering the task must be a member of the group, and the batch file must inherit the ACL with 
   the group. If either condition is not met, the app will not allow the details to be saved.

    .. image:: ss.png

#. If the group is not available in the dropdown list, send a request to SPI to register the group in the application. To do that provide the group name and path to the .bat file 
   in an email to shopkins@seagen.com. SPI will request IT create a corresponding service account with membership in that group that is used as the identity to execute programs in  
   that location. The idenities are also members of SAS_Users and SAS_ClinProg_GXP and will have access to the infrastructure outside of the SS folder, effectively impersonating
   a member of that SS group. Once the identity is created and the service is hosted, SPI will notify the requestor that the service is enabled. There may be a signficant 
   lag due to dependence on IT to create the service account. 

.. warning::

   The SAS programs submitted by the batch file in a SS folder will have default access and access to folders that inherits the SS group only. If the programs reference another location 
   not explicitly accessible by the SS group, an access violation is returned. In cases like this it may be necessary to alter security on the folder through CS-096, or split the job 
   into two jobs under two identities. Contact SPI for complicated security configuration support.
     
.. include:: nav.rst


Macro Database Maintainence
===============================
Any member of SAS_Infrastructure_Write can update the database through the UI. The unlocked icon next to the user name in the UI indicates 
the current user has admin privs. Open the **Update Macros** page to update the database. 

In order for the application to parse the macro, the macros must be 
recorded in specific format. There is some flexibility built into the parser to handle variations, but to ensure accurate parsing adhere to the following rules.

#. Record a brief description of the macro after the Purpose: key in the macro header. The descrition may span multiple lines, but leave a space before the next section.

    .. code::

        | Purpose : Create shell for ADEQ5D.
        |
        | ----------------- Version History ------------------------------------------------------------------------

#. Record parameters in the following format        

   .. code::

       ,parameter =  <default if available> /* parameter description limited to just a single line */

#. To get Scope and Path to the SPO User Guide, Save the SPO `All Items page <https://seagen.sharepoint.com/sites/BMInfra/Lists/ADaMSDTM%20Macros/AllItems.aspx>`__ to the  
   location and file name defined in SPO extract. 

.. note:: 

    If this is not possible or the macro is already written, it can always be copied to any folder, modified to be consistent with the requirements, and uploaded from 
    that temporary location by changeing the value of Macro folder and clicking update

        .. image:: macro-folder.png
        

.. include:: nav.rst

Requirements
===========================================
Prior to configuring a new protocol, the following conditions must satisfied:

    #. The standard protocol folder structure must exists on the SAS file share 
    #. There must be at least one event recorded in the Safety and Clinical databases.  If no events have been captured in Argus, you cannot configure the protocol.
    #. IT/GSDB must configure your protocol for inclusion in the daily Argus *CASEDATA* extract. 

Once these requirements have been met, any member of DM study team (e.g. member of DG_Data_Management_646 or GEN.6610.DataManagement) can configure the 
protocol for reconciliation. 

Configure a new Protocol
-----------------------------

#. Click **Configure** > **Add new protocol** from menu ribbon 
#. Select the AE dataset using the |browse| to navigate to the data folder, typically *ALL_DATA*
#. Select the Death and Enroll datasets from the dropdown list

.. note::

    Death, Enroll, and **EOT** datasets must exist in the same folder as the AE dataset

#. Select the Argus safety dataset. Contact Tami Bowman if you are unsure of the location.
#. Update the protocol name if desired
#. Use the drop-down menus in the **Map data set variables** to associate a variable with the data point. Only variables of the expected type are displayed.        
#. Map the AE relationship to study drug to corresponding safety product

    * Move the variables from the *Available AE variables* list box to the *AE Relationship variables* list box using the |arrow_left| and |arrow_right| buttons.
    * Order the *AE Relationship variables* using |arrow_up| |arrow_down| keys to correspond to the appropriate drug in *Safety products*

    .. caution::

        You must map the AE relationship variable to the correct relationship in Argus. The application will display list of drugs associated with each ID. If the
        product descriptions do not make sense contact Tami Bowman as it's possible for drug safety to enter drugs inconsistently. Each relationship in Argus must have 
        a corresponding AE relationship variable or the app will not allow the configuration to be saved. If this happens, contact IT.  

#. Select the paths for each of the categories in the folder mapping section. The standard path is the typical location, but this can vary by protocol. Consult with programmer for best 
   location to reference the SDTM DM domain. 

    .. csv-table:: Folder Paths
        :widths: 20,30,50
        
        "Folder", "Description", "Standard Path"
        "Clinical data","Location of the Rave datasets","O:\\Data Management\\[product]\\[protocol]\\Data and Programs\\Data\\ALL_DATA"
        "Safey data","Location of the Argus datasets","K:\\Biometrics\\~GSDB\\ae_recon\\[protocol]"
        "Report","Location to write reconciliation report","O:\\Data Management\\[product]\\[protocol]\\Data and Programs\\Data\\Programs\\WORK\\SAE_RECON\\OUTPUT"
        "Log","Location to write SAS log file","O:\\Data Management\\[product]\\[protocol]\\Data and Programs\\Data\\Programs\\WORK\\SAE_RECON\\LOGS"
        "Output data","Location to write the Safety data as XLSX file","O:\\Data Management\\[product]\\[protocol]\\Data and Programs\\Data\\ARCHIVE\\SAE_RECON"
        "SDTM","Path of clinical programming SDTM dataset that contains the last exposure date variable  **rfxendtc**","O:\\Projects\\[product]\\[protocol]\\[analysis]\\[version]\\data\\sdtm"

.. note:: 

    SDTM is optional. This is used to calculate the last study drug exposure to identify if an event is within the safety reporting period. Set the SDTM path to blank to turn off this functionality.

#. Select the appropriate subject variable from the DM dataset. Determine this by comparing the values of AE.Subject with DM.[subject variable]. Select the variable with values consistent with AE.Subject. 
#. Assign the **Safety period** as the number of days after last exposure that subject is still considered in the Safety reporting period. 
#. Save the changes by clicking the *Save* button in the top left

Update an Existing Protocol
-----------------------------------

#. Select the protocol from *Select protocol* menu on the main form
#. Click Configure > Update selected protocol
#. Modify attributes as needed and click Save to persist changes to the database.

    .. warning::

        Reassigning variables in configuration will cause any saved review to be moved to the audit table.



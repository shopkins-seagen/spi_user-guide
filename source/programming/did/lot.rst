.. include:: nav.rst
    
Create and Upload LoT to PFE LoT Repository
===================================================
The List of Tables (LoT) spreadsheet identifies all the of the SDTM, ADaM, and TLF files included within a deliverable. The name of the LoT file must match the 
name of the deliverable. The LoT does not need to be regularly updated because of status changes, only if the content of the delivery changes significantly.

Create the LoT File
--------------------------
The mcr_spi_run_aim SAS macro has three parameters to control the creation of the LoT file. Use these to control the generation of the LoT file from your run aim program.  

.. note:: 

    Have the study team record their identities in the `DID User Registry <https://sgcpapp1:7051/>`__ prior to generating the LoT file the app will translate the L-Seagen accounts to 
    Pfizer network IDs for developer and tester in the LoT file. Otherwise, users must manually update the the spreadsheet with corresponding Pfizer IDs.

.. list-table:: 
  :widths: 20 80
  :header-rows: 1

  * - Parameter
    - Description
  * - CREATE_LOT_YN
    - Indicates if AIM calls the LoT API to generate the LoT file. Y- create lot. N (default) - do not create LoT
  * - PFE_DID 
    - Pfizer study identifier. Use the PFE name if one exists. You can look it up `here <https://seagen.sharepoint.com/:x:/r/sites/StatProg/_layouts/15/Doc.aspx?sourcedoc=%7bF25E609F-1E1B-4F3A-AE4E-09CFAE96D0EF%7d&file=seagen-pfizer-study-ids.xlsx&action=default&mobileredirect=true&web=1>`__ if you do not know your studies Pfizer Id
  * - DID_N
    - Deliverable suffix. This corresponds to the deliverable name in DID. It's and integer incremented by 1 for each deliverable within a study. 

Upload the LoT to DID Repository
---------------------------------------------
#. Click the *d_LoT_Folder* link on the `DID_0 <https://pfizer.sharepoint.com/sites/SDSADIDManagement/Lists/DID_0/DID_0.aspx>`__ page to navigate to the d_Lot Repository. 
#. Click the |upload| button and select Files
#. Select the LoT file under your <analysis>\\<deliverable>\\utilities\\ai\\lot d_LoT_Folder
#. Refresh the LoT file after significant changes to the inventory of files. You do not need to refresh the table for status changes.
.. include:: nav.rst

Perform SAE Reconciliation
===================================

Generate the report
---------------------------
    #. Select a protocol from the *Select protocol* menu on the main form

       .. note::

        The structure of *Relationship to study drug*  in the Safety data can change with protocol amendments that add arms or unblinding happens. This
        will generate an error in the *Variable mapping* section and will not allow the user to proceed. Contact DevBOT if this occurs. 

    #. Observe the extract dates for the Clinical and Safety are as expected. The Safety data should be extracted daily. The clinical data will have the extract date
       equal the last extraction from Rave. Do not proceed if the dates appear incorrect!
    #. Click *Run*
    #. If the comparison is successful, a "Log is clean" message is written to *SAS Log Review* box. If an unexpected message is encountered in the SAS log, it 
       will be summarized in the *SAS Log Review* window. Use the **View Outputs** > **Log** menu to see the complete SAS log file. 
    #. If there is at least one discrepancy, the application will generate a report file. If not, a message is displayed in the *Run Log* indicating no discrepancies were noted.

Review the report
-------------------------
    #. Use the  **View Outputs** > **Report** menu item to open the report. You can  also use the |browse| button on the folder paths to navigate to the folder. 
    #. Assign a status, action, and comment as necessary for each record. The data filter can be used to restrict records to those of interest (e.g. Open status).
    #. Save the report. You can save with the same name or a different name. It's recommended that suffix the report name with a flag like "_reviewed" 
       so there is no ambiguity during the upload. A report file can be saved anywhere and uploaded any time without having to run a report. 

Upload the report  
-------------------------     

    #. Click the **Upload** button in the menu bar to display the upload dialog. 
    #. Select the file to be upload and click Open.
    #. Review the *Upload results* window a summary of the status assignments. Records can be processed in three ways

        .. list-table::
           :widths: 15 85
           :header-rows: 1

           * - Result
             - Description
           * - Retired
             - A record in the *Review* table with no corresponding entry in the report is moved into *Review History*. This results when a value in critical 
               field of the record is changed. This means the record must be re-reviewed, or the data has been corrected and is no longer discrepant.
           * - Added
             - A record is added to *Review* table if the hash of all the critical fields represents a new record. 
           * - Updated
             - If a record exists in both the *Review* table and the report, and a user-controlled field is changed, the record is modified in the *Review* table. 
               The previous state of the record is recorded in the *Review History* table.
    
.. note:: 

    * You don't need to run the report to upload a file - this can be done at any time
    * The reviewer does not have to complete action and status assigments an all records to upload a report
    * You must close the file prior to uploading!
    * Do not modify any field other than those in the UI section (status, action, and comment)      
    * Use filtering on the columns, do not delete records then upload as they will be seen as *Retired*    
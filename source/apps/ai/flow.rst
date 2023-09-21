.. include:: aim_nav.rst

AIM Functionality
============================================
The table below details each action performed by AIM in sequence. 

 .. list-table:: 
    :widths: 40 60
    :header-rows: 1

    * - Step
      - Actions/Conditions
    * - Check the AI workbook
      - * Confirm AI file exists and is not locked for editing
        * Ensure the analysis folder is not locked per CS-096 by reviewing folder security as the API runs as a privileged account.
    * - Get the external macros for the analysis if indicated
      - If UseMacroDates is true, the application gets the list of all the macros used by the TLF and Dataset programs in a 
        single call to the MacroUsage database (populated by RunSAS). SPI maintains a list of macros not considered in the calculation of 
        latest macro date as they are deemed no risk to the QC status.
    * - Read, parse, and captures the records from  the following worksheets in sequence:

        #. Datasets
        #. TLFs
        #. Col_Layout
        #. Pop_set
        #. Common_footers

      - Read records from each spreadsheet into the data model and validate the data
        
        * If any worksheet is missing, return fatal error and terminate execution
        * If any expected field is missing from any worksheet, return fatal error and terminate execution
        * If a value cannot be parsed (wrong format, unexpected value for controlled field) write a warning to the log
        * If Type is invalid or Ignore_Record is true, do not process the record and write a message to the log

    * - Derive Status for TLFs and Datasets in a single call to the Status Assignment function.
      - See `Status Algorithm <status.html>`__
    * - Create the batch shell scripts 
      - * Create shell scripts and corresponding CSV files for each  dataset and TLF Type encountered during the current run 
        * Create a dynamic shell script that runs all the files. This batch file can be copied/edited to meet user requirements.   

          .. note::

            AIM will overwrite all files that do not have the read-only property set. If files are modified in this folder, set the read-only attribute to preserve changes.
                
    * - Backup the current AI file to history
      - Create history folder if it doesn’t exist. Copy both the AI and AI log to the history folder and append an ISO date suffix. If a fatal error is 
        encountered during this process, execution terminates
    * - Update the TLFs and Datasets worksheets in the AI workbook
      - * Assign or remove hyperlinks from cells linked to files on the network 
        * Set or remove auto-populated values based on the existence of external files on the network
        * Populate the data validation lists for fields with discrete values for 100 rows after the last used row in each worksheet

    * - Run consistency checks for the following and write a warning to the log if detected
      - * Duplicate TLF output numbers
        * Duplicate TLF base names
        * Duplicate dataset names
        * Length of TLF base name > 31 or length of TLF output name > 64
        * QC Reason recorded as 'First QC' after the output has a record in the DB where QC Status = QC Pass
        * QC Reason is recorded as 'Other' but Source_or_QC_Comments is not specified
        * A user-defined QC program, not consistent with the expected naming convention, is recorded, but the file does not exist in the expected location on the network

    * - If Final run, update team sign-off and validate user identities
      - * Get a list of unique user ID recorded in the TLF and Dataset worksheet from the developer, tester, spec_author, and spec_reviewer columns
        * Retrieve user properties from AD and verify the accounts are valid
        * If the account is valid update the team sign-off sheet with the user details
        * Write a warning to the log if any invalid users IDs are recorded
      
    * - Convert the AI file to native Excel
      - The library that processes the AI files saves the file as OpenXmL. The AIM calls the `http://spi:9010/api/SaveAsNativeExcel` endpoint asynchronously to convert to Xlsx 
        format so it is readable by the SAS macros
    * - If indicated, launch the get_ai.sas program in RunSAS
      - If the get_ai program exists in the pgms subfolder submit the program using RunSAS (e.g., batch job). Review the log and if any issues are detected write a warning to the AIM log and 
        direct the user to review the get_ai.log.
    * - Update the SQL database
      - * Compile the data from the AI into the `relational model <sql.html#database-schema>`__
        * If a record exists for the AI with the current date, replace the records with the new data, otherwise add the new records to the database.
    
    * - Generate the HTML log
      - * Create the overall summary table
        * List the issues detected during AIM execution
        * Create a summary table of outputs by status



        

       
        
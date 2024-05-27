.. include:: aim_nav.rst


Analysis Index
=========================
The AI workbook is the user interface for tracking the outputs and datasets for an analysis. Because this file is managed programmatically, it's critical that certain 
constraints are followed to ensure the data are not corrupted. Do not just modify the version 4 AI and use with the version 5+ AIM. 

Use the `migration utility <migrate.html>`__ to move the data from your existing AI and QCI into the v5+ AI template, or copy 
the v5 template `AI template <https://seagen.sharepoint.com/:x:/r/sites/BMInfra/Shared%20Documents/SPI%20Analytical%20Utilities/Analysis%20and%20QC%20Index/templates/analysis_index_v5_0-template.xlsx?d=we8df83e9875c49bbb3f97c0600304bd1&csf=1&web=1>`__
to your analysis and enter or paste the **VALUES** (not the formats, styles, validation lists from v4) into the workbook. 

.. list-table::
    :widths: 50 50
    :header-rows: 1

    * - *Modify as Needed*
      - *Do NOT modify*
    * - .. note:: 
            * Presentation: Colors, font size, highlighting, column/row width
            * Add or re-order Columns 
            * Add or re-order Worksheets. Adding worksheets will increase the time required to process the file as it will be larger
            * Turn on sharing per G-SP-023
      - .. error::
            * Existing column names, types, formats 
            * Existing sheet names
            * Heading rows of sign off sheet
            * Controlled terminology where there is data validation (drop down list). The application updates the data validation lists when AIM executes. 
            * Don't apply write protection


Analysis Index Column Descriptions
---------------------------------------
With the exception of Type and Program, all other columns do not require a value to be entered in the spreadsheet in order to capture the record in the database. If Type or Program 
is missing, the record will be excluded from processing and a warning is generated in the log.

.. raw:: html

  <embed>

    <span style="color: grey;"><img alt="ap" src="../../_images/auto.png">auto-populated</span>   

  </embed>
 

.. list-table::    
    :widths: 10 40 40 10 
    :header-rows: 1

    * - Column Name
      - Description
      - Valid Values
      - AI Worksheet
    * - Add_Col_Label
      - Optional; if needed, provides additional text to be added to the column labels for this specific table, below the more general column layout specified by Col_Layout_ID.  Text contained in this column will be appended as a final line to all the column labels.  
        Generally expected to be blank, "n (%)", or "n/N1 (%)"" to clarify the statistical values in the column of the corresponding output. This column is required to automate 
        the column headers, if applicable, in table outputs
      - Any text string. Use macro variables defined in env.sas for special characters
      - TLFs
    * - Auto_QC_Result |ap|
      - Displays the result of the comparison test using mcr_spi_qc_compare macro for *OutputName*. If the macro is not called for an output, the field is not populated. This value is not considered in Status assignment.
      -  
        .. list-table:: 
           :widths: 20 75
           :header-rows: 1
                        
           * - Value
             - Description
           * - Pass
             - The output passed the automated QC test in mcr_spi_qc_compare
           * - Fail
             - The output failed the automated QC test in mcr_spi_qc_compare

      - Common  
    * - Auto_QC_Finding |ap|
      - High-level text description of the category(ies) of comparisons that failed
      - One or more pipe-delimited text descriptions of the reason(s) for failure
      - Common     
    * - Auto_QC_Date |ap|
      - Datetime of the last call to mcr_spi_qc_compare for the ouptut
      - DateTime
      - Common             
    * - Base_Name
      - TLF name without table number
      - Name of the TLF without table number. Ex: t-ae.rtf
      - TLFs
    * - Class
      - Category for the TLF. 
      - Study-defined description of the TLF class. Ex: Demographics
      - TLFs
    * - Col_Layout_ID
      - Value of Col_Layout_Id selected from the Col_layout worksheet. AIM populates the dropdown from the list of available values in the Col_Layout worksheet
      - Drop-down menu populated from the discrete values in the Col_Layout.Col_layout_id column
      - TLFs
    * - Dataset_Date  |ap|
      - Last modified date of the dataset
      - Auto populated datetime
      - Datasets
    * - Dataset_Name
      - Name of the SAS dataset, extension optional
      - Single-level SAS dataset name, extension optional. 
      - Datasets
    * - Developer
      - A single user ID that identifies the last person to modify the program. Do not specify multiple users.
      - Valid user account. Ex: shopkins
      - Common
    * - External_Macro  |ap|
      - List of autocall macros compiled by the SAS program during execution using RunSAS (e.g., right-click). Retrieved from SQL database populated by RunSAS. 
      - Auto populated, comma-delimited list of SAS autocall macros 
      - Common
    * - Footnotes
      - {/} Delimited list of footnotes
      - optional string
      - TLFs
    * - Latest_Macro_Date  |ap|
      - Max modified date determined from the network files listed in the External_Macro column
      - Auto Populated datetime
      - Common
    * - Latest_Source_Data_Date  |ap|
      - Max modified date determined from the network files listed in the Source_Data column
      - Auto Populated datetime
      - TLFs
    * - Number
      - Table number
      - Table number, delimited by '.' for TLFs. Ex: 16.1.1.1 
      - TLFs
    * - Pop_Set_ID
      - Value of Pop_Set_Id selected from the Pop_set worksheet. AIM populates the dropdown from the list of available values in the Pop_Set worksheet. 
      - Discrete values in the Pop_set.Pop_set_id column
      - TLFs
    * - Priority
      - User-defined string for use by the team
      -  
        .. list-table:: 
           :widths: 20 75
           :header-rows: 1
                        
           * - Value
             - Description
           * - Cancelled
             - Status assignment algorithm sets Status to *Cancelled*
           * - [user-defined string]
             - Study team can use this field as needed. All other values are captured as free text in the DB and have no impact on Status assignment.  

      - Common    
    * - Program
      - Name of the SAS program, extension optional. Hyperlink is added if the file exists on the network.
      - File name of the SAS program, extension optional. 
      - Common
    * - Program_Date  |ap|
      - Last modified date of the SAS program
      - Auto populated datetime
      - Common 
    * - Program_Log  |ap|
      - Hyperlinked name of the SAS program log, if it exists
      - Auto populated string/hyperlink
      - Common
    * - Program_Log_Date  |ap|
      - Last modified date of the SAS program log. 
      - Auto populated datetime
      - Common 
    * - QC_Date
      - Date QC was completed by the Tester. Date component only, time is not supported.
      - Date is entered by the Tester in the format 'dd-mmm-yyyy'
      - Common 
    * - QC_Log  |ap|
      - Hyperlinked name of the QC program log, if it exists.
      - Auto populated string/hyperlink
      - Common 
    * - QC_Log_Date  |ap|
      - Last modified date of the QC program log.
      - Auto populated datetime
      - Common                   
    * - QC_Method
      - Discrete list of values to indicate QC methodology. 
      -  
        .. list-table:: 
           :widths: 20 75
           :header-rows: 1
                     
           * - Value
             - Description
           * - Independent Programming
             - Tester develops and retains code that programmatically verifies that the results of the production program meet the requirements
           * - Code Review
             - Tester reviews the production code against the department standards 
           * - Metadata Review
             - Review the metadata and confirm the annotations for analysis data sets, variables, formats, and where clauses are correct relative to data set specifications.
           * - Metadata Review + IP
             - Review the metadata and confirm the annotations for analysis data sets, variables, formats, and where clauses are correct relative to data set specifications in
               addition to independent programming. 

      - Common      
    * - QC_Program  
      - Hyperlinked name of the QC program, if it exists. The user can specify a program name to force AIM to look for that specific file, or allow the app to locate the program if the default naming convention “v-“[program name] is followed.
      - Program name specified by the user, or auto-populated if the default naming convention is followed. 
        
        .. warning::
           
            If you change the program name of an existing record, delete QC_Program if the expectation is for AIM to find the new QC program by naming convention. AIM will 
            not look for a QC program by convention if an existing value if recorded. 

      - Common
    * - QC_Program_Date  |ap|
      - Last modified date of the QC program
      - Auto populated datetime
      - Common 
    * - QC_Reason
      - Discrete list of values to indicate the reason QC was performed
      -  
        .. list-table:: 
           :widths: 20 75
           :header-rows: 1
                     
           * - Value
             - Description
           * - First QC
             - Initial QC after production program is released
           * - Spec/program change
             - QC performed after first QC in response to a modification to the program or specifications 
           * - Input data change
             - QC performed after first QC in response to an update to the source data
           * - Macro change
             - QC performed after first QC in response to an update to a dependent macro 
           * - Metadata change
             - QC performed after first QC in response change to Pop set, column layout, or row layout metadata for outputs that use E2E macros 
           * - Final QC
             - QC performed prior to delivery, typically after the analysis has been localized 
           * - Other
             - Any other QC method not described in the dropdown list. Clarify in the Source_or_QC_Comments field if needed  

      -  Common
    * - QC_Status
      - Discrete list of values that indicates the QC state of the output
      -  
        .. list-table:: 
           :widths: 20 75
           :header-rows: 1
                     
           * - Value
             - Description
           * - Ready for QC
             - Program is released for QC but testing has not yet been performed
           * - QC Fail
             - Tester determined the production program did not meet requirements or the results deviated from those of the QC program
           * - QC Pass
             - Tester determined the production program met requirements 

      - Common       
    * - Row_Layout_ID
      - This is the ID that links to the definitions (i.e., metadata) for the table row statistics defined in the Master Reporting Specifications (MRS). 
        This is used in the end-to-end metadata-driven table automation. See the `MRS Template <https://seagen.sharepoint.com/:x:/r/sites/BMInfra/Shared Documents/SPI Analytical Utilities/TFL Macros/autorep/templates/spi_template_mrs_tlf_row_layout.xlsx?web=1>`__ for more details.
      - Any ID value defined in the future row layout file
      - TLFs
    * - SB_Ignore_Record
      - Boolean that indicates if a record in AI will be processed. (Used by Safety Biometrics)
      -  .. list-table:: 
            :widths: 20 75
            :header-rows: 1
                     
            * - Value
              - Description
            * - True
              - The record is ignored; no columns are updated and it's not captured in the database
            * - [blank]
              - The record is processed normally   

      - Common  
    * - SB_Output_Folder
      - Name of the subfolder under the [analysis]\\outputs that contains the TLF files. If the value is null, AIM defaults to *tlfs*.
      - Any valid subfolder under [analysis]\\outputs. Example: adhocs (used by Safety Biometrics) 
      - Datasets          
    * - SB_Study_Folder
      - Name of the folder under the [analysis]\\data\\[category] folder that stores the protocol-specific elements in iSAFE
      - Folder name of the protocol-specific folder under the pooled level in iSAFE folder hierarchy. (used by Safety Biometrics)
      - Datasets
    * - Section_Number	
      - Required for the TLF stapler application, otherwise not used by AIM. Section number the TLF belongs in the concatenated PDF submission file
      - `See TLF Stapler User Guide <https://sgcpapp1:7011/apps/stapler/stapler.html#analysis-index-prerequisite-columns>`__
      - TLFs
    * - Section_Name
      - Required for the TLF stapler application, otherwise not used by AIM. Section name the TLF belongs in the concatenated PDF submission file
      - `See TLF Stapler User Guide <https://sgcpapp1:7011/apps/stapler/stapler.html#analysis-index-prerequisite-columns>`__
      - TLFs            
    * - Shell_ID
      - Contains the shell ID reference to the TLF Shell file.  A same shell ID may be used by multiple outputs.
      - Any valid shell ID from the TLF shell file
      - TLFs
    * - Source_Data
      - Comma-delimited list of SAS datasets (extension optional) referenced by the TLF program. If datasets other than ADaM are used, use two-level
        SAS dataset name (s and r are the only allowable librefs)
      - Ex: ADSL,S.DM, R.Consent
      - TLFs
    * - Source_or_QC_Comments
      - Free text field users may populate with relevant comments
      - [string]
      - Common
    * - Spec_Author
      - A single, valid user ID of the last person to review the specifications
      - Valid user account. Ex: shopkins
      - Common
    * - Spec_Reviewer
      - A single, valid user ID of the last person to review the specifications
      - Valid user account. Ex: shopkins
      - Common
    * - Status  |ap|
      - Auto-populated value returned from the algorithm used to identify the status of a TLF or Dataset
      -  
        .. list-table:: 
           :widths: 20 75
           :header-rows: 1

           * - Value
             - Description
           * - Not started
             - Source program not found
           * - Programming
             - TLF/Dataset not found but QC not started
           * - Ready for QC
             - TLF/Dataset found and status is Ready for QC
           * - Testing
             - QC Program exists and/or QC date is missing
           * - Tested fail
             - Tester set QC_Status to Fail
           * - Tested pass
             - Tester set QC_Status to Fail
           * - Re-test needed
             - Test set QC_Status to Pass, but a condition requires re-test 			 			 
           * - Cancelled
             - Priority is set to Cancelled	
      - Common
    * - Status_Desc  |ap|
      - Auto-populated explanation of why a particular status was assigned
      - See status algorithm
      - Common
    * - Submission
      - User-defined free-text field. Study steam determines how this field is used. 
      - [string] optional
      - TLFs      
    * - Tester
      - Single, valid user id of the last person to perform QC for the TLF or dataset
      - Valid user account. Ex: shopkins
      - Common
    * - Titles
      - {/} delimited list of titles
      - [string]
      - TLFs
    * - TLF_Date  |ap|
      - Last modified date of the TLF, if it exits
      - Auto populated datetime
      - TLFs
    * - TLF_Name  |ap|
      - Auto populated value from TLF base name and Number. Value is hyperlinked if it exists.
      - Ex: t16-01-01-01-ae.rtf 
      - TLFs
    * - Type
      - Discrete list of values that define the type of output. If this value is missing, the record is not processed. 
      -  
        .. list-table:: 
           :widths: 20 75
           :header-rows: 1
                     
           * - Value
             - Description
           * - Lookups
             - Standardized or analysis-specific reference data managed outside of EDC system
           * - Raw
             - Unmodified EDC or vendor data
           * - SDTM
             - CDISC-standardized clinical trial data
           * - ADaM
             - Analysis data 
           * - Adhoc
             - Analysis data developed to support a non-standard request (iSAFE)
           * - Derived
             - Pooled analysis data intended to support meta analysis (iSAFE)
           * - Harmonized
             - Protocol-specific data standardized to enabled pooling across platforms			 			 
           * - Common
             - Value of TLF type that indicates a records in the TLFs worksheet defines global titles and footnotes
           * - Table
             - Summary of clinical trial data
           * - Listing
             - Un-summarized raw data from a clinical trial			 			 
           * - Figure
             - Graphic summary of clinical trial data	
      - Common (only applicable values are displayed in the AI Worksheet)      
    * - Metadata_Report  |ap|
      - Auto-populated link to the metadata report for an output. Column in added by AIM if it does not already exist. 
      - link
      - TLF     
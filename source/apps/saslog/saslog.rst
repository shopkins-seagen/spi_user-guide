.. include:: saslog_nav.rst

SAS Log Report Generator
================================
The SAS Log Report Generator is a .NET Core API that reviews SAS log files for occurrences of issues in the same manner as `SAS Job Manager <https://sgcpapp1:7011/apps/sasjobmgr/logissues.html#list-of-log-issues-detected>`__ , 
and records the findings in an Excel workbook. The macro can be set up to review logs from one or more folders in an analysis. The Excel file contains columns that can be used to record 
details about log issues, if then cannot be removed from source programs. The adjudications remain associated with issue in the report when the app is re-run. 

Using the Report
-----------------------
The report is an Excel workbook with a spreadsheet for each folder included in the review that contains at least one log file. Users can update the *Accept (Yes/No)* column using the dropdown list and 
record text in the *Reason to Accept* column. No other modifications are permitted. Once records are reviewed, save the file in place. During subsequent runs, the app 
will carry the values of *Accept* and *Reason to Accept* to the new report, joining by MessageType and Message. For messages that include line number in the message text, changing the code 
may result in adjudications not matching a record. The application will archive a the current report in the history subfolder with an ISO datetime suffix prior to overwriting the file.  

Example worksheet
++++++++++++++++++++++
|ss|

.. note:: 

    The *Owner* column is parsed from the SAS program header, from the last entry in the program history section. Future release of the app will optionally capture 
    program owner from the AIM database  

Calling the Application
-----------------------------
The application is invoked from the SPI autocall macro *mcr_spi_log_review_report*. A strategy a team can use is to create a program under [analysis]\\utilities\\admin\\pgms, 
then add the macro call for the appropriate locations. Accept the default for out_dir and perform the review in this folder. This is a suggestion only, teams can implement as 
the needs dictate. 

Keyword Parameters
++++++++++++++++++++++++     

.. list-table::
    :widths: 10 40 30 20
    :header-rows: 1

    * - Parameter
      - Description
      - Arguments
      - Default/Required
    * - in_dirs
      - Pipe-delimited list of directories to search for SAS log files. Users can specify a complete path to any folder, the path to subcategory level folder (e.g. [path]\\data\\adam) 
        to include both the adam pgms and testing folders, or the category level (e.g. [path]\\data) to include all the subcategory level folders pgms and testing folders.

      - Examples:

          .. list-table::
            :widths: 20 75
            :header-rows: 1
                  
            * - Argument
              - Description
            * - in_dirs=&sdtmpath
              - Includes the SDTM pgms and testing folders in the search
            * - in_dirs=&root.\draft\data
              - Includes the pgms and testing folders for raw, adam, sdtm, and any other data subcategory folders in the search    
            * - in_dirs=&root.\outputs\tlfs\pgms|&adampath
              - Includes the TLF programs and the ADaM pgms and testing folders in the search

      - Required
    * - out_dir
      - Path to direct the log report. Users cannot name/rename the log report Excel file as the app looks for the current report to carry the adjudications forward into 
        subsequent reports
      - [folder path]
      - CURRDIR            
    * - include_clean_logs_yn
      - Boolean to indicate if SAS logs without any findings are included in the report 
      - 
        .. list-table::
            :widths: 20 75
            :header-rows: 1
                  
            * - Value
              - Description
            * - Y
              - Include all SAS logs, even those without any findings, in the report.
            * - N
              - Only include SAS logs with at least one finding in the report. 

      - N

Example calls      
++++++++++++++++++++++++

.. code-block:: python

    %include "O:\stat_prog_infra\utilities_dev\autocall\mcr_spi_log_review_report.sas";

    /*Includes all the log files in the ADaM,SDTM, and raw data pgms and testing subfolders, and the logs in the tlfs pgms and testing subfolders*/
    %mcr_spi_log_review_report(
        in_dirs=&ADAMPATH.|&SDTMPATH.|&RAWPATH.|&root.\\&draft.\outputs\tlfs          
        );

    /*Includes all the log files in the SDTM pgms and testing subfolders, including logs without any findings, and writes report in OUTDIR */
    %mcr_spi_log_review_report(
        in_dirs=&SDTMPATH.       
        ,out_dir =&outdir    
        ,include_clean_logs_yn=Y  
        );

.. note::

   Because of the infinite patterns possible for user-defined log messages, a log maybe have a message parsed incorrectly or the owner is not located as the header is non-standard. 
   If you encounter something like this, send SPI a message and that pattern will be handled. if feasible.       
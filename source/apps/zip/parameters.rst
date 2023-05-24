.. include:: nav.rst

SAS Macro Keyword Parameters
==============================================
The following table lists the available keyword parameters. Depending on the action, the only 2 required parameters are either IN_ZIP and OUT_DIR to extract files from a Zip archive, 
or OUT_ZIP and IN_SOURCE to create a new Zip archive. The macro performs a single action, either create or extract a Zip, per call. Providing arguments for both IN_ZIP and OUT_ZIP 
in the same call will result in an ERROR. The FILTER parameter described below is a regular expression, not a wild card (e.g. *.sas or %-ae.sas). The user guide discusses 
`regular expression <regex.html>`__ and provides common examples to use in the filter. 

.. list-table::
    :widths: 10 45 45
    :header-rows: 1

    * - Parameter
      - Description
      - Valid Values
    * - IN_SOURCE
      - Path to the folder containing the files to include in Zip file creation
      - Network path (drive alias)
    * - OUT_ZIP
      - Path\filename of the Zip file to create
      - Network path (drive alias)
    * - FILTER
      - Regular expression, not a wild-card, used to filter files when creating a new Zip, or extracting files from an existing Zip. Expressions are case-insensitive by default. 
      - See `Regex Patterns <regex.html>`__
    * - INC_SUBFOLDERS_YN
      - Indicates if the app considers files in subfolders under IN_SOURCE for inclusion into the Zip file
      -       
        .. list-table:: 
           :widths: 10 50
           :header-rows: 1
                        
           * - Value
             - Description
           * - **N**
             - Do not include subfolders
           * - Y
             - Do consider files in subfolders for inclusion 
    
    * - MAX_FOLDER_DEPTH 
      - Positive integer that limits the depth of nested subfolders under IN_SOURCE that are considered in Zip file creation. 
      -       
        .. list-table:: 
           :widths: 10 50
           :header-rows: 1
                        
           * - Value
             - Description
           * - **0**
             - Considers all subfolders
           * - [positive integer >0]
             - Threshold of the depth of subfolders to consider. '1' searches folder directly under IN_SOURCE
    
    * - IGNORE_HISTORY_YN
      - Optionally excludes folders named 'history' from consideration in Zip file creation
      - 
           * - Value
             - Description
           * - **Y**
             - Exlude files in history from the Zip file
           * - N
             - Consider files in history for inclusion in the Zip file    

    * - IN_ZIP   
      - Path\\file name of the Zip file to extract
      - Network path (drive alias)     
    * - OUT_DIR  
      - Location to extract file from Zip file
      - Network path (drive alias)
    * - IGNORE_FOLDER_LIST     
      - Space-delimited list of specific folders to exclude from processing during the creation of Zip file, case-insenstive. 
      - 
    * - OVERWRITE_ZIP_YN
      - Indicates if the app will overwrite an existing Zip file if the read-only attribute is not set. The app will never overwrite read-only files.
      - 
           * - Value
             - Description
           * - **Y**
             - Overwrite existing Zip file
           * - N
             - Do not overwrite existing Zip file

    * - KEEP_DIR_STRUCTURE_YN
      - Indicates if the app keeps the relative paths of the files during Zip creation and extraction. A warning is generated when this option is set to N but files with the 
        same name exist in different relative paths. 
      - 
           * - Value
             - Description
           * - **Y**
             - Keep the relative paths of the files in the Zip and extraction
           * - N
             - Remove the relative paths. All files will be in the same level in the Zip or the same folder in the extract.

    * - SPI_DEBUG_YN 
      - Turns on/off debugging features
      - 
           * - Value
             - Description
           * - **N**
             - Debugging is turned off for the macro
           * - N
             - Debugging is enabled for the macro
 

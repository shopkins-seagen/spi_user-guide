.. include:: aim_nav.rst

Running Analysis Index Manager
=================================


.. AIM can be run from a client machine either via a command-line utility (SPI context menu item) or .BAT file, or by sending a Post request to the API endpoint. While there 
.. are many ways to send an API request, the scope of this documentation will only include PROC HTTP from within a SAS program file.

.. Regardless of how AIM is run, it is critical that the log file be reviewed. The log file lists the overall status, details each issue detected, and provides a summary 
.. table of the output and dataset metrics for the run. Errors need to be addressed, Warnings typically are related to data issues that don't affect the execution of AIM, while 
.. NOTEs and Informational messages are less critical or purely informational. 

.. .. note::
..     An error in the get_ai.sas program is not related to the execution of the AIM. AIM only launches the file. If an issue was detected in get_ai.sas, review get_ai.log 
..     to determine the issue.

Launch AIM from SAS
--------------------------------------
AIM can be run using the department macro **mcr_spi_run_aim**. Create a new SAS program program, *run-aim.sas*, in the <analysis>\\utilities\\ai\\pgms folder. Paste the code below 
into that program after %include "init.sas";. Modify the arguments as appropriate for your study. 

.. code-block:: python

   /* Macro call from [analysis]\utilities\ai\pgms */
   %mcr_spi_run_aim( in_ai_dir = &aipath.
                    ,in_ai_fil=analysis_index_v5_0.xlsx
                    ,latest_macro_dates_yn=Y
                    ,run_get_ai_yn=Y
                    ,final_run_yn=N);

.. warning::

   Do not place the macro call in init_supp.sas. This will crash the SAS Application server. As a general rule, don't put any macro calls directly into init_supp.sas without approval from 
   the study lead programmer. See the init_supp.sas `user guide <https://sgcpapp1:7011/programming/environment.html#init-supp-sas>`__ for guidance on content of init_supp.sas if you have questions.

Keyword Parameters
--------------------------
The keyword parameters for mcr_spi_run_aim are described in the following table.      

.. list-table::
    :widths: 10 40 30 20
    :header-rows: 1

    * - Parameter
      - Description
      - Arguments
      - Default/Required
    * - in_ai_dir 
      - Path to the directory where the analysis index file exists. Use drive alias e.g. O: not a UNC path e.g. \\\\sgsasv1\\Biometrics
      - Ex: O:\\Projects\\Training\\aim\\csr\\production\\utilities\\ai\\analysis_index_csr.xlsx 
      - Macro variable: AIPATH
    * - in_ai_fil 
      - Name of the analysis index file. The default is analysis_index_&analysis..xlsx
      - Ex: analysis_index_csr.xlsx 
      - analysis_index_&analysis..xlsx      
    * - latest_macro_dates_yn
      - Boolean to indicate if status assignment algorithm will use latest macro dates from SAS macros referenced by TLF and dataset creation programs. 
      - 
        .. list-table::
            :widths: 20 75
            :header-rows: 1
                  
            * - Value
              - Description
            * - Y
              - Identify and use the latest macro date in the status assignment algorithm.
            * - N
              - Do not identifies and use latest macro date to calculate status. 

      - Y
    * - run_get_ai_yn
      - Boolean to indicate if the *get_ai.sas* program is launched by AIM    
      - 
        .. list-table::
            :widths: 20 75
            :header-rows: 1
                  
            * - Value
              - Description
            * - Y
              - Launch 'get_ai.sas' if it exists.
            * - N
              - Do not launch 'get_ai.sas'

      - Y
    * - final_run_yn 
      - Boolean to indicate if the app will execute the final run activities. 

        * Update the Team Sign-off page
        * Validate the values of user identity recorded in the developer, tester, and spec author/reviewer columns. 

      - 
        .. list-table::
            :widths: 20 75
            :header-rows: 1
                  
            * - Value
              - Description
            * - Y
              - Execute the final run activities 
            * - N
              - Do not execute the final run activities 

      - Y     
    * - create_lot_yn 
      - Boolean to indicate if the app creates the List of Tables spreadsheet in the \\ai\\lot subfolder. LoT is used by Pfizer for DID. Nightly scheduled AIM jobs always create LoT. 

        * Update the Team Sign-off page
        * Validate the values of user identity recorded in the developer, tester, and spec author/reviewer columns. 

      - 
        .. list-table::
            :widths: 20 75
            :header-rows: 1
                  
            * - Value
              - Description
            * - Y
              - Create the LoT spreadsheet
            * - N
              - Do not create the LoT spreadsheet

      - N            
    

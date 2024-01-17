.. include:: nav.rst

MCR_SPI_SDTM_CRF_ANNOTATOR
===============================
The mcr_spi_sdtm_crf_annotator macro provides the interface to the .NET Core API that provides the functionality. Given that it can do two separate operations 
based on the value of Action, required parameters are dependent on the value of Action. 

Parameters
--------------------------
|req| indicates parameters that are required regardless of Action. 

.. list-table:: 
  :widths: 20 50 30
  :header-rows: 1

  * - Parameter
    - Description
    - Valid Values
  * - spec_file |req|
    - The path\\filename for the output (action=S) or input (action=A) specfications workbook. 
    - Excel workbook saved to network 
  * - in_unique_crf
    - DM-created file that lists the unique CRFs in PDF format. 
    - See `Unique CRF <annotate_crf.html#unique-crf-pdf>`__  for details on acceptable file format. Required if action=A.  
  * - in_crf_tree
    - DM-created file that lists the forms by visit. Used to generate the Visits bookmarks. 
    - Required if action=S
  * - in_sds
    - EDC programmer-created Excel workbook that captures the form, field, and visit metadata 
    - Excel workbook saved to network. Required if action=s
  * - action |req|
    - Indicates what function the application performs; specification file creation or crf annotation.
    - .. list-table:: 
        :widths: 20 80
        :header-rows: 1
        
        * - Value
          - Description
        * - S
          - Create the specifications file 
        * - A
          - Annotate the CRF

  * - rgx_form_prefix
    - The prefix the app uses to location the name of the form in the form header. 
    - Default: form:\\s*
  * - spi_debug_yn
    - Toggles debug logic in macro 
    - .. list-table:: 
        :widths: 20 80
        :header-rows: 1
        
        * - Value
          - Description
        * - N (default)
          - Disabled debuggin logic          
        * - Y
          - Enables debugging logic

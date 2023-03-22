.. include:: nav.rst

TLF Stapler
======================
The TLF stapler is a .NET Core API that creates a single PDF file from a collection of TLFs(in PDF format) using the metadata in the Analysis Index (AI) to define 
the content of the output file. The TLF stapler is is called via a HTTP POST request using a the SAS macro mcr_spi_tlf_stapler. The SAS macro is responsible for 
making the request via PROC HTTP and parsing the response from the API back into the SAS log as SAS log lines.

Analysis Index Prerequisite Columns
-------------------------------------------
Before the stapler can be used, the AI file must have columns for Section_Number and Section_Name created and populated for each output intended for inclusion in the 
output file.  Guidance for numbering sections can be found in the `TLF Standards Output Numbering Guide  <https://seagen.sharepoint.com/:w:/r/sites/DataStandardsCommittee/_layouts/15/Doc.aspx?sourcedoc=%7BB29CCA27-E946-4E26-AF45-DAA47A827D75%7D&file=CSR-output-numbering-guide.docx&action=default&mobileredirect=true>`__


.. list-table::
    :widths: 20 40 40
    :header-rows: 1

    * - Column
      - Description
      - Example
    * - *Section_Number*
      - Section number is the primary sort value for document. The numeric components of Section_Number are parsed and left-padded with zeros to enforce alphanumeric sorting.
      - 14.1
    * - *Section_Name*  
      - The table of contents entry for the Section
      - Disposition and Protocol Deviations

.. note::

   

Launch the TLF Stapler
------------------------------
The TLF Stapler API is launched from a SAS program in a pgms folder that calls the mcr_spi_tlf_stapler macro. Below is a sample call to the stapler macro. If necessary, a call 
to the `mcr_spi_convert_rtf_to_pdfdoc <https://seagen.sharepoint.com/:w:/r/sites/BMInfra/Shared%20Documents/SPI%20Analytical%20Utilities/General%20Use%20Macros/mcr_spi_convert_rtf_to_pdfdoc/user_guide_mcr_spi_convert_rtf_to_pdfdoc.docx?d=w6327625a407144ce805f131aab838e48&csf=1&web=1>`__ macro to convert all the RTF files to PDF can be added prior to the call to the stapler.  

Example Macro calls
+++++++++++++++++++++++++
.. code-block:: python

    /* Default */
    %mcr_spi_tlf_stapler(in_pdf_dir =&outdir.
                        ,out_pdf_dir=&outdir.
                        ,out_pdf_title=%str([Protocol]FDA Meeting)
                        ,out_pdf_fil=[protocol]-fda-meeting.pdf
                        ,in_ai_dir=&aipath.
                        ,in_ai_fil=analysis_index_FDA_meeting.xlsx);

    /* Only include tables */
    %mcr_spi_tlf_stapler(in_pdf_dir =&outdir.
                        ,out_pdf_dir=&outdir.
                        ,out_pdf_title=%str([Protocol]FDA Meeting)
                        ,out_pdf_fil=[protocol]-fda-meeting.pdf
                        ,in_ai_dir=&aipath.
                        ,in_ai_fil=analysis_index_FDA_meeting.xlsx
                        ,tlf_type=T);

    /* Filter records using an equality comparison foruser-defined column */
    %mcr_spi_tlf_stapler(in_pdf_dir =&outdir.
                        ,out_pdf_dir=&outdir.
                        ,out_pdf_title=%str([Protocol]FDA Meeting)
                        ,out_pdf_fil=[protocol]-fda-meeting.pdf
                        ,in_ai_dir=&aipath.
                        ,in_ai_fil=analysis_index_FDA_meeting.xlsx
                        ,tlf_type=T
                        ,filter=submission:Yes);





SAS Macro Keyword Parameters
-----------------------------------
The keyword parameters for mcr_spi_tlf_stapler are described in the following table. Default values are indicated by |default| and can be omitted from the call if the default 
is the desired value.

.. list-table::
    :widths: 10 40 30
    :header-rows: 1

    * - Parameter
      - Description
      - Arguments
    * - in_pdf_dir 
      - Path to the PDF versions of the TLFs
      - [analysis]\\outputs\\tlfs
    * - out_pdf_dir
      - Path to the location to create the concatenated PDF file
      - [analysis]\\outputs\\tlfs
    * - out_pdf_fil
      - Name of the concatenated PDF file created by the macro
      - [filename].pdf
    * - out_pdf_title
      - Optional title that appears above the TOC on first page of report.
      - [Protocol] Integrated Summary of Safety     
    * - in_ai_dir
      - Path to the location of the analysis index file
      - &aipath |default|
    * - in_ai_fil
      - Name of the analysis index file
      - [ai].xlsx
    * - tlf_type
      - Discrete list that restricts the files that are included in the concatenated file by TLF type. 
      - 
        .. list-table::
            :widths: 20 75
            :header-rows: 1
                  
            * - Value
              - Description
            * - All |default|
              - All files are included                 
            * - T
              - Only tables are included in the concatenated file.
            * - L
              - Only listings are included in the concatenated file.
            * - F
              - Only figures are included in the concatenated file.     
                     
    * - sort_column
      - Name of the column in AI that is used to sort the outputs. To order outputs differently than table number, users can create a custom column. Internally, the app
        evaluates sequence using character values. If the custom column uses integers, set PAD_SORT_COLUMN_YN=Y.
      - Number |default|
    * - pad_sort_column_yn
      - Indicates if the app will pad numeric components. The app will also split text strings delimited by periods(e.g. Number) and pad each component to enforce the expected alphanumeric sequence. 
      - 
        .. list-table::
            :widths: 20 75
            :header-rows: 1
                  
            * - Value
              - Description
            * - Y |default|
              - Pads the period-delimited numeric components with leading zeros
            * - N
              - Does not parse sort_column                     

    * - create_toc_yn
      - Indicates if the app creates a table of contents from the bookmarks and inserts the TOC into the first page of the concatenated files. 
      - 
        .. list-table::
            :widths: 20 75
            :header-rows: 1
                  
            * - Value
              - Description
            * - Y |default|
              - Creates and inserts the TOC 
            * - N
              - Does not create a TOC. This can be used circumstances where the TOC has requirements that cannot be met by the app. In which case SPI can assist 
                using Adobe with ISI publisher to create a compliant TOC.                    

    * - number_pages_yn
      - Indicates if the app creates a footer in the format *Page x of y* on each page of the concatenated file. 
      - 
        .. list-table::
            :widths: 20 75
            :header-rows: 1
                  
            * - Value
              - Description
            * - Y |default|
              - Creates page x of y footer. 
            * - N
              - Does not number the pages. This can be used circumstances where the TOC needs to be created using Adobe or where Page x of y format is not acceptable. SPI can assist 
                using Adobe with ISI publisher to create compliant page numbering.                
   
    * - filter
      - Optional expression in the format [column name]:[value] that subsets outputs where column = value is true. The tlf_type restriction is evaluated 
        before filter. If the filter expression is intended to restrict all TLF types, ensure tlf_type is specified as *all*
      - priority:topline   
    * - spi_debug_yn
      - Indicates if debugging mode is enabled
      - 
        .. list-table::
            :widths: 20 75
            :header-rows: 1
                  
            * - Value
              - Description
            * - N |default|
              - Disable debugging.               
            * - Y 
              - Enable debugging



List of TLF Stapler Exceptions
--------------------------------
Below are a list of exceptions the API can return to the SAS log. ERRORS cause the execution of the stapler to terminate. WARNINGS do not interrupt the execution, 
but should be addressed in subsequent runs. 

.. list-table::
    :widths: 10 40 40
    :header-rows: 1

    * - Exception type
      - Message
      - Corrective action
    * - ERROR 
      - The TLFs worksheet is missing from the workbook
      - Use the v5 `AI template <https://seagen.sharepoint.com/:x:/r/sites/BMInfra/Shared Documents/SPI Analytical Utilities/Analysis and QC Index/templates/v05/analysis_index_v5_0-template.xlsx>`__
    * - ERROR
      - Duplicate tables detected in AI. {TlfType} {Number} {Name}
      - Duplicate entries in the AI by type, number, and output name are not allowed
    * - ERROR
      - Duplicate TOC entries were detected for: {TlfType} {Number} {Toc}
      - Add additional titles to make the output unique or update the table number
    * - ERROR
      - The expected column 'column name' was not found in the TLFs worksheet
      - Ensure Section_Name and Section_Number columns, and any user-defined columns specified in the macro exist. If the error persists, use the v5 `AI template <https://seagen.sharepoint.com/:x:/r/sites/BMInfra/Shared Documents/SPI Analytical Utilities/Analysis and QC Index/templates/v05/analysis_index_v5_0-template.xlsx>`__ 
    * - ERROR
      - The file '{AiFn}' does not exist
      - Specify the correct AI file in the macro call
    * - ERROR
      - The file '{AiFn}' is locked for editing
      - Use the Open File Manager to close the file or determine the user that has the file opened
    * - WARNING
      - Could not evaluate filter condition for value '' of '{column}' for row {number}
      - The expression could not be evaluated for a row. confirm the data are correct for the filter condition
    * - WARNING
      - The {tlfType} could not be located
      - Ensure the PDF version of the RTF file is available 

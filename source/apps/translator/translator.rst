.. include:: nav.rst

Excel Workbook Translation Service
============================================
The Excel Workbook Translation Service(Translator) is a ASP.NET Core Web API that uses Azure Cognitive Translation Service to translate all the worksheets in an Excel workbook 
from/to any of the `supported languages listed in the documentation <https://learn.microsoft.com/en-us/azure/ai-services/translator/language-support#translation>`__. 

The app creates a copy of the document in memory, maintining all of the existing formatting, and replaces occurences of the From language text strings with the 
TO language translation. The translated document is saved as [location]\\[input file]-[to language code].xlsx. For Simplified Chinese (zh-Hans), the application only 
translates cells that contain at least one Chinese character, an optimization added to support the original request. For other languages, all cells are considered for 
translation. The app will translate substrings within a cell where a mix of the FROM and TO languages both exist. The app handles cells that are already in the TO language.

To faciliate QC of the translations, the application creates a worksheet with all the values of original and translated text. Since the app uses a third party neural network 
tranlation service to perform the actual translation, the accuracy of the translations cannot be modified. 

SAS Macro Usage
------------------------

Parameters
++++++++++++++++++++++++++++

 .. list-table::        
      :widths: 20 70 20 10
      :header-rows: 1      

      * - Parameter
        - Description
        - Valid Values
        - Default/Required
      * - IN_XLS
        - Path and name of the the file to be translated
        - Valid network Path\\Excel file 
        - required
      * - OUT_DIR
        - Path to save the translated file. The file name is automatically saved as [file name]-[to language code].xlsx, so do not specfiy a file name
        - Valid network Path
        - required
      * - FROM_LANG_CODE
        - The language code in the input file to translate from.  
        - `Language codes <https://learn.microsoft.com/en-us/azure/ai-services/translator/language-support#translation>`__ where *Cloud text translation support* is indicated.
        - zh-Hans  (Simplified Chinese)
      * - TO_LANG_CODE
        - The language code to translate text to in the output file 
        - `Language codes <https://learn.microsoft.com/en-us/azure/ai-services/translator/language-support#translation>`__ where *Cloud text translation support* is indicated.
        - en (English)
  
Example Macro Calls
++++++++++++++++++++++

.. code::

        /* Simplified Chinese to English */

        %mcr_spi_translate_excel(
            in_xls =&outdir.\original.xlsx               
            ,out_dir=&outdir.          
        ); 

        /* English to Spanish */

        %mcr_spi_translate_excel(
            in_xls =&outdir.\original.xlsx              
            ,from_lang_code=en
            ,to_lang_code=es      
            ,out_dir=&outdir.          
        ); 


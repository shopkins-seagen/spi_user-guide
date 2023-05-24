.. include:: nav.rst

Example Macro Calls
============================================
Below are a list of example patterns that can be modified to handle most situations. Couple these with the filter examples to get exactly the desired behavior. Contact SPI if you 
have an example you wanted added to help your team


Create a Zip file of just SAS datasets from a single folder
-----------------------------------------------------------------

.. code::

    %mcr_spi_zip_api(
       in_source=O:\stat_prog_infra\testing\generic-utility\mcr_spi_zip_api\v2\data\raw        
      ,out_zip=O:\stat_prog_infra\testing\generic-utility\mcr_spi_zip_api\v2\data\raw\testing\zip04-01.zip      
      ,filter = \.sas7bdat$
      );

Create a Zip file of all the data validation programs in zip without relative paths 
---------------------------------------------------------------------------------------

.. code::

    %mcr_spi_zip_api(
        in_source=O:\stat_prog_infra\testing\generic-utility\mcr_spi_zip_api\v2\data   
       ,out_zip=O:\stat_prog_infra\testing\generic-utility\mcr_spi_zip_api\v2\data\raw\testing\zip04-01.zip        
       ,inc_subfolders_yn=Y
       ,max_folder_depth=2
       ,keep_dir_structure_yn=n
       ,ignore_folder_list=pgms 
       ,filter = ^v-.*\.sas$
      );

Extract all the contents of a Zip file
------------------------------------------------------------------------------------------------------------

.. code::

    %mcr_spi_zip_api(
       out_dir=O:\stat_prog_infra\testing\generic-utility\mcr_spi_zip_api\v2\data\raw        
      ,in_zip=O:\stat_prog_infra\testing\generic-utility\mcr_spi_zip_api\v2\data\raw\testing\zip04-01.zip 
      );


Extract all the PDFs and Docx files in a Zip into a single folder, without maintaining the relative paths
------------------------------------------------------------------------------------------------------------

.. code::

    %mcr_spi_zip_api(
       out_dir=O:\stat_prog_infra\testing\generic-utility\mcr_spi_zip_api\v2\data\raw        
      ,in_zip=O:\stat_prog_infra\testing\generic-utility\mcr_spi_zip_api\v2\data\raw\testing\zip04-01.zip 
      ,keep_dir_structure_yn=n     
      ,filter = \.(pdf|docx)$
      );
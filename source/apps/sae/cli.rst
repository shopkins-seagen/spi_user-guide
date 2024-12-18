.. include:: nav.rst

Perform SAE Reconciliation
===================================
Prior to performing SAE reconciliation, you must install the content menus on your SAS VM or PC. To do this, open the `content menu libary <https://sgcpapp1:7011/programming/registry/library.html>`__ 
and look for the card that says *SAE Recon App*. Click the download button to save the zip file to your machine. Open the downloads folder and right-click on the sae.zip file 
and select 'extract all'. Double click the sae.reg file extracted from the zip archive to install the context menus. 
See `installing context menus <https://sgcpapp1:7011/programming/registry/add.html>`__ for details about how to install context menus if you encounter difficulties.

Generate the report
--------------------------------
Generation of the SAE report is no longer done through the SAE Recon Tool/GUI desktop app. Use the context menus to call a hosted service to perform the report generation. 

#. Navigate to the folder that contains the Argus safety data for your protocol. This can be found in *O:\\Data Management\\ae_recon\\data\\derived\\[protocol]*. 
#. Right-click on the casedata.sas7bdat file and select **SAE: Generate Report**. 
#. Review the discrepancies in the report located in *O:\\Data Management\\[product]\\[protocol]\\DATA AND PROGRAMS\\PROGRAMS\\WORK\\SAE_RECON\\OUTPUT*

Upload the Results
---------------------------
After the output/report is adjudicated per BP-0389 Serious Adverse Events Reconciliation, 
upload the output/results to the database.  This will bring forward comments for next rune.

#. Navigate to the folder that contains the report.
#. Right-click on the Excel file and select **SAE: Upload Results**

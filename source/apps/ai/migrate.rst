.. include:: aim_nav.rst


Migrate Version 3+ AI and QCI into Version 5 AI 
========================================================
SPI provides a utility to support migration of the contents of existing AI and QCI files (version 3 and higher) into the new AI version 5 template. The API joins the QC details in the 
QCI file (Developer, Tester, Reason, Method, Findings, QC date and Status) to the output/dataset data in AI by program name to populate the AI v5 template. The migrator does not copy 
derived fields or update validation lists for columns with discrete values as these are handled by AIM the first time the AI is processed.

Instructions
---------------------------------
#. Create the json file in the format below and save as json.txt in C:\\users\\[username]. Be sure to change the path separator from single slashes *\\* to double slashes *\\\\*. 

    .. code:: python

        {"aifn":"O:\\Projects\\Training\\aim\\v4_3\\production\\utilities\\ai\\analysis_index_file.xlsx",
         "qcifn":"O:\\Projects\\Training\\aim\\v4_3\\production\\utilities\\ai\\qc_index_file.xlsx"}

#. Open a console window and ensure the current folder is the same as the folder where the json.txt file created in the previous step is saved. Paste the command:

    .. code:: python

        CURL http://spi:9070/api/migrate -H "Content-type:application/json" -X POST -d @json.txt

#. Review the JSON response. MsgType should be 1 (success), Msg points to the newly created AI file. If you get a different message, ensure your json.txt file is correct, and you have 
   write access to the location where the AI and QCI file exist. If not, just move the Ai and QCI to a different location, it doesn't matter where. 

    .. code:: python

        [{"msgType":1,"msg":"AI and QCI migrated into v5 AI 'O:\\Projects\\Training\\aim\\v4_3\\production\\utilities\\ai\\analysis_index_csr_1643_v5.xlsx'","method":"Ai.Migrate"}]

#. Create a SAS program to call AIM v5 (AIM v5 is not called via right-click). See instructions `here <http://sgcpapp1/cp/apps/ai/run.html#launch-aim-from-sas.html>`__ . AIM v5 
   will update the derived columns as appropriate. 
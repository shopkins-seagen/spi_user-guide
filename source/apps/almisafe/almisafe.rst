.. |add| image:: add.png
.. |delete| image:: delete.png
.. |edit| image:: edit.png
.. |list| image:: list.png
.. |sort| image:: sort.png
.. |studyadd| image:: studyadd.png
.. |studyremove| image:: studyremove.png


iSAFE Study Manager
=================================
The iSAFE Study Manager(ISM) allows the iSAFE team to create analyses and associate one or more studies with an analysis to enable the protocol-specific level folder creation in 
iSAFE ALM. The application replaces the analysis and data source management functionality in Candid. In the Candid workflow, the Candid admin creates and manages study 
data sources, and the user creates analyses and adds those data sources. In ISM, the user is responsible for creating and managing studies and analyses.
The source of the analysis metadata is the ISM database as there are no longer any dependencies on the Candid database. 

Invoke ISM from I:\\apps_stratus\\iSAFE DataSource Manager [UAT]

Manage Studies
---------------------------------------
Before creating or updating an analysis, ensure the desired studies exist in the Available Studies listbox. The name of the study becomes the protocol-specific subfolder for the analysis when the folders are created in ALM. 
Use the controls described in the table to below to define the desired study data source. The controls for study are located inside the study group box and along the right 
margin. 

  .. list-table::        
      :widths: 20 80
      :header-rows: 1      

      * - Button
        - Function
      * - |add|
        - Create a new study data source item
      * - |edit| 
        - Modify the text of the study data source. The study ID will not change. (study ID is the prefix that appears in the references at the pooled level in env.sas)
      * - |delete|
        - Delete a study data source from the database. This is only allowed if no analyses reference the study. 
      * - |list|
        - Deselects the current analysis and displays all the available studies in the database
      * - |sort| 
        - Sort the studies in the opposite alphanumeric sequence of the current states

.. note:: 

    This step was performed by the Administrators in Candid, but is performed by the users in ISM. 

Manage Analyses
-----------------------
This step is very similar to the workflow in Candid. Users create or update an analysis, then add or remove studies as needed during the lifecycle of the analysis. 

  .. list-table::        
      :widths: 20 80
      :header-rows: 1      

      * - Button
        - Function
      * - |add|
        - Create a new analsis. The analysis appears in ALM as the ISM Id number (formerly Candid ID) | analysis name. Use descriptive names (not CSR)
      * - |edit| 
        - Modify the text of the analysis name. This does not effect value of ISM Id, just adds clarity when selecting the analysis in ALM. 
      * - |delete|
        - Delete an analysis from the ISM database
      * - |studyadd| 
        - Located between the Selected and Available Study listboxes. This associates the selected Available Studies with the selected analysis
      * - |studyremove|  
        - Located between the Selected and Available Study listboxes. This disassociates the selected Selected Studies from the selected analysis         

Manage the Analysis Folders
-----------------------------------
Once the analysis is configured in ISM, launch iSAFE ALM (I:\\apps_stratus\\iSAFE ALM v3.1.2 [UAT]) to create the analysis on the file system. 

.. note:: 

    Analyses with only a single study DO NOT require a dummy analysis to create the protocol-specific folders anymore. iSAFE ALM always creates the protocol-specific 
    folders regardless of the number of data sources. 
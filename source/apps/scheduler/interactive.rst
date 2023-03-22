User interface in *FAST* Automation Manager
=======================================================

.. include:: nav.rst

While in the automation manager application, users can execute elements of reports defined in the application. The functionality of the various controls is defined in the table 
below. |br|

|rule|



.. list-table::
  :widths: 10 10 80
  :header-rows: 1

  * - Control
    - View
    - Function 
  * - .. image:: _static\gears_16_blue_2f48ee.png
    - Report
    - Displays the report configuration view (e.g. Schedule, Transfer, and Email configuration views)
  * - .. image:: _static\delete-blue-16.png
    - All
    - Deletes the current record
  * - .. image:: _static\file-code-_16_0_2f48ee_blue.png
    - Report
    - Runs the SAS programs in the driver file for the current record ith selected error tolerance. 

       .. note::

            * Does not perform file transfers
            * Does not send emails
            * Does not update the RunLog table in the database
            * Creates SAS log summary but does not send notification to admin
         
  * - .. image:: _static\run_and_transfer_16_0_2f48ee_blue.png
    - Report
    - Runs the SAS programs in the driver file and performs files transfers for the current record with selected error tolerance.  
    
       .. note::

            * Performs file transfers
            * Does not send emails
            * Updates the RunLog table in the database
            * Creates SAS log summary but does not send notification to admin

  * - .. image:: _static\run_16_blue_2f48ee.png
    - Report
    - Runs the SAS programs in the driver file and performs files transfers and distributes emails for the current record with selected error tolerance.  
    
       .. note::

            * Performs file transfers
            * Sends emails
            * Updates the RunLog table in the database    
            * Create SAS log summary and sends notification to admin   

  * - .. image:: _static\mail_16_0_2f48ee_none.png
    - Report
    - Distributes the emails for the selected report, optionally by date.  
    
       .. note::

            * Does not perform file transfers
            * Sends emails
            * Updates the RunLog table in the database    
            * Sends notification of email status to admin                  

  * - .. image:: _static\folder-open-o_16_0_2f48ee_blue.png
    - Report, Transfer
    - Opens the location of the report element in the file browser.  
    
  * - .. image:: _static\unlink_16_blue_2f48ee_none.png
    - Email
    - Removes the selected link from the email message.    

             
       




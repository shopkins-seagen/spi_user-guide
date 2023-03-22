Create a new SAS Job
=======================================

.. include:: nav.rst

Invoke the Automation Manager from I:\\apps\\FAST ([dept]) then follow steps below to manage automated reports.

**Add a record in Report, Transfer, or Email**
-------------------------------------------------------
  #. Click in the first column of top row in the table to open the editor
  #. Enter values into the required columns 
  #. Tab past the last column. If the data is acceptable, the application will insert the row into the database
  #. To enter email recipients, use the **+** to expand the email record and follow the steps above

    .. note::

      You can use **ESC** to cancel the new record editor

**Update a record in Report, Transfer, or Email**
-------------------------------------------------------
  #. Click in the cell to invoke the editor and update the values
  #. Click the Save button at the top of the grid to commit all pending changes for the table, or Cancel to abandon pending changes

   .. note::

      For updates to email recipients, use the |SAVE| button on the row in the recipient table

**Schedule the report**
-------------------------------------------------------   
  #. Click in the |GEAR| on the report to define the schedule
  #. Double-click (or use column/row head to select all) a cell to select
  #. When the desired months/days are selected, click the **Save** button at the top of the section to commit changes, **Cancel** to abandon changes.

**Report definition**
---------------------------------
In the context of this application, a *report* is collection of related programs executed sequentially with 
optionally imposed conditions based on program status. A report is very similar, but not analogous to an analysis in that a report could consist of multiple analyses. |line|
A report consists of four components defined in the table below |rule|

    #. **Report** - The parent object that contains the definitions of all the functionality. 
                  

        .. list-table::        
          :widths: 20 80  
          :header-rows: 1

          * - Property
            - Description
          * - Title
            - Unique text identifier for the report.
      





.. include:: aim_nav.rst

Analysis Index Manager Version 5 Scheduler
============================================
The Analysis Index Manager Scheduler (AIM Scheduler) allows users to automate nightly execution of the Analysis Index Manager.

Configure AIM for Nightly execution
----------------------------------------
#. Open the application by navigating to I:\\apps_stratus and double-click the AIM Scheduler shortcut 
#. Use the |select| button to select an AI file for your analysis. 
#. Use the |add| button to add the AI file to the list of AI files to include in the nightly run
#. Navigate to the new entry and set the appropriate run time attributes.

    * Include - Check this box to enable execution in AIM. Uncheck the box to disabled execution without deleting the entry. 
    * Run Get AI - Check the box to have AIM run the get_ai.sas program for your analysis. 
    * Use Macro Dates - Check the box to have AIM retrieve the last modified date for department macros called from the program. This date is used in the status assignment algorithm 
      for Re-Test conditions.

    *  Configure the notification - only occurs during automated runs, not when AIM is run interactively. 

        * *Notify*: The user that will receive an email notification from AIM based on the notification threshold selected. 
        * *Notification threshold*: an enumerated list of threshold values compared to the overall status of the AIM run. If the selected threshold is greater or equal to the AIM status, a notification is sent to the user in the Notify column.

            .. list-table:: Threshold values
                :widths: 25 60
                :header-rows: 1

                * - Value
                    - Description
                * - All (1)
                    - Always send a notification when automated AIM run completes
                * - Warning (2)
                    - Send notification if any AIM warnings are raised during execution. AIM warnings typically don't affect the outcome of AI or QCI. 
                * - Error (3)
                    - Send notification in any AIM errors are raised during execution. Errors are conditions that must be corrected as they impact the 
                    quality of the data, but do not interfere with the actual execution of AIM. 
                * - Fatal (4) 
                    - Sends a notification in the event of an unexpected exception that prevents the successful execution of AIM. 
                    

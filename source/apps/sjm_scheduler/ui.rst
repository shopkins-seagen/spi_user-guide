.. include:: nav.rst

.. |new| image:: new-task-button.png

.. |save| image:: save-button.png

.. |cancel| image:: cancel-button.png

.. |changes| image:: changes.png

.. |export| image:: export.png

.. |select| image:: select.png


SJM Scheduler UI
=========================
The UI provides functionality for users to create, update, or delete a scheduled task. The UI also display a run log that details each time the job was successfully executed. Users can 
view the currently scheduled jobs by down using the |export| button, which downloads a spreadsheet with a frequency of jobs x day. This can be helpful to choose a less busy time 
to schedule a task. 

Create a New Scheduled Task
----------------------------------
#. Click the |new| button to display the Create new task menu. 
#. Enter a description in the format Protocol Identifier_Deliverable_Purpose. Example: *SGNXX-001_CSR_Raw data refresh*. While this isn't enforced as some elements might 
   not be applicable, it will make the task easier to find later. There is task filter that filters jobs by keystroke as well.
#. Select the SJM batch file by clicking the |select| button to bring up the file selection dialog. For jobs that access special security(SS) folders, the batch file must exist under 
   the folder where the security is applied and the user must be a member of the AD group that provides access. For default security(DS) jobs, the file can reside at any 
   level in the folder hierarchy and be created by any member of SP.
#. Click the |save| button to add the new job to the database, or |cancel| to discard. Once saved, the app displays the scheduling details for the selected job in the right pane.
#. By default, the 'Recurring' check box is checked. This indicates the jobs will execute weekly. If this is a one-time job, uncheck 'Recurring?'. This will cause the job 
   to execute once, then automatically disable itself. To run the job again, enable the job within 7 days prior to scheduled execution. To temporarily disable a job, unchecke the 
   'Enabled' checkbox.
#. If the job accesses locations that have special security, check the 'Does the analysis have custom security ACLs' box and select the AD group with modify access     
   on that location. Only members of the special security group can schedule tasks that access restricted folders. If the AD group needed to access for a job  is not available in 
   the drop-down menu, contact SPI to register the appropriate group. Since each registered group requires IT to create a corresponding identity, this process can take a while.
   See `special security <blinded.html>`__ for more details on restricted folders.
   
    .. warning::

      Using default security for a job in a restricted folder will result in an access violation exception. Only locations accessible by SAS_ClinProg_GXP can be scheduled without
      specifying a security group. 

#. Select the day(s) of the week for the job to execute, and select the hour (0-23) to execute the program. Use |export| to view all the jobs if you have a resource intenstive job 
   to ensure there is sufficient server availabilty.
#. Once the changes are made, the |changes| indicator is displayed in the upper right. Click |save| in the upper right corner to save the scheduling details. The |cancel| button in the 
   upper right will discard unsaved changes.

.. note:: 

    You can select a job in the left pane and edit scheduling details at any time. Be sure to disable (uncheck 'Enabled?') or delete jobs that are not active to preserve bandwith. 

Run a Scheduled Task on Demand
----------------------------------
The |run| button allows users to send a job for execution on the server using the same configuration as the SJM Scheduler Task Launcher. The job is launched without any
connection to the user's computer. If the computer that submitted the job is diconnected from the network, the SAS process continues uninterrupted. Notification of completion 
is provided by using -n true and -u [username(s)] in the .BAT file. The app will display an optional prompt to update the .BAT file with notification arguments if -n is not 
true or the current user isn't listed in the -u parameter. 

The job runs in the context of the service account associated with security group defined for the job. If no special security group is defined for a job, it runs under the 
default permissions for O:\\Projects. While only a member of  a special security group can create and scheduled task that references a location under special security folder, 
any user can submit an existing job without being a member of the group. 

Run Logs
--------------------
Each time a job is successfully launched, an entry is recorded in the Run Log and is accessible by selecting the job in the left pane. The application records the start and end times 
for the job, and the worst SAS error condition encountered during the entire job execution. Click a run log to view the SJM application notifications generated during execution.

.. image:: runlog.png



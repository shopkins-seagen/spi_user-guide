.. include:: nav.rst

Interactive Submission of a Scheduled Task
======================================================
SJM supports two approaches for a user to launch a scheduled task interactively:

    * `Manually launch the job from the SJM Scheduler <interactive.html#manually-launch-the-job-from-the-sjm-scheduler>`__
    * `Invoke the job from a call to mcr_spi_launch_sjm_job in a SAS program <interactive.html#mcr-spi-launch-sjm-job>`__

Each method will launch the task on a new thread not monitored by the 
client application. Execution takes place entirely on the application server without a connection to the user's device. If the device that launched the job 
is disconnected from the network, the job continues to run uninterrupted. 

The user that launches the task does not need to be able to access the location on the file server, but must be listed as a recipient for notification of 
completion in the associated .BAT file in the -u parameter. 

As with normal execution, the job executes as the service account associated with the security group recorded for the job in the UI. If no group is recorded, 
the job executes using the default security for Statistical Programming (SAS_ClinProg_GXP). If you try to reference an area controlled by a special security 
group without an appropiate account created by SPI, the task will fail. 

When a successfully launched job completes, users recorded in the -u parameter will recieve an email notification. 

Manually launch the job from the SJM scheduler
----------------------------------------------
Users can launch a scheduled job on demand by clicking the |run| button in the UI. 

MCR_SPI_LAUNCH_SJM_JOB
------------------------------------------------
User can call the **mcr_spi_launch_sjm_job** macro to launch a job from within a SAS program. The parameter IN_JOB accepts the value of *Description* recorded for the job recorded 
in the SJM scheduler. If the macro is able to successfully launch the job, a NOTICE indicating the job was launched is displayed in the SAS log and a global macro 
variable SPI_SJM_LAUNCH_YN is set to Y. An error condition that prevents successful 
execution is written into the SAS log and SPI_SJM_LAUNCH_YN is set to N. The 
macro variable is provided as a convenience, and can be used to add conditional logic dependent on a job being successfully launched.

.. note:: 

    A successfully launched job does not mean the SAS code completed or executed without error. The job is operating on a different thread disconnected from the client
    application that launched the session. The email notification arrives to the recipients listed in -u on completion with the status of the SAS programs defined in 
    the job.

Example Macro Call with Optional Conditional Logic
------------------------------------------------------------
.. code:: 

    %mcr_spi_launch_sjm_job(in_job=test); 

    %if %symexist(spi_sjm_launch_yn) %then %do;
        %if &spi_sjm_launch_yn=Y %then %do;

            /* operations dependent on successful submission */

        %end;
    %end;

    
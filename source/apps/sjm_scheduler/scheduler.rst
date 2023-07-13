.. include:: nav.rst

SAS Job Manager Task Scheduler
====================================
The SJM Task Scheduler allows users to set up weekly recurring jobs for execution at a specific time. The SAS job is defined in an SJM batch file with some slight modifications 
to support automation. The task is configured for automation in the scheduler UI. The Windows Task Scheduler on hosted on an SPI application server calls the SJM job launcher 
hourly to identify and tasks scheduled for executions. If any tasks are found for that day/time, the launcher calls a service which triggers SJM to run the job. The actual SAS 
programs defined in a job execute as specified in the SJM batch file.

Table of Contents
--------------------

.. toctree:: 
   :maxdepth: 3

   batch  
   ui
   blinded


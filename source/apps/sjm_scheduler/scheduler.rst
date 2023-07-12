.. include:: nav.rst

SAS Job Manager Task Scheduler
====================================
The SJM Task Scheduler allows users to set up weekly recurring jobs for execution at a specific time. The SAS job is defined in an SJM batch file with some slight modifications 
to support automation. The task is configured for automation in the scheduler UI. The Windows Task Scheduler on host checks hourly for tasks set to execute and triggers each
job to execute sequentially. The actual SAS programs defined in a job execute as specified in the batch file (e.g. in parallel, sequentially, or combination of the two).

.. warning::

   Automation for special security folders is currently disabled. If you know your protocol requires special security and have not already mentioned this to SPI, follow the 
   instructions for `special security automation requests <blinded.html>`__ as soon as possible. 

Table of Contents
--------------------

.. toctree:: 
   :maxdepth: 3

   batch  
   ui
   blinded

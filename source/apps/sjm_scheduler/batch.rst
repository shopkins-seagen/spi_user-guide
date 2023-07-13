.. include:: nav.rst

SJM Batch File for Automation
====================================
The first step in creating a scheduled task is to create or update an SJM batch file to support automation, do not use batch files that call runsas.exe . This requires the 
addition of a few command line flags to the call to your SJM batch file.

#. Set the -i flag to false to turn off the interactive log checker. This still creates the log summary, it just prevents the app for opening and displaying the file to the user. This 
   should be set on each call within the batch file.
#. Set -n true to turn on notifications,  and specify the recipents to notify that the job was executed using the -u flag. More than one user can be specified, 
   e.g. -u shopkins atella rnordfors. If there are multiple calls in the batch file, this can be limited to just the last call. Always explicitly define the recipients as the 
   job executes in the context of a service account.

Example
--------------

.. code:: 

    @echo off
    "I:\deploy\client_apps\runsas\cmd\SasJobManager.Cli.exe" ^
        -c "%cd%\auto.csv" ^
        -n true ^
        -u shopkins atella ^
        -i false ^
        -m False ^
        -s best ^
        -h "%cd%\auto.html" 


.. warning:: 

    The scheduler only works with SJM. Do not schedule batch files that reference runsas.exe.
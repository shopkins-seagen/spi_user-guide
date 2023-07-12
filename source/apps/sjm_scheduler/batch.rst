.. include:: nav.rst

SJM Batch File for Automation
====================================
The first step in created a scheduled task is to create or update an SJM batch file to support automation. This requires the addition of a few command line flags to the call.

#. Add the -i false flag to turn off the interactive log checker. This still creates the log summary, just prevents the app for opening and displaying the file to the user. This 
   should be set on each call within the batch file.
#. Add the -n true to turn on notifications,  and -u [users] to identify recipients the job was executed. Since this job is executed by a service account on a server, the turning on notifications is 
   the easiest way to get feedback on jobs status. More than one user can be specified, e.g. -u shopkins atella rnordfors. This can be set on only the last call in the batch file.

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
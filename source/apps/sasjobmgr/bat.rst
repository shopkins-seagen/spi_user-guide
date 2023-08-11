.. include:: nav.rst

Launch SJM from Batch File 
========================================
For recurring jobs or final runs, programmers should create .BAT files to manage the execution of the programs. See `create bat files from UI <ui-bat.html>`__ for 
details on how to create .bat file using the SAS Launcher UI.

A single .bat file can have mulitple calls, though each call creates a separate HTML summary. Starting in v2, user can use the mixed run 
mode to process files sequentially, and process groups programs without dependencies in parallel.

Example: Default Call 
----------------------------------------------------
This is the simplest example. The app submits the programs on the production server in parallel, records the macros used, reviews the log, and generate the summary file. There 
are three required parameters, specified below, the rest of the options assume the default value.

.. code:: 

  @echo off
  "I:\deploy\client_apps\runsas\cmd\SasJobManager.Cli.exe" ^
    -c "%cd%\test.csv" ^
    -s sgsasv1.sg.seagen.com ^
    -h "%cd%\test.html" 

Example: Run programs sequentially on Best server and Notify on Completion 
-------------------------------------------------------------------------------------
This example runs all the programs in CSV in sequence (-a False), waiting for each program to complete before submitting the next on the stage server. Upon completion,
the app sends an email notification (-n true) to the user that sumitted the job.  To send the notification to multiple users, or a different user, specify the users 
in a space-delimited list using the -u flag. 

.. code:: 

  @echo off
  "I:\deploy\client_apps\runsas\cmd\SasJobManager.Cli.exe" ^
    -c "%cd%\test.csv" ^
    -n true ^
    -a False ^
    -s best ^
    -h "%cd%\test.html" 

Example: Multiple Calls for Different Processing modes
--------------------------------------------------------------------------------------------
In this example, the first call to runsas runs SDTM programs sequentially (-a false). Once all the SDTM data are complete, 
the corresponding QC programs are run in parallel. 

.. code::

    @echo off

    :: Sequentially run pgms in stdm1.csv as they are dependencies for other programs
    "I:\deploy\client_apps\runsas\cmd\SasJobManager.Cli.exe" ^
      -c "%cd%\stdm1.csv" ^
      -s sgsasv1.sg.seagen.com ^
      -a False ^
      -h "%cd%\stdm1.html" 
      
    :: parallel run pgms in sdtm-qc.csv run the qc programs once the sdtm are completed
    "I:\deploy\client_apps\runsas\cmd\SasJobManager.Cli.exe" ^
      -c "%cd%\stdm-qc.csv" ^
      -s sgsasv1.sg.seagen.com ^
      -h "%cd%\stdm-qc.html" 

Example: Mixed Run Mode, display Programmer and Tester in the HTML Summary, and quit if a program has an error (v2+)
------------------------------------------------------------------------------------------------------------------------------------
This example, the CSV file contains an optional 3rd position to indentify the sequence of the programs and the run mode. 
-f captures the AI to get the programmer and tester, and -d true indicates that the app uses the 3rd position of the CSV to define sequence and run mode. 
-q True indicates that app will stop execution if any program has an ERROR in the log. 

.. code::
    @echo off

    :: Sequentially run pgms in stdm1.csv as they are dependencies for other programs
    "I:\deploy\client_apps\runsas\cmd\SasJobManager.Cli.exe" ^
      -c "%cd%\submit.csv" ^
      -s sgsasv1.sg.seagen.com ^
      -f "O:\product\protocol\analysis\production\ai\ai.xlsx" ^
      -t true ^
      -d true ^
      -q true ^
      -h "%cd%\submit.html" 

Contents of CSV
++++++++++++++++++++++++++
The 3rd position determines the order of execution. Programs with the same sequence will execute in parallel. The QC programs follow the corresponding primary
program category (default behavior of UI 'include QC program' when using the AI). 

.. code-block:: text

  O:\stat_prog_infra\testing\sjm\dotnet\use_ai\data\raw\pgms\copy1.sas,1,2
  O:\stat_prog_infra\testing\sjm\dotnet\use_ai\data\sdtm\pgms\dm.sas,1,1001
  O:\stat_prog_infra\testing\sjm\dotnet\use_ai\data\sdtm\pgms\ae.sas,1,1002
  O:\stat_prog_infra\testing\sjm\dotnet\use_ai\data\sdtm\pgms\cm.sas,1,1002
  O:\stat_prog_infra\testing\sjm\dotnet\use_ai\data\sdtm\testing\v-dm.sas,2,2001
  O:\stat_prog_infra\testing\sjm\dotnet\use_ai\data\sdtm\testing\v-ae.sas,2,2001
  O:\stat_prog_infra\testing\sjm\dotnet\use_ai\data\sdtm\testing\v-cm.sas,2,2001
  O:\stat_prog_infra\testing\sjm\dotnet\use_ai\data\adam\pgms\adsl.sas,1,3001
  O:\stat_prog_infra\testing\sjm\dotnet\use_ai\data\adam\pgms\adae.sas,1,3002
  O:\stat_prog_infra\testing\sjm\dotnet\use_ai\data\adam\testing\v-adsl.sas,2,4001
  O:\stat_prog_infra\testing\sjm\dotnet\use_ai\data\adam\testing\v-adae.sas,2,4001
  O:\stat_prog_infra\testing\sjm\dotnet\use_ai\outputs\tlfs\pgms\t-ae.sas,1,100000
  O:\stat_prog_infra\testing\sjm\dotnet\use_ai\outputs\tlfs\pgms\t-mh.sas,1,100000
  O:\stat_prog_infra\testing\sjm\dotnet\use_ai\outputs\tlfs\testing\v-t-ae.sas,2,101001
  O:\stat_prog_infra\testing\sjm\dotnet\use_ai\outputs\tlfs\testing\v-t-mh.sas,2,101001
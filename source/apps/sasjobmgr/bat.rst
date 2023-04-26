.. include:: nav.rst

.BAT File Examples
================================
For recurring jobs or final runs, programmers should create .BAT files to manage the execution of the programs. A single .bat file can have many calls to SJM, each with a different 
set of options on a different .CSV file. For example, first call to SJM in a .bat file for SDTM automation might execute the DM, TA, TI, TE, TV, SE, and SV domain programs sequentially, a
second call runs the renmaining SDTM programs in parallel, when that completes, a final call runs all the QC programs in parallel. Users have access to all the options from the 
command line in the .BAT file. The app creates a summary file created for each call to the SJM (if checkLog is True); it does not aggregate the summaries by .BAT file.

Default Call 
----------------------------------------------------
This is the simplest example. The app submits the programs on the best server in parallel, records the macros used, reviews the log, and generate the summary file. There 
are three required parameters, specified below, the rest of the options assume the default value.

#. CSV file (-c) -  The path and name of the .CSV file that lists the programs to be executed. Optionally this can be replaced with -p followed by a space-delimited list of programs.
#. Server (-s) - The name of the server

    * sgsasv1.sg.seagen.com - production server
    * sgsasv1-stg.sg.seagen.com - stage server
    * best - let the app pick the server with the most availability

#. HTML summary (-h) - The path and name of the HTML summary file

.. code:: 

  @echo off
  "I:\deploy\client_apps\runsas\cmd\SasJobManager.Cli.exe" ^
    -c "%cd%\test.csv" ^
    -s best ^
    -h "%cd%\test.html" 

Run programs in Sequence and Notify on Completion on a Specific Server
--------------------------------------------------------------------------
This example runs all the programs in CSV in sequence (-a False), waiting for each program to complete before submitting the next on the stage server. Upon completion,
the app sends an email notification (-n true) to the user that sumitted the job.  To send the notification to multiple users, or a different user, specify the users 
in a space-delimited list using the -u flag. 

.. code:: 

  @echo off
  "I:\deploy\client_apps\runsas\cmd\SasJobManager.Cli.exe" ^
    -c "%cd%\test.csv" ^
    -n true ^
    -a False ^
    -s sgsasv1-stg.sg.seagen.com ^
    -h "%cd%\test.html" 

Create a workflow for an entire analysis
--------------------------------------------------------------------------------------------
In this example, the first call to runsas runs the programs sequentially. Once that completes, the next group of programs is run in parallel. When that completes,
the last group of programs is also run in parallel. This could be used to run SDTM dataset that are referenced by other domains, so they must exist prior to other programs executing. 
The next set of SDTM programs do not create dependencies referenced by other domains and can be run in no specific sequence. Once all the SDTM data are complete, run the QC programs. 

This pattern can be extended to run an entire workflow of an analysis from raw -> TLFs, using a single .bat file with seqential and async calls as needed to both 
support any dependencies and greatly reduce total run time.

.. code::

    @echo off

    :: Sequentially run pgms in stdm1.csv as they are dependencies for other programs
    "I:\deploy\client_apps\runsas\cmd\SasJobManager.Cli.exe" ^
      -c "%cd%\stdm1.csv" ^
      -s best ^
      -a False ^
      -h "%cd%\stdm1.html" 
      
    :: parallel run pgms in sdtm2.csv - no dependencies
    "I:\deploy\client_apps\runsas\cmd\SasJobManager.Cli.exe" ^
      -c "%cd%\stdm2.csv" ^
      -s best ^
      -h "%cd%\stdm2.html" 

    :: parallel run pgms in sdtm-qc.csv run the qc programs once the sdtm are completed
    "I:\deploy\client_apps\runsas\cmd\SasJobManager.Cli.exe" ^
      -c "%cd%\stdm-qc.csv" ^
      -s best ^
      -h "%cd%\stdm-qc.html" 
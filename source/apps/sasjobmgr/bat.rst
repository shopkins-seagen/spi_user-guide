.. include:: nav.rst

.BAT File Examples
================================
The location of the executable in the examples below is for evaluation only. This version is compiled as framework-independent to enable users without the necessary 
.NET runtimes installed locally to execute code. The drawback is the applications take about 2x as long to start. This path will updated when the client environments 
have the runtimes.

Default Call 
----------------------------------------------------
This example demonstrates the only required parameter, either CSV file (-c) or List of programs (-p). All the other options are set to the defaults 
defined by SPI. RunSAS selects the best server, submits all the programs in the CSV file, records the macros in the db, and reviews and summarizes the log files.

.. code:: 

    @echo off
    "I:\deploy\client_apps\runsas\cmd-standalone\SasJobManager.Cli.exe" ^
        -c "%cd%"\submit.csv ^

Run programs in Sequence and Notify on Completion on a Specific Server
--------------------------------------------------------------------------
This example runs all the programs in CSV in sequence, waiting for each program to complete before submitting the next on the stage server. Upon completion,
the app sends an email notification, -n True, to the users specified in -u.  

.. code:: 

    @echo off
    "I:\deploy\client_apps\runsas\cmd-standalone\SasJobManager.Cli.exe" ^
        -c "%cd%"\submit.csv ^
        -b false ^
        -s sgsasv1-stg.sg.seagen.com ^
        -a false ^
        -n true ^
        -u shopkins atella

Create a workflow for an entire analysis
--------------------------------------------------------------------------------------------
In this example, the first call to runsas runs the programs sequentially. Once that completes, the next group of programs is run in parallel. When that completes,
the last group of programs is also run in parallel. 

This pattern would support generating dependencies sequentially (e.g. copying, processing raw data) then performing
data transformations like SDTM, then running the QC programs for the SDTM datasets. This pattern can be extended to include the entire workflow from raw -> TLFs.

.. note::

  A separate run summary is generated for each call. 

.. code::

    @echo off

    :: Sequentially run pgms in seq.csv
    "I:\deploy\client_apps\runsas\cmd-standalone\SasJobManager.Cli.exe" ^
      -c "%cd%"\raw-data.csv ^
      -s sgsasv1-stg.sg.seagen.com ^
      -a False ^
      -b False 
      
    :: parallel run pgms in asy1.csv
    "I:\deploy\client_apps\runsas\cmd-standalone\SasJobManager.Cli.exe" ^
      -c "%cd%"\sdtm.csv ^
      -s sgsasv1-stg.sg.seagen.com ^
      -a True ^
      -b False

    :: parallel run pgms in asy1.csv
    "I:\deploy\client_apps\runsas\cmd-standalone\SasJobManager.Cli.exe" ^
      -c "%cd%"\sdtm-qc.csv ^
      -s sgsasv1-stg.sg.seagen.com ^
      -a True ^
      -b False 
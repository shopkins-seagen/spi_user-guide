.. include:: nav.rst

Automated QC Review
===============================
SJM supports the display of the QC results from automated QC in the HTML summary. The QC program **MUST** use mcrbincomp or equivalent logic to perform comparisons. The macro creates 
specific messages in the SAS log file SJM uses to generate the QC summary. 


Implement mcrbincomp in the Comparison of QC and Production data
--------------------------------------------------------------------
The v-[program].sas test program uses mcrbincomp to perform one or more comparisons of data sets. The macro records targets in the SAS log that SJM detects. Each call to 
mcrbincomp is considered a single 'test'. SJM summarizes the number of passing/total tests at the program level, and the number of passing programs/total programs at the 
job level. Log issues (errors, warnings,..), are not considered in whether a test passes or fails in SJM, as it does in RunSAS. 

Indicate the Program is a QC Program
------------------------------------------
If a validation program uses mcrbincomp, you must indicate so through one of the interfaces, as not all QC programs implement mcrbincomp. There are two ways to do so:

#. In the CSV file, the second position indicates the type of program, 1=production, 2=QC

    Ex: O:\\stat_prog_infra\\testing\\runsas\\dotnet\\unit_test\\data\\adam\\testing\\v-test.sas,2

#. In the SAS Launcher UI, check the IsQC box to the right of the program name

    .. image:: isqc.png


QC Report in HTML summary
-----------------------------------
If there is at least 1 QC program included in a run, the application generates the QC summary. The Automated QC Results box at the top of the file provide 
counts of the total number of tests passed // total number of tests. Total tests can exceed the number of programs as a single program may have multiple calls 
to the compare macro, each of which if 1 test. 

Below that, the tal number of programs that passes and failed are summarized and displayed in filter buttons. Click the Failed button and the summary will filter 
just the programs that have failing tests. 

In the Log Summary table, the number of passes/tests by program is listed in the Auto QC columns. The drop down menu in the Auto QC column header 
of the Summary of SAS Logs table can also be used to subset rows by QC status.


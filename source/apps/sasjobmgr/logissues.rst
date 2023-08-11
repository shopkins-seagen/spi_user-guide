.. include:: nav.rst

SAS Log Reviewer 
===============================================
RunSAS optionally can review the log object of a SAS program file after execution, or review SAS log files on the Biometrics file share. In either case, the app 
identifies occurences of the regular expressions in the table below in each log and generates are summary HTML file. The summary file is created in a run_summaries 
subfolder. After reviewing a summary, the file can be closed from browser using the X to retain the file, or click the |close| button to close and delete the file. 

List of Log Issues Detected
------------------------------
.. list-table::
    :widths: 10 90
    :header-rows: 1

    * - Detects
      - Regex Pattern
    * - Errors
      - ^ERROR(:|.*:)
    * - Warnings
      - ^WARNING(:|.*:)(?!.*Unable to copy)(?!.*scheduled to expire)
    * - Notice
      - NOTICE:
    * - Notes
      -       
        * UNINITIALIZED
        * REPEATS OF BY VALUES
        * W.D FORMAT
        * ASSUMING THE SYMBOL
        * VALUES HAVE BEEN CONVERTED TO
        * MISSING VALUES WERE GENERATED AS A RESULT
        * DIVISION BY ZERO DETECTED
        * OUTSIDE THE AXIS RANGE
        * INVALID ARGUMENT TO FUNCTION
        * MATHEMATICAL OPERATIONS COULD NOT BE PERFORMED
        * INVALID DATA
        * MEANING OF AN IDENTIFIER
    * - QC Pass flag       
      - QC_PASS!
    * - Qc Fail flag
      - QC_FAIL!
  
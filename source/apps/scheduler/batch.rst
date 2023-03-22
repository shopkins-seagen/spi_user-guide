Control Automation Manager using .BAT files
=======================================================

.. include:: nav.rst

.BAT files on the file share can be used to invoke *FAST* without the need to open the UI. These would need to be invoked by the user, as they are not the same as
the scheduled tasks created on the server. Care must be paid to the fomatting as spaces do matter. 


**Parameters**
---------------------------

.. list-table::
  :widths: 10 15 35 40
  :header-rows: 1

  * - Position
    - Parameter
    - Description
    - Example
  * - 1
    - **Executable**
    - Path to the executable file. The .exe location will vary by functional group. This allows each group to manage independent configuration files for the application.
    - "I:\deploy\auto_gsdb\RunSAS.exe"
  * - 2
    - **SAS files**
    - This argument identifies the SAS programs to submit by identifying a specific driver.CSV file, or with the key word defined in the {auto_flag} in the configuration file.
    - Valid values
    
        * "[analysis path]\utilities\admin\driver.csv" 
        * {auto_flag} by default this value is defined as "Auto". This will cause the application to identify all the reports scheduled for the [run date] and 
          parse the corresponding driver.csv files to identify all the SAS program files.

  * - 3
    - **Run date**
    - This argument identifies the date to evaluate which reports are scheduled when *SAS files* = {auto_flag}
    - Valid values
    
        * A date in SAS DATE9 format e.g. 20Apr2017
        * {current_date} by default this value is defined as "Current". This will cause the application to identify all the reports scheduled for the current date and 
          parse the corresponding driver.csv files to identify all the SAS program files.          

  * - 4
    - **Display mode**
    - This argument specifies the behavior of the HTML run summary log saved to the file share 
    - Valid values
    
        * Display - the HTML summary file is displayed in the user's browser
        * Quiet - the HTML summary file is not displayed

  * - 5
    - **Summary log**
    - This argument specifies the location to save the HTML run summary log. Use the same value as define in {summary_subfolder} (default is "auto_log")
    - [analysis path]\utilities\admin\auto_logs

  * - 6
    - **QC Level**
    - This argument specifies the behavior SAS program execution within a report when an ERROR or WARNING condition is encountered in a SAS log file
    - Valid values
    
        * QC_OFF - execute all SAS programs files listed in the driver file for the report
        * QC_Normal - terminate SAS program execution if an ERROR condition is detected in a SAS log file
        * QC_Strict - terminate SAS program execution if an ERROR or WARNING condition is detected in a SAS log file

  * - 7
    - **Run mode**
    - This argument specifies the behavior of the application 
    - Valid values

        * Standard - run the SAS programs 
        * AutoRun - run the SAS programs, perform the file transfers, and log the run in the database
        * Auto - run the SAS programs, peform the file transfers, perform the email distribution, and log the run in the database
        * AutoDistribute - execute the distribution and send email notification to {admin}

        .. note::

            Do not use the AutoDistribute mode from a .BAT file. Use the interactive mode to peform this function. 

  * - 8 - *n*
    - **Global variables**
    - One or more key:value pairs  in the form [macro variable name]|[value] that will become global macro variables in the all the SAS program environments. 
    - ExtractDate:10Jun2017

**Examples**
-----------------------

**.BAT file to run SAS programs, transfer, and distribute reports scheduled for the current date**
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

    .. raw:: html    
        
        <div style="background-color:#ffffe6;width:100%;border-radius: 25px;padding: 20px; ">
        <i style="font-style: normal;font-size: smaller;color: #268bd2;">@echo off</i><br/><br/ >
        <i style="font-style: normal;font-size: smaller;color: #268bd2;">"I:\deploy\auto_gsdb\RunSAS.exe" ^</i><br/ >
        <i style="font-style: normal;font-size: smaller;color: #268bd2;">&nbsp;"Auto" ^</i><br/ >
        <i style="font-style: normal;font-size: smaller;color: #268bd2;">&nbsp;"Current"  ^</i><br/ >
        <i style="font-style: normal;font-size: smaller;color: #268bd2;">&nbsp;"Quiet" ^</i><br/ >
        <i style="font-style: normal;font-size: smaller;color: #268bd2;">&nbsp;"S:\Projects\GSDB\utilities\admin\auto_logs"</i><br/ >
        <i style="font-style: normal;font-size: smaller;color: #268bd2;">&nbsp;"QC_Normal" </i><br/ >
        <i style="font-style: normal;font-size: smaller;color: #268bd2;">&nbsp;"Auto"</i><br/ >
        </div>

**.BAT file to just run the SAS programs for a report**
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

    .. raw:: html    
        
        <div style="background-color:#ffffe6;width:100%;border-radius: 25px;padding: 20px; ">
        <i style="font-style: normal;font-size: smaller;color: #268bd2;">@echo off</i><br/><br/ >
        <i style="font-style: normal;font-size: smaller;color: #268bd2;">"I:\deploy\auto_gsdb\RunSAS.exe" ^</i><br/ >
        <i style="font-style: normal;font-size: smaller;color: #268bd2;">&nbsp;"S:\Projects\GSDB\Periodic\stdrpt_sgn35-022_susar_fda\v01\utilities\admin\driver.csv" ^</i><br/ >
        <i style="font-style: normal;font-size: smaller;color: #268bd2;">&nbsp;"Current"  ^</i><br/ >
        <i style="font-style: normal;font-size: smaller;color: #268bd2;">&nbsp;"Display" ^</i><br/ >
        <i style="font-style: normal;font-size: smaller;color: #268bd2;">&nbsp;"S:\Projects\GSDB\Periodic\stdrpt_sgn35-022_susar_fda\v01\utilities\admin\utilities\admin\auto_logs"</i><br/ >
        <i style="font-style: normal;font-size: smaller;color: #268bd2;">&nbsp;"QC_Off" </i><br/ >
        <i style="font-style: normal;font-size: smaller;color: #268bd2;">&nbsp;"Standard"</i><br/ >
        <i style="font-style: normal;font-size: small;color:#073642;font-weight:bold;text-alignment:center;">Driver.csv file format</i><br />
        <i style="font-style: normal;font-size: smaller;color: #268bd2;">S:\Projects\GSDB\Periodic\stdrpt_sgn35-022_susar_fda\v01\data\raw\pgms\makedata.sas,1</i><br/ >
        <i style="font-style: normal;font-size: smaller;color: #268bd2;">S:\Projects\GSDB\Periodic\stdrpt_sgn35-022_susar_fda\v01\data\raw\testing\v-makedata.sas,2</i><br/ >
        </div>



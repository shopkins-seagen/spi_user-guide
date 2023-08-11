.. include:: nav.rst

Launch SJM from Context Menu 
============================================
Users can install context menus into their registry by downloading and installing the SJM menus from the library described 
in `initial setup <initial.html>`__

Once context menus are installed, users can right-click on one or more SAS programs or log files and submit program and review SAS logs in 5 different ways. 

#. Run on best server
#. Run on prod server
#. Run on stage server
#. Review SAS logs
#. Review SAS logs and summarize automated QC findings

All SJM menu items are prefixed with **SJM** to distinguish from RunSAS menu items. The table below details the new right-click context menu items 
that are available in SJM. If there is need for additional context menu selections, contact SPI to provide support.

Context Menu Item Configurations
----------------------------------------------------------

.. list-table::    
    :widths: 30 40 30
    :header-rows: 1

    * - Menu
      - Description
      - Default options
    * - SJM: Submit on Best Server
      - The application determines which server has more availability using a weighted comparison between prod and stage. For Parallel mode, the app recalculates the best 
        server between each batch. In sequential mode, the app calculates the best server before submitting each program. There is a small performance cost to use best, so if a 
        server has a low utilization and the job is small, explicitly selecting a server may be faster.
      - * Check log
        * Record macros
        * Parallel mode
        * SASApp94 server context
        * Write HTML summary under [current location]\\run_summaries folder
    * - SJM: Submit on Prod Server
      - Submits the programs on the production server. Does not evaluate CPU utilized.
      - * Check log
        * Record macros
        * Parallel mode
        * SASApp94 server context
        * Write HTML summary under [current location]\\run_summaries folder    
    * - SJM: Submit on Stage Server
      - Submits the programs on the stage server. Does not evaluate CPU utilized.
      - * Check log
        * Record macros
        * Parallel mode
        * SASApp94 server context
        * Write HTML summary under [current location]\\run_summaries folder      
    * - SJM: Open SAS Launcher UI
      - Open the SAS Launcher UI from the direcotry in which the user launched the application, optionally with one or more selected SAS programs
      - User has access to modify all the options
    * - SJM: Review Logs
      - The application reviews all the selected SAS log files and generates the HTML summary file in the [current location]\\run_summaries folder  
      - Review logs only
    * - SJM: Review Logs and Summarize QC
      - The application reviews all the selected SAS log files, summarizes the automated QC results and displays the results in the HTML summary file in the [current location]\\run_summaries folder.  
      - Review logs and summarize automated QC   



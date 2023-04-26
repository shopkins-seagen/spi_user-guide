.. include:: nav.rst

Launching SAS Job Manager
============================
RunSAS can be invoked directly by the user from either a a command line interface(CLI) via a.bat file or the a context menu, or by through SAS launcher grahic user
interface(GUI) application. Before attempting to use the app, install the context menu for SAS Job Manager Package in the `context menu library <http://sgcpapp1/cp/programming/registry/library.html>`__

The application has a dependency on the Windows .NET 6 x64 Desktop Runtime. If you are unable to launch the app because you do not have this 
installed contact [spi for now].

Context Menus 
-----------------------------------
Once context menus are installed `[see initial setup] <sasjobmgr.html#initial-setup>`__, users can right-click on one or more SAS programs or log files and submit in four different ways. Note that all SJM menu items are 
prefixed with **SJM** to distinguish from RunSAS menu items. The table below details the new right-click context menu items that are available in SJM. If there is need for
additional context menu selections, contact SPI to provide support.

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

Windows .BAT File CLI
+++++++++++++++++++++++++++++++++++
Using a .bat file to call the SJM application allows the user to have complete control over all the options without needing to invoke the UI. The parser for
command line interface accepts arguments prefixed with a flag `[see flags table <flags.html>`__. .BAT files, and the corresponding CSV file can be generated from the SAS Launcher. The app uses the 
selections in the GUI to create an identical .BAT file and a CSV file of the same name containing the selected programs. 

`[.BAT file examles] <bat.html>`__
`[Command line flags] <flags.html>`__

SAS Launcher GUI
--------------------------------------------------
The SAS launcher is invoked by optionally selecting one or more SAS files or from a directory background that contains SAS files, 
and selecting **SJM: Open SAS Launcher UI** from the right-click context menu. The UI provides access to all the SJM options without having to create a .BAT file. The 
figure below details all the controls in the interface. 

.. raw:: html 

    <embed>
        <style>
            li a:link{
            font-weight:bold;
            margin: 0px 5px 0px;
            }
        </style>

        <div class="container">
            <div class="row">
                <div class="col-6">
                    <h5>SAS Launcher UI Controls</h5>
                    <img src="ui3.png" alt="GUI" height="442" width="501">
                </div>
                <div class="col-6">
                   <h5>Desriptions of the UI Controls for SAS Launcher</h5>
                    <ol style="font-size: 12px;">
                        <li>Submits the selected SAS program files</li>
                        <li>Updates the %CPU utilized labels in UI elment #7</li>
                        <li>Opens a console window that persists the notification messages displayed during execution.</li>
                        <li>Open the main page of the SJM user guide.</li>
                        <li>Sets the location of the SAS program files. The UI only supports a programs from a single folder. Use the .BAT file to run programs in different folders.</li>
                        <li>Sets the SAS app server to execute the program.<a href="function.html#select-server-and-server-context">[See More]</a></li>
                        <li>Displays the current amount of CPU the production and Stage servers are using. The radio buttons available as a convenience and have the same functionality as the drop down menu</li>
                        <li>Sets the server context to use on the selected application server.<a href="function.html#select-server-and-server-context">[See More]</a></li>
                        <li>Sets run mode for the selected programs<a href="function.html#select-run-mode">[See More]</a></li>
                        <li>Check the box to review the SAS logs and generate the log summary HTML file<a href="function.html#review-logs">[See More]</a></li>
                        <li>Check the box to record the external SAS macros compiled during program execution<a href="function.html#record-macros">[See More]</a></li>
                        <li>Check the box to create stand-alone SAS program files without external macro dependencies for each program included in the run<a href="function.html#resolve-sas-code">[See More]</a></li>
                        <li>Check the box to recieve an email notification when the jobs completes</li>
                        <li>Check the box and provide a name for the .bat and .csv file to generate the files based on current selections. Use the <img src="bat-button.png"> button to generate the files without running the programs</li>
                        <li>Type into the text box to dynamically filter the SAS programs displayed in the list box. Remove the text to clear the filter</li>
                        <li>Toggles check/uncheck all programs for inclusion</>
                        <li>Toggles A-Z, Z-A sorting of the programs</li>
                        <li>Toggle check/uncheck all Is QC program attribute</li>
                        <li>Check box to include a program in run</>
                        <li>Check box to indicate the program implements logic to support automated QC results reporting [See details on automating QC]</li>
                        <li>In sequential run mode, drag and drop programs in the position in the list that corresponds to the sequence they are executed</li>
                        <li>Updates the list of SAS programs from the file server, in case a program was added or deleted while the app was open</li>
                    </ol>
                </div>                
            </div>
        </div>


    </embed>


.. include:: nav.rst

Run programs
=========================
The UI can be used to run programs with access to more of the options available in SJM that are not accessible in CLI mode. 

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
                    <img src="ui-main.png" alt="GUI" height="442" width="501">
                </div>
                <div class="col-6">
                   <h5>Desriptions of the UI Controls for SAS Launcher</h5>
                    <ol style="font-size: 12px;">
                        <li>Submits the selected SAS program files</li>
                        <li>Updates the %CPU utilized labels in UI elment #7</li>
                        <li>Opens a console window that collects the notification messages displayed during execution.</li>
                        <li>Open the main page of the SJM user guide.</li>
                        <li>Sets the location of the SAS program files. The UI only supports programs from a single folder. Use the .BAT file to run programs in different folders in the same call</li>
                        <li>Sets the SAS app server to execute the program.</li>
                        <li>Displays the current amount of CPU the production and Stage servers are using. The radio buttons available as a convenience and have the same functionality as the drop down menu</li>
                        <li>Sets the server context to use on the selected application server.</li>
                        <li>Sets run mode for the selected programs</li>
                        <li>Check the box to review the SAS logs and generate the log summary HTML file</li>
                        <li>Check the box to record the external SAS macros compiled during program execution</li>
                        <li>Check the box to create stand-alone SAS program files without external macro dependencies for each program included in the run</li>
                        <li>Check the box to recieve an email notification when the jobs completes</li>
                        <li>Check the box to terminate execution if a SAS program encounters an ERROR. This is only applicable in sequential or mixed(.bat only) modes</li>
                        <li>Checking the Create batch and csv files button exposes additional options available for batch files</li>
                        <li>Type into the text box to dynamically filter the SAS programs displayed in the list box. Remove the text to clear the filter</li>
                        <li>Toggles check/uncheck all programs for inclusion</>
                        <li>Toggles A-Z, Z-A sorting of the programs</li>
                        <li>Toggle check/uncheck all Is QC program attribute</li>
                        <li>Check box to include a program in run. In sequential run mode, drag and drop programs in the position in the list that corresponds to the sequence they are executed</li>
                        <li>Check box to indicate the program implements logic to support automated QC results reporting [See details on automating QC]</li>
                        <li>Updates the list of SAS programs from the file server, in case a program was added or deleted while the app was open</li>
                    </ol>
                </div>                
            </div>
        </div>
    </embed>    
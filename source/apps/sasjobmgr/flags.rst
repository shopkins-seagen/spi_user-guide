.. include:: nav.rst

Command Line Flags 
=======================================
The table below lists the flags available and the possible values. Default values are indicated in bold font. If a flag has a default, it is optional and does not have 
to be specified. Hover over the value in Option column to link to additional details if available. 

.. raw:: html 

    <embed>
        <style>
            .datagrid table { border-collapse: collapse; text-align: left;  } 
            .datagrid {font: normal 12px/150% Arial, Helvetica, sans-serif; background: #fff; overflow: hidden; -webkit-border-radius: 3px; -moz-border-radius: 3px; border-radius: 3px; }
            .datagrid table td, .datagrid table th { text-align: left;}
            .datagrid table thead th {background:-webkit-gradient( linear, left top, left bottom, color-stop(0.05, #006699), color-stop(1, #00557F) );background:-moz-linear-gradient( center top, #006699 5%, #00557F 100% );filter:progid:DXImageTransform.Microsoft.gradient(startColorstr='#006699', endColorstr='#00557F');background-color:#006699; color:#FFFFFF; font-size: 15px; font-weight: bold; border-left: 1px solid #0070A8; } 
            .datagrid table thead th:first-child { border: none; }.datagrid table tbody td { color: #00496B; border-left: 1px solid #E1EEF4;font-size: 12px;font-weight: normal; }
            .datagrid table tbody .alt td { background: #E1EEF4; color: #00496B; }.datagrid table tbody td:first-child { border-left: none; }
            .datagrid table tbody tr:last-child td { border-bottom: none; }
            .dft {font-weight:bold;}
            .flag {color:blue;font-style:italic;}
            .entry{background: aliceblue;corner-radius:5px;}
        </style>
            <div><table>
            <thead><tr><th>CLI Flag</th><th>Option</th><th>Description</th><th>Values</th></tr></thead>
            <tbody>
                <tr>
                    <td>-a</td>
                    <td><span>Async run mode</span></td>
                    <td>
                        Run mode refers to the manner in which the app groups and order programs for execution. There are 3 modes, each described below.
                        <h5>Parallel (-a true)</h5>
                        
                        <div class="entry">
                            Programs are submitted in aggregate without any order enforced. The app throttles the maximum number of programs based on the available CPU and
                            some constants specified by SPI. In Parallel mode, the app queries the amount of CPU available and calculates the 
                            maximum number of programs that can be submitted in parallel. The programs execute asynchronously while the app waits for all the programs in 
                            the batch to complete. Once a batch completes, the app optionally determines the best server(if best is specified for server), queries 
                            available CPU, recalculates batch size, and submits that number of programs in parallel. This cycle continues until all programs have been 
                            executed.<br />
                            <span class="badge badge-danger text-wrap">Because order cannot be enforced, it is critical that programs with overlapping dependencies not be submitted in parallel or a 
                            concurreny issue may result in a resource being locked</span>
                        </div>
                        <h5>Sequential (-a false)</h5>
                        <div class="entry">
                            Programs are submitted submitted in the sequence defined by the position in the grid in the UI(top to bottom) or by the integer value in the 
                            3rd position in the CSV file(optional). Each program is submitted in order and completes prior to submitting the next program. This mode is 
                            intended for programs that create dependencies for other programs (e.g. DM, ADSL) 
                        </div>
                        <h5>Mixed (-a true -d true)</h5>
                        <div class="entry">
                           Starting in v2, SJM accepts CSV files with an optional integer value in 3rd position that identifies sequence. Programs will be submitted in the 
                           order of the sequence, and programs with the same sequence are submitted in parallel. The UI provides functionality to create the CSV from AI 
                           using Derive_order to calculate the sequence.  
                           <span class="badge badge-primrary text-wrap">-a must not be set to false or the app will default to sequential mode</span>                       
                        </div>
                    </td>
                    <td>
                        <ul>
                            <li class="dft">true (parallel or mixed)</li>
                            <li>false (sequential)</li>
                        </ul>
                    </td>
                </tr>
                <tr>
                    <td>-c</td><td>.csv file</td>
                    <td>.CSV file (path\name) that lists programs for execution. Starting in v2, SJM accepts an optional 3rd position for sequence that enables mixed mode. 
                    <table class="table table-bordered table-dark">
                    <tr><td>Position 1</td><td>Path\program</td><tr>
                    <tr><td>Position 2</td><td>1 or 2, 1=Production, 2=QC</td></tr>
                    <tr><td>Position 3</td><td>Sequence</td></tr>
                    </table>                    
                    </td><td>Required if -p is not specified</td>
                </tr>
                
                <tr>
                    <td>-d</td><td>Use sequence in CSV file for order/run mode</td><td>If True, the app uses the optional sequence field in the CSV file to enabled mixed mode post-processing. 
                     -a must not be false</td>
                    <td><ul><li class="dft">False</><li>True</li></ul></td>
                </tr>
                <tr>
                    <td>-e</td><td>Export log summary to Excel</td><td>Exports the SAS log findings to an Excel file in the same location as the HTML summary</td>
                    <td><ul><li class="dft">False</><li>True</li></ul></td>
                </tr>
                <tr>
                    <td>-f</td><td>AI</td><td>Path of the AI file. Used at execution time to add Developer and Tester to the HTML summary when -t is True</td>
                    <td>Required if -t is true, otherwise optional</td>
                </tr>
                <tr>
                    <td>-h</td><td>HTML log summary</td><td>Path\name of the HTML summary file</td><td>required</td>
                </tr>
                <tr>
                    <td>-i</td>
                    <td>Open summary and display console messages interactively</td>
                    <td>Opens the HTML summary is the associated browser. User may have associate a browser with an HTML file
                    to get the behavior to work the first time. Should be set to false for .BAT files used in the SJM scheduler</td>
                    <td><ul><li class="dft">true</><li>false</li></ul></td>
                </tr>
                <tr>
                    <td>-l</td><td>Review logs</td>
                    <td>Specify if the app scans the logs for occurences of <a href="">log issues</a> 
                    and generates an HTML file summarizing the findings for all the logs. If run interactively,
                    the summary is written to the 'run_summaries' subfolder. The user can direct the location of the summary file in the .bat file 
                    using the -h flag.</td>
                    <td><ul><li class="dft">true</><li>false</li></ul></td>
                </tr>
                <tr>
                    <td>-m</td>
                    <td>Record macros</td>
                    <td>Specify if the app identifies all the department-level macros compiled in the SAS environment during program execution. 
                    AIM uses these records to determine re-test status if a dependent macro was modified after the output was validated.</td>
                    <td><ul><li class="dft">true</><li>false</li></ul></td>
                </tr>
                <tr>
                    <td>-n</td>
                    <td>Notify</td>
                    <td>Specify if the app generates an email notification with a brief summary of log findings for each program in a job. If the app is 
                    run interactively, the notification is sent to the current user. In the .bat file, a list of recipients can be optionally specified 
                    in the -u flag.
                    </td>
                    <td><ul><li>true</><li class="dft">false</li></ul></td>
                </tr>
                <tr>
                    <td>-p</td>
                    <td>Programs to run</td>
                    <td>Space-delimited list of program, including path, to execute</td>
                    <td>Required if -c is not specified</td>
                </tr>  	
                <tr>
                    <td>-q</td>
                    <td>Quit on error</td>
                    <td><em>True</em> indicates the app terminates execution if a SAS error is detected in a program</td>
                    <td><ul><li>true</><li class="dft">false</li></ul></td>
                </tr>  	
                <tr>
                    <td>-r</td>
                    <td>Resolve SAS Code</td>
                    <td>
                        Indicates if the app generate a corresponding single, stand-alone .sas program file, free of external macro dependencies, for each program 
                        included in a job. The app creates the raw, resolved code SAS program file in the 'resolved' subfolder. The app also creates another version, 
                         formatted for presentation, in the 'formatted' subfolder under resolved. This functionality will evolve over time as new patterns 
                        that didn't resolve or format correctly are brought to SPI and corrected. The resulting program files can be shared externally as 
                        runnable programs without the need to provide Seagen's macro library. Data file dependencies will need to be included in the delivery
                        as they will not become part of the code. 
                        <br />
                        <span class="badge badge-warning text-wrap">Enabling this feature will add significant processing time</span>
                    </td>
                    <td><ul><li>true</><li class="dft">false</li></ul></td>
                </tr>	
                <tr>
                    <td>-s</td>
                    <td>Server</td>
                    <td>
                        Seagen's SAS environment exposes two SAS application servers available to run SAS code. Users can select a specific server to run programs, 
                        or allow the app to make the determination (e.g. best) about which server to use. 
                        <h5>SGSASV1.sg.seagen.com <em>prod</em></h5>
                        <div class="entry">
                            Normally prod is significantly more performant than stage as it has more cores and less 
                            I/O(eg. read/write disc operations) time as the file server is mounted locally.
                            <ul>
                                <li>16 CPU cores</li>
                                <li>200GB RAM </li>
                                <li>Locally-mounted file server which hosts the I, O, and U drives</li>
                            <br />
                        </div>
                        <h5>SGSASV1-stg.sg.seagen.com <em>stage</em></h5>
                        <div class="entry">
                            Stage is intended more as a backup or an alternate server in case prod is down or at 100% utilization. It is validated for produciton use. 
                            <ul>
                                <li>6 CPU cores</li>
                                <li>200GB RAM </li>
                                <li>Networked connection to file server</li>
                            <br />
                        </div>
                        <h5>Best</h5>
                        <div class="entry">
                            'Best' server allow the application to determine which server to submit jobs on based on the CPU availability. Prod is given a bias 
                             in the selection algorithm  as under similar utilization, it will be faster. In parallel mode, the app will 
                             re-evaluate the best server after each batch of programs complete. In sequential mode, the app re-evaluates best server after each 
                             program.

                             There is a time cost to evalute best with each iteration. For small jobs, selecting a specific server might be ideal. 
                             Since the CPU utilization can vary by the second,large jobs can benefit from determining the best server between batchs or programs, 
                             depending on run mode.

                            <br />
                            <span class="badge badge-danger text-wrap">Best algorithm only takes CPU utilization into account. Since both servers use the same 
                            file server (e.g. O: drive) an I/O bottleneck might can cause the poor performance even though a server has high availabilty</span>
                        </div>
                    </td>
                    <td><ul><li>best</><li class="dft">sgsasv1.sg.seagen.com</li><li>sgsasv1-stg.sg.seagen.com</li></ul></td>
                </tr>	
                <tr>
                    <td>-t</td>
                    <td>Display developer and tester</td>
                    <td>Indicates if the Programmer and Tester are displayed in the HTML summary. AI must also be specified.</td>
                     <td><ul><li>true</><li class="dft">false</li></ul></td>
                </tr>	
                <tr>
                    <td>-u</td><td>Notification recipients</td>
                    <td>
                        Optional space-delimited list of recipients to recieve notification. If not specified, current user is notified when -n is true. 
                        <br />
                        <span class="badge badge-secondary text-wrap">-u must be specified for tasks run from SJM Scheduler</span>
                    </td>
                    <td><ul><li class="dft">[don't specify]</li><li>[users] shopkins atellla mness</li></ul></td>
                </tr>	
                <tr>
                    <td>-x</td><td>Server Context</td>
                    <td>
                    Each server has two server contexts available. Unless UTF-8 support is required, <em>SASApp94</em> should be used. Use <em>SASAppUTF98</em> context 
                    for working with datasets encoded in a multibyte character set if trancoding is not possible (e.g. Simplified Chinese) 
                    </td>
                    <td><ul><li class="dft">SASApp94</><li>SASAppUTF8</li></ul></td>
                </tr>                                   
            </tbody>
            </table></div>

    </embed>
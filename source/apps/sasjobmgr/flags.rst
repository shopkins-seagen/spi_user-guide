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
        </style>
            <div><table>
            <thead><tr><th>CLI Flag</th><th>Option</th><th>Description</th><th>Values</th></tr></thead>
            <tbody>
            <tr>
                <td>-a</td><td><a href="function.html#select-run-mode" title="See details"><span class="flag">Run Mode</span></a></td><td>Submit programs in parallel or sequentially</td><td><ul><li class="dft">true (parallel)</><li>false</li></ul></td>
            </tr>
            <tr>
                <td>-s</td><td><a href="function.html#select-server-and-server-context" title="See details"><span class="flag">Server</span></a></td><td>SAS application server to run programs</td><td><ul><li class="dft">best</><li>sgsasv1.sg.seagen.com</li><li>sgsasv1-stg.sg.seagen.com</li></ul></td>
            </tr>
            <tr>
                <td>-x</td><td><a href="function.html#server-context" title="See details"><span class="flag">Server Context</span></a></td><td>Application server context</td><td><ul><li class="dft">SASApp94</><li>SASAppUTF8</li></ul></td>
            </tr>    
            <tr>
                <td>-i</td><td>Interactive</td><td>Display log summary automatically</td><td><ul><li class="dft">true</><li>false</li></ul></td>
            </tr>
            <tr>
                <td>-l</td><td><a href="function.html#review-logs" title="See details"><span class="flag">Review logs</span></a></td><td>Include log review post-processing step</a><td><ul><li class="dft">true</><li>false</li></ul></td>
            </tr>
            <tr>
                <td>-m</td><td><a href="function.html#record-macros" title="See details"><span class="flag">Record macros</span></a></td><td>Include record macro post-processing step</td><td><ul><li class="dft">true</><li>false</li></ul></td>
            </tr>
            <tr>
                <td>-n</td><td><a href="function.html#notify-on-completion" title="See details"><span class="flag">Notify</span></a></td><td>Send email message on completion</a><td><ul><li>true</><li class="dft">false</li></ul></td>
            </tr>
            <tr>
                <td>-u</td><td>Notification recipients</td><td>Optional space-delimited list of recipients to recieve notification. If not specified, current user is notified</td><td><ul><li class="dft">[don't specify]</li><li>[users] shopkins atellla mness</li></ul></td>
            </tr>
            <tr>
                <td>-r</td><td><a href="function.html#resolve-sas-code" title="See details"><span class="flag">Resolve SAS Code</span></a></td><td>Create stand-alone SAS program without external macro dependencies</a><td><ul><li>true</><li class="dft">false</li></ul></td>
            </tr>
            <tr>
                <td>-c</td><td>.csv file</td><td>.CSV file that lists programs for execution. Include path</td><td>Required if -p is not specified</td>
            </tr>
            <tr>
                <td>-p</td><td>Space-delimited list of programs</td><td>Space-delimited list of program to execute. Include path</td><td>Required if -c is not specified</td>
            </tr>   
            <tr>
                <td>-h</td><td>HTML log summary</td><td>Path\name of the HTML summary file</td><td>required</td>
            </tr>  

                   
            </tbody>
            </table></div>

    </embed>
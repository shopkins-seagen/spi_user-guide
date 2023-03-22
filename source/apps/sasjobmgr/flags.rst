.. include:: nav.rst

Commandline Flags Quick Reference
=======================================
The table below lists the flags available and the possible values. Default values are indicated in bold blue font. If a flag has a default, it is optional. The only 
required parameter is either -c, a CSV file that lists the programs to run, or -p a space-delimited list of programs (or logs if -o true). For comprehensive descriptions of 
each option, see `Functionality and Options <interfaces.html#functionality-and-options>`__ .

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
            .dft {color:blue;font-weight:bold;}
        </style>
            <div ><table>
            <thead><tr><th>Flag</th><th>Option</th><th>Values</th></tr></thead>
            <tbody>
            <tr>
                <td>-a</td><td>Run programs in parallel</td><td><ul><li class="dft">true</><li>false</li></ul></td></tr>
            <tr class="alt">
                <td>-b</td><td>Select best server</td><td><ul><li class="dft">true</><li>false</li></ul></td></tr>
            <tr>
                <td>-c</td><td>[path]\[CSV file]</td><td></td></tr>
            <tr class="alt">
                <td>-i</td><td>Interactive</td><td><ul><li class="dft">true</><li>false</li></ul></td></tr>
            <tr>
                <td>-l</td><td>Review logs</td><td><ul><li class="dft">true</><li>false</li></ul></td></tr>
            <tr class="alt">
                <td>-m</td><td>Record macros</td><td><ul><li class="dft">true</><li>false</li></ul></td></tr>
            <tr >
                <td>-n</td><td>Email notification when complete</td><td><ul><li>true</><li class="dft">false</li></ul></td></tr>
            <tr class="alt">
                <td>-o</td><td>Review existing logs only</td><td><ul><li>true</><li class="dft">false</li></ul></td></tr>
            <tr>
                <td>-p</td><td>Space-delimited List of [path]\\[SAS program name]</td><td></td></tr>
            <tr class="alt">
                <td>-r</td><td>Resolve SAS Code</td><td><ul><li>true</><li class="dft">false</li></ul></td></tr>
            <tr>
            <tr>
                <td>-s</td><td>Server</td><td><ul><li class="dft">sgsasv1.sg.seagen.com</><li>sgsasv1-stg.sg.seagen.com</li></ul></td></tr>
            <tr class="alt">
                <td>-u</td><td>Space-delimited list of user to email</td><td><ul><li class="dft">Current user</></ul></td></tr>
            <tr>     
            <tr>
                <td>-x</td><td>Server Context</td><td><ul><li class="dft">SASApp94</><li>SASAppUTF8</li></ul></td></tr>                       
            </tbody>
            </table></div>

    </embed>
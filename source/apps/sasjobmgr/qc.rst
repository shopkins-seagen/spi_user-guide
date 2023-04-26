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
If there is at least 1 QC program included in a run, the application generates the QC summary. The Automated QC Results box at the top of the file provide counts of all, 
passed, and total. Click the button to filter for that QC programs with the desired status.At the program level, the application provides the number of passed/total 
tests for each record. The drop down menu in the Auto QC column header of the Summary of SAS Logs table can also be used to subset rows by QC status.

.. raw:: html 

    <embed>

        <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.2.1/css/bootstrap.min.css"
            integrity="sha384-GJzZqFGwb1QTTN6wy59ffF1BuGJpLSa9DkKMp0DgiMDm4iYMj70gZWKYbI706tWS" crossorigin="anonymous">
        <style>
            .detailFilteredRow {
                visibility: collapse
            }

            .detailUnfilteredRow {
                visibility: visible
            }

            .detailRow {}

            .expandChildTable:before {
                content: '+ Findings'
            }

            .expandChildTable.selected:before {
                content: '- Findings'
            }

            .parentRow {
                border-left: 1px solid #708090
            }

            .childTableRow {
                display: none
            }

            .childTableRow table {
                border: 1px solid #708090
            }

            .isQc {
                visibility: visible;
            }

            .sup {
                color: green;
                margin-left: 6px;
                font-weight: 700
            }

            .failQc {
                color: red
            }

            .passQc {
                color: #00f
            }

            .tableBtn {
                font-variant: small-caps;
                width: 90px
            }

            .filteredRow {
                visibility: collapse
            }

            .unfilteredRow {
                visibility: visible
            }

            .clean {}

            .notice {}

            .note {}

            .warning {}

            .error {}

            .passed {}

            .failed {}

            .filterButton {
                width: 90px;
            }

            .tdCentered {
                text-align: center;
            }

            .filterQcButton {
                width: 90px;
            }
        </style>
        <style>
            .isQc {
                visibility: visible;
            }
        </style>
    </head>

    <body>
        <div class='wrapper'>
            <div class='container'>
                <div style='margin-top:10px;margin-bottom:10px;'>

                    <div class='wrapper'>
                      
                        <div class='isQc'
                            style='float:right;border: 1px solid lightslategray;padding:5px;border-radius: 5px;'>
                            <p style='font-weight:bold;color:midnightblue;'>Automated QC Results</p>
                            <table>
                                <tr>
                                    <td>
                                        <button class='btn btn-sm btn-secondary filterQcButton'>All</button>
                                    </td>
                                    <td>
                                        <button class='btn btn-sm btn-success filterQcButton'>Passed</button>
                                    </td>
                                    <td>
                                        <button class='btn btn-sm btn-danger filterQcButton'>Failed</button>
                                    </td>
                                </tr>
                                <tr>
                                    <td class='tdCentered'>2</td>
                                    <td class='tdCentered'>1</td>
                                    <td class='tdCentered'>1</td>
                                </tr>
                            </table>
                        </div>
                    </div>
                    <div style='clear: both;'></div>
                </div>
                <div class='container' style='margin-top:20px;'>
                    <div style='text-align:center;border-top: 1px solid lightgray;padding:5px;'>
                        <button style='float:left;' id='btn' class='btn btn-sm btn-dark expandChildTable'></button>
                        <h5 style='color:midnightblue'>Summary of SAS logs</h5>
                    </div>
                    <table class='table table-bordered table-sm' style='table-layout:fixed;' id='t1'>
                        <thead>
                            <th style='width:25%;background-color:lightgray;'>
                                <div style='text-align:center;display: flex;'>
                                    <div class='input-group-prepend'>
                                        <label class='input-group-text' style='font-weight: bold;'
                                            for='selIssueLevel'>Status</label>
                                    </div>
                                    <select class='custom-select' id='selIssueLevel' onchange='filterTable()'
                                        style='width:100px;margin:0px;'>
                                        <option class='btn btn-sm btn-secondary'>All</option>
                                        <option class='btn btn-sm btn-danger'>Error</option>
                                        <option class='btn btn-sm btn-warning'>Warning</option>
                                        <option class='btn btn-sm btn-info'>Note</option>
                                        <option class='btn btn-sm btn-primary'>Notice</option>
                                        <option class='btn btn-sm btn-success'>Clean</option>
                                    </select>
                                </div>
                            </th>
                            <th style='width:50%;background-color: lightgray;'>SAS Log <span style='float:right'>(elapsed
                                    time)</span></th>
                            <th style='background-color: lightgray;' class='isQc'>
                                <div style='text-align:center;display: flex;'>
                                    <div class='input-group-prepend'>
                                        <label class='input-group-text' style='font-weight: bold;' for='selQCLevel'>Auto
                                            QC</label>
                                    </div>
                                    <select class='custom-select' id='selQCLevel' onchange='filterTableQc()'
                                        style='width:100px;margin:0px;'>
                                        <option class='btn btn-sm btn-secondary'>All</option>
                                        <option class='btn btn-sm btn-success'>Passed</option>
                                        <option class='btn btn-sm btn-danger'>Failed</option>
                                    </select>
                                </div>
                            </th>
                            </tr>
                        </thead>
                        <tr>
                            <td colspan='3'><span
                                    style='font-weight:bold;color:midnightblue;'>O:\stat_prog_infra\testing\runsas\dotnet\unit_test\data\adam\testing</span>
                            </td>
                        </tr>
                        <tr class='parentRow clean passed'>
                            <td><span class='btn tableBtn btn-success'>Clean</span></td>
                            <td><a target="_blank"
                                    href="O:\stat_prog_infra\testing\runsas\dotnet\unit_test\data\adam\testing\v-test1.log">v-test1.log</a>
                                <sup class='sup'>QC</sup>
                                <i style='float: right;'>(3.1 sec)</i>
                            <td class='passQc'>(3/3) Tests passed</td>
                        </tr>
                        <tr class='childTableRow clean passed'>
                            <td colspan='3'>
                                <h5>Findings</h5>
                                <table id='Findings1' style='table-layout:fixed;width:100%;' class='table'>
                                    <thead>
                                        <tr>
                                            <th style='width:20%'><span>Type (Line#)</span>
                                                <select id='selDetailLevel1' onchange="filterDetails(1)"
                                                    style='width:75px;margin:0px;text-align: left;font-size: smaller;'>
                                                    <option class='btn btn-sm btn-secondary'>All</option>
                                                    <option class='btn btn-sm btn-danger'>Error</option>
                                                    <option class='btn btn-sm btn-warning'>Warning</option>
                                                    <option class='btn btn-sm btn-info'>Note</option>
                                                    <option class='btn btn-sm btn-primary'>Notice</option>
                                                </select>
                                            </th>
                                            <th style='width:80%;overflow-wrap: normal;'>Message</th>
                                        </tr>
                                    </thead>
                                    <tbody>
                                        <tr>
                                            <td>Clean</td>
                                            <td>No log findings</td>
                                        </tr>
                                    </tbody>
                                </table>
                            </td>
                        </tr>
                        <tr class='parentRow clean failed'>
                            <td><span class='btn tableBtn btn-success'>Clean</span></td>
                            <td><a target="_blank"
                                    href="O:\stat_prog_infra\testing\runsas\dotnet\unit_test\data\adam\testing\v-test2.log">v-test2.log</a>
                                <sup class='sup'>QC</sup>
                                <i style='float: right;'>(3.4 sec)</i>
                            <td class='failQc'>(1/3) Tests passed</td>
                        </tr>
                        <tr class='childTableRow clean failed'>
                            <td colspan='3'>
                                <h5>Findings</h5>
                                <table id='Findings2' style='table-layout:fixed;width:100%;' class='table'>
                                    <thead>
                                        <tr>
                                            <th style='width:20%'><span>Type (Line#)</span>
                                                <select id='selDetailLevel2' onchange="filterDetails(2)"
                                                    style='width:75px;margin:0px;text-align: left;font-size: smaller;'>
                                                    <option class='btn btn-sm btn-secondary'>All</option>
                                                    <option class='btn btn-sm btn-danger'>Error</option>
                                                    <option class='btn btn-sm btn-warning'>Warning</option>
                                                    <option class='btn btn-sm btn-info'>Note</option>
                                                    <option class='btn btn-sm btn-primary'>Notice</option>
                                                </select>
                                            </th>
                                            <th style='width:80%;overflow-wrap: normal;'>Message</th>
                                        </tr>
                                    </thead>
                                    <tbody>
                                        <tr>
                                            <td>Clean</td>
                                            <td>No log findings</td>
                                        </tr>
                                    </tbody>
                                </table>
                            </td>
                        </tr>
                    </table>
                </div>
            </div>
            <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.9.1/jquery.min.js" type="text/javascript"></script>
            <script src='https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.6/umd/popper.min.js'
                integrity='sha384-wHAiFfRlMFy6i5SRaxvfOCifBUQy1xHdJ/yoi7FRNXMRBu5WHdZYu1hA6ZOblgut'
                crossorigin='anonymous'></script>
            <script src='https://stackpath.bootstrapcdn.com/bootstrap/4.2.1/js/bootstrap.min.js'
                integrity='sha384-B0UglyR+jN6CkvvICOB2joaf5I4l3gm9GU6Hc1og6Ls7i6U/mkkaduKaBhlAXv9k'
                crossorigin='anonymous'></script>
            <script>function filterDetails(e) { var l = $('#' + 'selDetailLevel' + e).val().toLowerCase(); $('#' + 'Findings' + e + ' > tbody  > tr').each(function (e, t) { if ('all' != l) { var s = $(this).attr('class'); null != s && s.toLowerCase().includes('detailrow') && (s.toLowerCase().includes(l.toLowerCase()) ? ($(this).removeClass('detailFilteredRow'), $(this).addClass('detailUnfilteredRow')) : ($(this).removeClass('detailUnfilteredRow'), $(this).addClass('detailFilteredRow'))) } else $(this).removeClass('detailFilteredRow'), $(this).addClass('detailUnfilteredRow') }) }
                function filterTable() { $('#selQCLevel').val('All'); var val = $('#selIssueLevel').val().toLowerCase(); $('#t1 > tbody  > tr').each((function (index, tr) { if ('all' != val) { var rowClass = $(this).attr('class'); null != rowClass && (rowClass.toLowerCase().includes(val) ? ($(this).removeClass('filteredRow'), $(this).addClass('unfilteredRow')) : ($(this).removeClass('unfilteredRow'), $(this).addClass('filteredRow'))) } else $(this).removeClass('filteredRow'), $(this).addClass('unfilteredRow') })) } function filterTableQc() { $('#selIssueLevel').val('All'); var val = $('#selQCLevel').val().toLowerCase(); $('#t1 > tbody  > tr').each((function (index, tr) { if ('all' != val) { var rowClass = $(this).attr('class'); null != rowClass && (rowClass.toLowerCase().includes(val) ? ($(this).removeClass('filteredRow'), $(this).addClass('unfilteredRow')) : ($(this).removeClass('unfilteredRow'), $(this).addClass('filteredRow'))) } else $(this).removeClass('filteredRow'), $(this).addClass('unfilteredRow') })) } $((function () { $('.expandChildTable').on('click', (function () { $(this).toggleClass('selected').closest('tr').next().toggle() })) })), $((function () { $('.filterButton').on('click', (function () { $('#selIssueLevel').val($(this).html()), filterTable() })) })), $((function () { $('.filterQcButton').on('click', (function () { $('#selQCLevel').val($(this).html()), filterTableQc() })) })), $((function () { $('.tableBtn').on('click', (function () { $(this).toggleClass('selected').closest('tr').next().toggle() })) })), $('#btn').click((function () { $('#t1 > tbody  > tr').each((function (index, tr) { var rowClass = $(this).attr('class'); null != rowClass && rowClass.includes('parentRow') && $(this).toggleClass('selected').closest('tr').next().toggle() })) })), $('#btnToggleFindings').click((function () { $('#t1 > tbody  > tr').each((function (index, tr) { var rowClass = $(this).attr('class'); null != rowClass && rowClass.includes('parentRow') && $(this).toggleClass('selected').closest('tr').next().toggle() })) }));</script>
            <script>$(document).ready(function () {
                    $('#exit').click(async function (e) {
                        e.stopPropagation();
                        e.preventDefault();
                        fetch("http://spi:9090/api/delete?fn=O:\\stat_prog_infra\\testing\\runsas\\dotnet\\unit_test\\data\\adam\\testing\\run_summaries\\summary-shopkins-20230418132950.html",
                            {
                                method: "GET",
                                mode: 'no-cors',
                                headers: { 'Accept': 'text/plain', 'Content-Type': 'text/plain' },
                            }).then(x => { window.close() });
                    });
                });
            </script>



    </embed>

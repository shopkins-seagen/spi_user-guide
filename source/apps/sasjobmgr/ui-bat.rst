.. include:: nav.rst


Create Batch files
========================================
The UI can be used to generate .BAT and CSV files based on the selection in the form. Either select the programs from the UI or use the AI to drive the 
creation of the CSV file. 

As of v2.0, users can generate the CSV file based on the AI, and optionally enable mixed processing mode using dervie order. The app includes 
all the programs that exist on the network where SB_Ignore_Record isn't true. The sequence of the programs is derived by adding Derive_Order to the category offset 
constant. This enforces a sequence by category and allows a place for the QC programs to follow directly after the corresponding primary program category. By default 
all QC programs are given the same sequence so they execute in parallel. 

Users can make updates as needed to the order in the CSV file, there is no further dependency 
on AI for mixed mode processing once the CSV is created.

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
                    <img src="ui-bat.png" alt="GUI" >
                </div>
                <div class="col-6">
                   <h5>Desriptions of the UI Controls for SAS Launcher</h5>
                    <ol style="font-size: 12px;">
                        <li>Enables the .BAT file creation functionality</li>
                        <li>Writes the .BAT and CSV files to the currently selected program location</li>
                        <li>When checked, the app will identify if the corresponding QC programs exists, and if so, include it in the CSV file. If 'Use AI' is selected, the QC programs are listed after all the programs of the corresponding category, otherwise they are listed at end</li>
                        <li>Name of the .BAT file. Does not include path. Path comes from the currently selected program location</li>
                        <li>Select the AI file. This is required to generate the CSV using derive_order to support mixed mode processing. It is also required to display programmer and tester in the HTML summary at execution time</li>
                        <li>Clears the selected AI file and resets options to default</li>
                        <li>Check Use AI to create a the CSV file that include all the programs in the AI that exist on the network and SB_Ignore_Record != True. This must be checked to use derive_order</li>
                        <li>Check to display the developer and tester in the HTML summary for each program. A valid AI must be selected to enable this option</li>
                        <li>Check to create a third column in the CSV based on derive order + [offset const] to enable mixed mode processing. This submits the jobs in sequence and jobs with the same value are submitted in parallel</li>

                    </ol>
                </div>                
            </div>
        </div>
        <hr />
    </embed>

Category Offset Constants for Derive_Order
----------------------------------------------------

.. list-table:: 
  :widths: 30 10
  :header-rows: 1

  * - Category
    - Offset Const
  * - raw
    - 0
  * - SDTM
    - 1000
  * - ADaM
    - 3000
  * - adhoc
    - 5000
  * - derived
    - 7000
  * - harmonized
    - 9000
  * - TLFs
    - 100000
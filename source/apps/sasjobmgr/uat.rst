.. include:: nav.rst

User Acceptance Testing
========================================

.. raw:: html 

    <embed>
        <style>
            .uat{border:1px solid lightgray;border-radius:5px;}
            .dl {padding-bottom:5px;border-top:1px solid lightblue;padding-top:5px;}
        </style>
        <div class="container">
            <h4>Instructions for User Acceptance Testers</h4>
            <ol>
                <li>Identify ~5 production SAS programs in your study that you can run without interfering with any deliverables. It's not critical that they be free of issues, just that you are 
                familiar with the outcome. Avoid choosing very long-running programs for this round of testing. We don't want to overwhelm the already overwhelmed server.</li>
                <li>Groups I and II: Identify at least 2 QC programs that correpsond to selected production programs. It is critical that they use <em>mcrbincomp</em> to perform the comparison of the 
                    qc and production data. If you do not have any QC programs that use mcrBinComp, then omit steps releated to QC</li>
                <li>Download the UAT spreadsheet for your group assignment, and perform the tests listed using your selected programs. Record and deviations from expected results or
                    anything you think may be an issue.</li>
                <li>Attach the completed form in an email to shopkins@seagen.com when you are done</li>
            </ol>
            <p>If you have any questions, first try to use the user guide to figure out the issue, as that's part of the UAT. There is a search box in the upper right hand corner
               if you are having difficulty finding a topic. If it's still unclear, contact me and we can solve the issue and determine if we need to add/update content in the UG</p>
            <div class="row">
                <div class="col-lg-4 uat">
                <h5>Group I: .BAT file</h5>
                    <ul>
                        <li>Adarsh Gunukula</li>
                        <li>Bhavana Bommisetty</li> 
                        <li>Shawn Hopkins</li>
                    </ul>
                    <div class="col text-center dl">
                        <button onclick="window.open('sjm-uat1.xlsx')" class="btn btn-sm btn-primary">download UAT</button>  
                    </div>
                </div>
                <div class="col-lg-4 uat">
                <h5>Group II: SAS Launcher UI</h5>
                    <ul>
                        <li>Alex Tian</li>
                        <li>Hongjie Cui</li> 
                        <li>Irene Liu</li>
                    </ul>        
                     <div class="col text-center dl">
                        <button onclick="window.open('sjm-uat2.xlsx')" class="btn btn-sm btn-primary">download UAT</button>     
                     </div>   
                </div>
                <div class="col-lg-4 uat">
                <h5>Group III: Right-Click</h5>
                    <ul>
                        <li>John Gunshenan</li>
                        <li>Rajesh Jakka</li>
                        <li>Venkatesulu Salla</li>
                    </ul>        
                    <div class="col text-center dl">     
                    <button onclick="window.open('sjm-uat3.xlsx')" class="btn btn-sm btn-primary">download UAT</button>  
                    </div> 
                </div>
            </div>
         </div>
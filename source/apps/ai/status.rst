.. include:: aim_nav.rst
    
Status Assign Algorithm
=============================
The table below lists the steps in the status assignment algorithm in sequence. Evaluation of status continues until a Return is hit, at which time the current status and status description, 
if assigned, are returned for that record.

.. list-table::
    :widths: 50 50
    :header-rows: 1

    * - Independent Programming (IP)
      - Other QC Method (not IP)
    * - #. If a program exists, set status = Programming
        #. If an output exists, then evaluate:      

            #. If no QC program and QC_Status=Ready for QC, return Status=Ready
            #. If a QC program exists, set Status=Testing
            #. If QC_Status = Fail, return Status = Fail
            #. If QC_Date is missing, return Status=Testing, Description = No QC Date
            #. If QC_Result=Pass, set Status = Pass
            
                *Evaluate the following only if inside of Database Lock (or DBL is not specified in init_supp.sas)*

                #. If Output date is after QC date return Status=Retest, Description=Output re-rerun after QC inside DBL
                #. If output date is after QC Log date, then return Status=Retest, Description=Output re-rerun after QC log inside DBL
                #. (TLFs only) If Latest source data date exists and is less than QC Log date return Status = Retest, Description=Source data re-run after QC Log inside DBL
                #. (TLFs only) if Latest source data date exists and is less than QC Date, date return Status = Retest, Description=Source data re-run after QC inside DBL

            #. If Latest macro date exists and after QC Log date, return Status = Retest, Description=Macro modified after QC Log
            #. If Latest macro date exists and after QC date, return Status = Retest, Description=Macro modified after QC
            #. If Program date is after QC Log date, return Status=Retest, Description = Source program modified after QC Log
            #. If Program date is after QC date, return Status=Retest, Description = Source program modified after QC
            #. If an output uses the E2E TLF macros (e.g. col_layout_id, row_layout_id, and pop_set_id are not missing) and the last modified date for row or column layout or pop set are after the QC date, return Status=Retest, Description=Metadata modified after QC.
        
        #. Return Status
      - #. If a program exists, set status = Programming
        #. If an output exists, then evaluate:      

            #. If QC_Status=Ready for QC, return Status=Ready
            #. Set Status=Testing
            #. If QC_Status = Fail, return Status = Fail
            #. If QC_Date is missing, return Status=Testing, Description = No QC Date
            #. If QC_Result=Pass, set Status = Pass
            
                *Evaluate the following only if inside of Database Lock (or DBL is not specified in init_supp.sas)*

                #. If Output date is after QC date return Status=Retest, Description=Output re-rerun after QC inside DBL
                #. (TLFs only) if Latest source data date exists and is less than QC Date, date return Status = Retest, Description=Source data re-run after QC inside DBL

            #. If Latest macro date exists and after QC date, return Status = Retest, Description=Macro modified after QC
            #. If Program date is after QC date, return Status=Retest, Description = Source program modified after QC
            #. If an output uses the E2E TLF macros (e.g. col_layout_id, row_layout_id, and pop_set_id are not missing) and the last modified date for row or column layout or pop set are after the QC date, return Status=Retest, Description=Metadata modified after QC.
            
        #. Return Status
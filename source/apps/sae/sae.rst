Serious Adverse Event Reconciliation Utility
==============================================

The SAE Reconciliation Utility facilitates the reconciliation of serious adverse event records between the safety (ARGUS) and 
clinical (Medidata Rave) databases as described in OP-0095 Serious Adverse Events Reconciliation. The core functionality 
is to identify discrepancies between the Clinical data (coded AE and death data) and the safety database.  Unmatched records 
and corresponding records with differences in the values of critical variables are written in the reconciliation report.



.. toctree::
   :maxdepth: 2

   Protocol Configuration <configure>
   Reconcile SAEs between Rave and Argus <run>
   The SAE Report design <report>
   
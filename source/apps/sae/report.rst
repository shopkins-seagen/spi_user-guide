.. include:: nav.rst

SAE Reconciliation Report 
==================================

Overview 
------------------
The utility reports differences in the Rave and Safety databases using the variable mapping data in the protocol configuration to harmonize and 
compare the critical data points. Records in Rave are joined to Safety by exact matches on **Subject**, **Preferred Term**, and **Onset Date (num)**. |br|

The utility collapses events in Rave using following algorithm prior to comparing with Safety:

    .. note::

        Collapse events by SUBJECT and AESEQ where the end date of the prior event is equal to the start date of the subsequent event. 
        The new collapsed event has following derived fields:

        * Onset date is the first occurence of the serious event (non-serious will be collapsed as long as they meet criteria)
        * End date the end date of the last contiguous event
        * Outcome is an outcome of the last event
        * Relationship to drug(s) is worst case (e.g. related)

The utility compares the value of the critical variables for matching records and reports differences. Any unmatched(no corresponding event by subjects, PT, and onset)  serious 
records from either Rave or Argus are output to the report.

The utility tracks a record by hashing the values of all the critical variables into a unique identifier. A user can assign a status, action, or comment to a record and it 
will persist for the life of that record. If any of the values that contribute to the hash change, then the record will be perceived as new and requires review again. Any previous 
reivew will move to the review history table. 

Report structure
-----------------------------------
The SAE reconciliation reports is an Excel workbook with two worksheets, Summary and Data. |br|

The summary worksheet summarizes the number of open records for the following categories:

    * Unmatched Rave records - A record in the clinical database without a match in Argus
    * Unmatched Safety records - A record in Argus without a match in the clinical database
    * Discrepancies - Unequal values for critical fields in corresponding records between Safety and Rave.

The data worksheet contains the critical data points for each unmatched and discrepant record. The Issues field identifies the discrepant variable(s) for matched records and
the source (e.g. Rave or Safety) for unmatched records.  each record contains. Discrepant fields are clearly marked with colored border and background. |br|

The report contains a *user interface* section with light background surrounded by double blue margins. User records  Status, Action, and Comments that can be uploaded and 
associated with the record. The review will remain associated with that record until a critical data point in that record changes. No other fields should be modified. Unhiding 
and modifying HashId or ProtocolId and uploading the file will corrupt the database.

Saving SAE recon report review
---------------------------------
After records in a report have been assigned statuses, actions, and comments, the user saves and closes the file, and uses the **Upload** menu item to send the upload the contents of the selected 
file to the database. The application will manage the record statuses using the unique record identifies.

. The hashid and protocolid fields are the keys for the tracking the records. The utility can take one of three actions for a record upon upload:

    * New hashid - the utility inserts the new record into the Review table. 
    * Existing hashid - the utility updates current record with the new data and writes the old data into the audit table
    * Unmatched hashid in the database - this indicates a critical data point for a previously reviewed record has changed. The record will be moved to the audit table. 


SAE recon report content
------------------------------------
The following table describes each field of the report. 

.. list-table::
  :widths: 15 85
  :header-rows: 1

  * - Field
    - Description
  * - HashId (hidden)
    - Unique identifier for a record created using SHA256. Persists until a variable contributing to the hash changes. 
  * - ProtocolId (hidden)
    - Unique identifier for protocol
  * - Issues
    - Delimited list of discrepant data points or unmatched Status
  * - Subject 
    - Unique subject identifier
  * - Case number
    - Case number in Argus associated with the event
  * - Log Line
    - Concatenation of AESEQ and RecordPosition from Rave AE data section
  * - Case Status
    - The workflow state of the case in Argus
  * - Initials
    - Subject's Initials
  * - Verbatim
    - Reported event Term
  * - Preferred Term
    - Coded event Term
  * - Onset Date
    - Start of event
  * - End Date
    - End of event
  * - Last Exposure/EOT
    - Cutoff date for safety reporting period. If onset is > *Last Exposure/EOT* then subject is outside safety reporting period (identified by green font in this field)
  * - Serious
    - Boolean indicator seriousness. If a record in Argus has no serious matching event in Rave, the utility will attempt to identify a matching non-serious event.
  * - Death date
    - Death date for events recorded as Fatal
  * - Related to [product]
    - One or more relationship to study drug data points. The labels for relationship columns are derived from the SAS variable label. Change the label in the AE dataset to 
      change the label in the report
  * - Status [editable]
    - Discrete list of values the user can assign to a record.

        * **Open**  (default)
        * Closed
        * DBL_review

  * - Action [editable]
    - Discrete list of actions the user can assign to a record

        * **None** (default)
        * Queried_DM 
        * Queried_PL 
        * Queried_Safety
        * Verified_Discrepant
        * Other

  * - Comment [editable]
    - Free-text comment field
  * - Reviewer
    - username of the reviewer that uploaded the record the last time it was altered
  * - Run date
    - Date the report was created

SAE Reconciliation database
---------------------------------------
The SAE utility persists configuration and review data in a SQL Server database. The database is accessible to DM and can be used to generate 
metrics across protocols or investigate review histories. Any technology that supports a connection to SQL Server can be used to query the database 
(contact IT for details). 

  .. warning:: 
   Only perform read operations on backend as updates not executed through the UI may corrupt the database.

Database design
++++++++++++++++++++++++

.. list-table::
  :widths: 15 25 85
  :header-rows: 1

  * - Table
    - Relationships
    - Description
  * - AdverseEvent
    - **PK** ProtocolId is the unique identifier for each protocol 
    - Captures the configuration details for each protocol.
  * - Relationship
    - One to many relationship with *AdverseEvent* on **ProtocolId**
    - Captures the relationship to study drug(s) for each protocolid
  * - Review
    - One to many relationship with *AdverseEvent* on **ProtocolId**
    - Captures the current state of SAE reconciliation. Records in this table are uniquely identified by HASHID, a 
      SHA256 hash of all the values of critical fields. The value of HASHID changes when any value of the critical field changes.      

      
      Enumerations for **STATUS**

      .. list-table::
       :widths: 10 30
       :header-rows: 1

       * - Code
         - Decode
       * - 0 
         - Open
       * - 1 
         - Closed
       * - 2 
         - DBL_Review

      Enumerations for **Action**

      .. list-table::
       :widths: 10 30
       :header-rows: 1

       * - Code
         - Decode
       * - 0 
         - None
       * - 1 
         - Queried_CRF
       * - 2 
         - Queried_PL  
       * - 3 
         - Queried_Safety
       * - 4
         - Verified_Discrepant        

  * - ReivewHistory
    - One to many relationship with *AdverseEvent* on **ProtocolId**
    - Provides audit trail for Review table. Retired or updated records are written to this table.
  * - AeOutcome
    - n/a
    - Standardized values of Outcome from Rave
  * - SafetyOutcome
    - One to many relationship with *AeOutcome* on **AeOutcomeId**
    - Maps outcome in Safety to outcome in Rave

Entity relationship diagram
+++++++++++++++++++++++++++++++++
.. image:: /_static/erd.png


          
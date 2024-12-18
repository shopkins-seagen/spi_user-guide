.. include:: nav.rst

FSP Guidance
=====================================================

For certain DID to be available in Daily Survey for FSP colleagues, following are some points to take:

* "FSP Other PoC" has value in internal DID area https://pfizer.sharepoint.com/sites/SDSADIDManagement/Lists/DID_0/DID_0.aspx . 
* DID information synchronizes from internal DID to FSP DID area twice a day at 6:00 and 16:00 (UTC-8 time zone) if 'FSP Other PoC' has value
* For certain DID available in Daily Survey (for both internal and FSP colleague), 'DID Status' must turn to 'Ongoing' for DID (exclude DID_0). In order for DID status to turn to 'Ongoing'
    #. The DID corresponding d_LoT is present in d_LoT Repository in DID tool
    #. SDSL manager approves the DID
    #. The Planned Delivery Date for that DID is within 90 days from today (could extend to 6 months depending on SDSL selection when creating DID)
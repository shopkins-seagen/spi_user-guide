Analysis LifeCycle Manager v3 
=============================================================



The Analysis LifeCycle Manager v3(ALM) is the first version of ALM without a dependency on Candid. Users can create analyses on the file system without having a corresponding 
entry in the Candid analysis management system. This limits analyses to a single source of raw data by default (e.g. CDM libref), though users can extend 
non-standard data sources through init_supp.sas. Projects like iSAFE cannot use this version of ALM. 

Version 3.2 works seamlessly with analyses created in previous versions of ALM v3.0+ without migrating. See SPI for assistance if you are working on a study with multiple data sources in Candid and want to use ALM 3.2. 

.. toctree::
   :maxdepth: 2
   :caption: Functionality

    Create new study folders <new>
    Update/localize existing study folders <update>
    Delete or rename an analysis or production-level folders <delete>


.. warning::

   Use for a SAS VM when using ALM, especially for actions like snapshot, localization, or copying from an existing analysis. If you do not, the app could run 
   for a long time.



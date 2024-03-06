.. include:: nav.rst

SetTransfer Endpoint
================================
The settransfer endpoint parses the body of a POST request and creates a new transfer request in the database. 

The JSON Body Request Format
------------------------------------
The SPI department macro is responsible for formatting the user arguments into JSON to pass to endpoint via PROC HTTP. 

.. list-table:: 
  :widths: 20 80
  :header-rows: 1

  * - Key
    - Value Description
  * - protocol
    - name of the protocol-level folder under which the study-facing SAS program resides
  * - analysis
    - name of the analysi-level folder under which the study-facing SAS program resides
  * - indir
    - network path of the location of the input database
  * - outdir
    - network path of the location of the output data
  * - sjmjob
    - the description field of the SAS job defined in SJM scheduler 

Example
++++++++++++++++

.. code:: JSON

   {
    "protocol":"blinding_process",
    "analysis":"blinding",
    "indir":"O:\\stat_prog_infra\\testing\\blinding_process\\blinding\\dotnet\\data\\raw",
    "outdir":"O:\\STAT_PROG_INFRA\\TESTING\\BLINDING_PROCESS\\BLINDING\\DOTNET\\DATA\\ADAM",
    "sjmjob":"test"
   }

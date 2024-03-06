.. include:: nav.rst

GetTransfer Endpoint
================================
The GetTransfer endpoint returns the Transfer Request object defined in the SetTransfer endpoint. This allows the arguments from the orginal, study-level program to pass 
arguments to the department-level utility without compromising security boundaries. 

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
  * - sjmjob
    - the description field of the SAS job defined in SJM scheduler 

Example
++++++++++++++++

.. code:: JSON

   {
    "protocol":"blinding_process",
    "analysis":"blinding",
    "sjmjob":"test"
   }



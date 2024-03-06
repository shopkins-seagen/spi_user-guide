.. include:: nav.rst

UpdateTransfer Endpoint
================================
The UpdateTransfer endpoint populates the IsTransferSuccessful field SasDataSets collection for the specific TranferRequest in the database. 

The JSON Body Request Format
------------------------------------
The SPI department macro is responsible for formatting the user arguments into JSON to pass to endpoint via PROC HTTP. 

.. list-table:: 
  :widths: 20 80
  :header-rows: 1

  * - Key
    - Value Description
  * - TransferId
    - Primary key that uniquely identifies the Transfer in the database
  * - IsSuccess
    - Boolean that indicates if the transfer was successfully completed or not
  * - Data
    - Key:Value pairs of dataset:{variables} that were blinded in the Transfer object. 

Example
++++++++++++++++

.. code:: JSON

   {
    "id":1,
    "issuccess":true,
     {"dsn1":{"var1","var2"},"dsn2":{"var1","var2"}}
   }
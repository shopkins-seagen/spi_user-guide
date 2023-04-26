.. include:: nav.rst

SAS Job Manager
=======================================
The SAS Job manager(SJM) is a distributed .NET application that provides functionality for users to submit SAS program files in batch mode from the Biometrics file share. SJM replaces 
the current version of RunSAS. 

Initial Setup
---------------------
There are two dependencies that must be installed on the SAS VM prior to using the application. 

#. .NET 6 Windows Desktop Runtime x64 - this must be installed by an adminstrator. Contact SPI if you do not have the runtime (you'll know as the SAS launcher will prompt you to install it)
#. Install the context menus for the SAS Job Manager. Download the SAS Job Manager Package from `[here] <http://sgcpapp1/cp/programming/registry/library.html>`__ , extract to your VM, and double-click to install `[see instructions] <http://sgcpapp1/cp/programming/registry/add.html>`__.

Table of Contents
--------------------

.. toctree:: 
   :maxdepth: 3

   interfaces
   function   
   qc

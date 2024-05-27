.. include:: nav.rst

RAR Archive Unpacker
========================================
The RAR Archive Unpacker provides functionality to unpack the files in a RAR archive to the network and optionally translate the unpacked file names into English. The system consists of a 
SAS macro, mcr_spi_rar_unpacker, that calls an ASP .NET Core API that performs the unpacking and translation services. 

Macro Parameters
-------------------------------------------

.. list-table::    
    :widths: 20 50 30
    :header-rows: 1

    * - Parameter
      - Description
      - Valid values    
    * - in_rar
      - Path and file name of the .RAR file to be unpacked
      - Network path\\file name of RAR file.  
    * - out_dir
      - Path of the folder to write the contents of the .RAR file
      - Network Path
    * - password
      - Optional password for encrypted RAR files. Leave blank if there is a password.txt file that contains the password in the same folder as RAR file.
      - string
    * - convert_chinese_yn
      - Optionally converts the file name of the unpacked files from Chinese to English
      -       
        .. list-table:: 
           :widths: 10 50
           :header-rows: 1
                        
           * - Value
             - Description
           * - **Y**
             - translate the unpacked file names from Chinese to English as needed
           * - N
             - do not translate unpacked file names 

    * - preserve_folders_yn
      - Optionally maintains the folder structure from the RAR archive to OUT_DIR
      -       
        .. list-table:: 
           :widths: 10 50
           :header-rows: 1
                        
           * - Value
             - Description
           * - **N**
             - extract all the files to OUT_DIR
           * - Y
             - preserve the folder structure defined in the RAR archive when unpacking contents to OUT_DIR.
             
    * - spi_debug_yn
      - Optionally enables debugging features defined by the macro developer
      -       
        .. list-table:: 
           :widths: 10 50
           :header-rows: 1
                        
           * - Value
             - Description
           * - **N**
             - disables debugging mode
           * - Y
             - enables debugging mode                            

Example Macro Calls
-----------------------

Unpack All Files to a Single Folder and Translate File Names to English if Necessary
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
Default macro call that will unpack the files of the RAR archive to OUT_DIR and translate the file names to English if Chinese characters are detected. If the RAR archive 
is encrypted, the assumption is that password.txt exists in the same folder as the RAR file and contains only that password (no other content is allowed).

.. code:: 

     %mcr_spi_rar_unpacker(
             in_rar= &currdir.\%nrstr(RC48-C001_PK&ADA data_20200224.rar)
            ,out_dir= &outdir.);

Unpack Files Preserving the Folder Struture Defined in an Encrypted RAR Archive without a Password.txt File
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
This macro call will unpack the folders and files under OUT_DIR and not convert the file names to English. Password is passed 
directly to the macro as there is no corressponding password.txt file in the same folder as the RAR file.

.. code::

    %mcr_spi_rar_unpacker(
          in_rar= &outdir.\src\%nrstr(RC48-C001_PK&ADA data_20200224.rar)
         ,convert_chinese_yn=N
         ,preserve_folders_yn=Y
         ,password=%nrstr(C001@2020)
         ,out_dir= &outdir.);
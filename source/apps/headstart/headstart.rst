HeadSTART - Header SAS Template and Readying Tool 
=========================================================
HeadSTART is a .NET Core 3.1 console application invoked from the context menu of the background of any folder in Windows Folder Explorer. While the app 
will create a .SAS program file with the standard header, the suggestions for prefix and purpose are only available for Statistical Programming analyses 
under the O: drive. 

Invoke the Application
-----------------------------
#. Right=click in the background of Windows File Explorer in the folder you want to create a new program and select *Create new SAS program w/Header*

    .. image:: invoke.png 

    .. note:: 
        
        While you can create a program anywhere, the app will display a warning if the location is outside a pgms or testing subfolder 

#. Enter the name of the program. In a testing subfolder the app suggests the prefix "v-". You do not need to type the extension .sas.
#. The application suggests a purpose for the program based on the location of the program and program name. Modify the text as needed.
#. The application creates the SAS program file and populates the standard header with the available details. 
#. Once the program is created, the app presents three keystroke options to user:

    * Press *Enter* to create another SAS programs
    * Press *e* to open the program in SAS Enterprise Guide and quit HeadStart
    * Press *Esc* to quit HeadStart 


.. warning:: 

    Do not modify the structure of the standard header. You can add content and adjust the values under program history, but the keywords to the left of the semicolon 
    (e.g. Program, Purpose) and the heading lines (e.g *Seagen Standard Program Header [v1.0]* and *Program History*). ALM 3.2.4 uses those targets in the header 
    to update the program headers when copying an existing analysis into a new analysis. It will not update headers when you update an existing analysis or create a new 
    snapshot.
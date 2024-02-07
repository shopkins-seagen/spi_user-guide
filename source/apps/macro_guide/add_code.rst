.. include:: nav.rst

Add a Macro From Existing SAS Code File
=================================================
The fastest way to add a macro to the database is to have the application parse the code of an SAS program file. Click the |addcode| button to navigate to the 
upload page. 

Optionally download  `All Items page <https://seagen.sharepoint.com/sites/BMInfra/Lists/ADaMSDTM%20Macros/AllItems.aspx>`__ to the  location specified in |spo| 
to get utility type, scope, and URL. This step is optional as the fields can be updated using the edit buttons from the Macro Library (home) page.

In order the app to parse the macro, it must follow 
a particular format (described below). If the macro  doesn't follow the expected format, copy the macro to a new folder,
update the header and keyword parmeters to match the description below. Copy and paste the path into the |folder| box and click |update|. 

Use the filter to find the macro, and click the |add| button have the app parse and add the new macro to the database. Return to macro library by 
clicking |home|. Use the edit functionality as needed to clarify fields or correct parsing errors. 

.. note:: 

    In order for the application to parse the macro, the macros must be 
    recorded in specific format. There is some flexibility built into the parser to handle variations, but to ensure accurate parsing adhere to the following rules.

    #. Record a brief description of the macro after the Purpose: key in the macro header. The descrition may span multiple lines, but leave a space before the next section.

        .. code::

            | Purpose : Create shell for ADEQ5D.
            |
            | ----------------- Version History ------------------------------------------------------------------------

    #. Record parameters in the following format        

    .. code::

        ,parameter =  <default if available> /* parameter description limited to just a single line */


.. warning:: 

    The |library| functionality is restricted to the application owner as this can have undesired consequences
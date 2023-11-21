.. include:: nav.rst

SAS Macro Quick Reference
====================================
The `SAS Macro Quick Reference <https://sgcpapp1:8082/>`__ provides a searchable interface to quickly lookup details about SPI department macros. The first time the site is 
opened on a computer, it may have to be reloaded once, if the client certificate is not located. Just refresh the site using the browser refresh button and the issue will 
resolve. The scope of the content only include SPI macros, e.g. macros that start with 'mcr_spi'. 

Browse for macros using the text filters above either the macro name or description. By default, the filter type is set to 'contains' and is case-insenstive. The filter type 
can be changes using the filter select button |filteron|. Remove a filter by using the filter clear button |filteroff|.  

.. image:: filter-text.png

View the Parameters, Descriptions, and Defaults
-----------------------------------------------------
The |expand| button to the left of the macro displays the available paramters, descriptions (if recorded by the devloper), and any default values. 

.. image:: parms.png

Command Buttons
-----------------------------------------------
The application has 3 command buttons associated with each macro:

#. |copy| - copies the macro parameters into the user clipboard. Use Paste to paste the contents of clipboard into your SAS program editor.
#. |preview| - displays the macro parameters in the format they will be captured in the clipboard. Users can also optionally copy the parameters to the clipboard using the 
               copy button exposed in this control. 
#. |ug| - opens the user guide in the SPO site. 


.. note:: 

    It's possible that scope and UG are not available. Contact SPI to update the contents if the user guide exists in SPO, but is not available in the app. 

    

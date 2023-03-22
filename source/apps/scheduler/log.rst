Reviewing the Automation log
==========================================
Every time a SAS job is run though automation, an entry is crated in the automation database. Users can access this information via a tabled-value function on the 
SQL database in SAS via pass through. 

#. Get the name of the data server and report ID from the configuration window of the scheduler app 

    .. image:: id.png

#. Run the following code in SAS 

    .. code:: Python

        %let server=SEACLPDB01D.DEVSG.SEAGEN.COM\DEV,25000;
        %let reportId=11;

        proc sql;
            connect to odbc ("DRIVER=SQL Server;SERVER=&server;DATABASE=stat_prog_automation;");
            create table log as select * from connection to odbc
            (SELECT * FROM [dbo].[fnGetRunLog](&reportId.));
            disconnect from odbc;
        quit;


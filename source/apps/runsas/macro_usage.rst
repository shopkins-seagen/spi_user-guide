Design of SAS Autocall Macro Usage Metrics
=============================================

#. The application conditionally enables macro usage collection (e.g. the steps that follow) if *IsLogging* is set to *true* in the app configuration file.
#. RunSAS submits the SAS code for the SAS program file. Once the code has executed, and if IsLoggin is true, the application submits the following code to 
   same instance of the workspace server process:

    .. code-block::

        %put SPI_STOPLOG;   /* Causes the LOG lines from this code to be excluded from log file that gets written to the network */

        /* Creates a dataset containing the autocall macros compiled in the session that start with mcr and have a non-missing description attribute */
        proc catalog cat = work.sasmac1 entrytype = macro;
            contents out=spi_macros(keep = name desc where =(upcase(name)=:'MCR' and ^missing(desc)));
        run;

        /* Creates a dataset containing environment macro variables in the WORK libref */
        data spi_env(keep= product--program);
            length product protocol analysis release $100 isLocalized $2 level $10 program $500 var $32;
            array vars[*] product--program;
            array env[7] $100 _temporary_('PRODUCT' 'PROJECT' 'ANALYSIS' 'DRAFT' 'ISLOCALIZED' 'FOLDERLEVEL' 'PGMDIR');
            do i = 1 to dim(vars);
                var = env[i];
                if symexist(var) then do;
                    vars[i] = resolve('&' || env[i]);
                end;
                else vars[i] = 'NA';
            end;
        run;

        /* Passes the physical location of the WORK libref to RunSAS via log object */
        options ls=max;
        %let spi_runsas_work=%sysfunc(pathname(work));
        %put SPI_RUNSAS_WORK=&spi_runsas_work;

#. RunSAS reads the SPI_ENV and SPI_MACROS datasets as network files via OLEDB and imports the SAS data into the application's environment.
#. RunSAS models the data from SPI_ENV and SPI_MACRO for reporting and passes the object to JSON serializer which writes the data to a globally accessible location.

    Example of JSON file:

    .. code-block:: 

        {
            "Product": "testing",
            "Protocol": "generic-utility",
            "Analysis": "runsas_1000",
            "Draft": "v01",
            "Pgm": "O:\\stat_prog_infra\\testing\\generic-utility\\runsas_1000\\v01\\data\\adam\\pgms\\macro1.sas",
            "Work": "F:\\Users\\shopkins\\AppData\\Local\\Temp\\SAS Temporary Files\\_TD30320_SGSASV1_\\Prc2",
            "RunDt": "2020-05-19T00:00:00-07:00",
            "Macros": {
                "MCRBINCOMP": "Version 1.1",
                "MCRMIXEDCASE": "Version 1.0"
            },
            "Level": "ANALYSIS",
            "IsLocal": false
       }

#. The JSON files are deserialed, modeled, and added to the database by an uncoupled service that can be triggered by a folder event, schedule, or manual trigger.

    .. note:: 

        The name of the JSON file is the same as the PK for the FULLSTIMER and I/O Performance Counter metrics tables. This value is captured in the macro usage table to allow the user 
        to link macro usage and performance metrics (if performance metrics also are enabled).
Performance of OMS transactions - OMSSchemaMetrics
=====================================================
The Python script obtains various schema metrics like table size, index size, tablespace size, table row count from the Oracle database for a specific IBM Sterling OMS environment/compartment, based on the parameters specified in the parameterized SQL Query in the property file, and generates an excel report, or appends the data to the appropriate excel file if one exists.


Benefits
========
> Effort is reduced by 90% by using this tool.

> Zero error rates and High turnaround

> Run single or multiple enviorment together

> Utility can be integarted with Jenkins or Microsoft Task Scheduler to run automatically at anytime.
****Script Details**** 
======================
1. config.properties file:
 -Defines all required parameters 
 -List of variable & its description:
----------------------------------------------------------
> env --> environment identifier like QA / Stage / Prod
> defaultenv --> when env input is not passed, default env is taken 
> dbconnect<env> --> database connect string for particular environment
> output_filename --> name of the output file. ex: QA or PERF, where file is taken as xlsx inplicitly ex: QA.xlsx
> Query_values --> Specifying which SQL queries to run 
  ex: Query_values=["IndexSizeQuery","TableSizeQuery","RowCountQuery","TableSpaceQuery"]
> IndexSizeQuery,TableSizeQuery,RowCountQuery,TableSpaceQuery --> Parameterized SQL query used for fetching required transactions
> Table_Space_Name=["SOM_STERLING_AUDIT","SOM_STERLING_HISTORY","SOM_STERLING"] --> Identifier used in parameterized SQL query for Table_Space_Name
> Owner_Name="STERLING" --> Identifier used in parameterized SQL query for Owner_Name
> Table_Owner="STERLING" --> Identifier used in parameterized SQL query for table_owner

2. ProdTableStats.exe
> Includes main steps to validate env and dbconnect variable values, if single or multiple databases.
> Reads the data from the config file and executes function to connect to database, call child function to fetch dataframes with stats data, forms the required excel report


****How to run****
===================
1. Place the Config.properties script and the executable file in the same folder
2. Update the config.properties file with valid data.
3. Go to the respective .exe folder and using the command specified in "command" section run the exe file .
Note: The bootloader takes ~2 minutes to uncompress the support files used by the script.
4. Excel sheet with the respective stats report is generated in the output folder defined in the config file.

Command
=======

ProdTableStats.exe <env> <config filepath>
 
Single Env example : ProdTableStats.exe QA C:\config.properties 

Multiple Env example : ProdTableStats.exe QA,PERF C:\config.properties
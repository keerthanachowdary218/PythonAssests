Performance of OMS transactions - critical components
=====================================================
The Python script captures performance metrics for IBM Sterling OMS from the Oracle database and generates an excel report, or appends the data to the appropriate excel file if excel exists. This metrics can be captured for any enviorment like QA / Prod and for any agents which are configured in the property file. 

Performance metrics such as the number of invocations, the number of GetJobsProcessed, and other parameters supplied in parameterized SQL queries specified in property file are captured based on the server selected (agent, integration, or both), as well as the environment defined.   


Benefits
========

> Effort is reduced by 90% by using this tool.

> Making it automated there are zero error rates and high turnaround.

> Run single or multiple enviorment together

> Utility can be integarted with Jenkins or Microsoft Task Scheduler to run automatically at anytime.


****Script Details**** 
======================
1. Config.properties file:
 -Defines all required parameters 
 -List of variable & its description:
----------------------------------------------------------
> env --> environment identifier like QA / Stage / Prod
> defaultenv --> when env input is not passed, default env is taken 
> dbconnect<env> --> database connect string for particular environment
> dop = "/*+ PARALLEL 12 */"  --> Identifier used in parameterized SQL query for Degree of parallelism 
> Server=["AGENT","INTEGRATION"] --> Specify AGENT OR INTEGRATION to execute respective related server queires 
> Statistics_Detail_Key --> when this input is not passed, this default value is taken which is starting date. (format: YYYYMMDD)
> Agent_Query_values=["AGENT_XXXQuery","AGENT_YYYQuery",]--> List all the critical agent servers 
> AGENT_XXXQuery --> Define the sql for each critical agent server mentioned above. 
> INTEGRATION_MultiServerQuery --> Parameterized SQL query used for fetching required transactions of integration server in IBM sterling OMS that can run for multiple servers mentioned in variable INTEGRATION_MultiServer_Name
> INTEGRATION_MultiServer_Name --> List of critical integration server names. 


2. criticalComponentsStats.exe
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

criticalComponentsStats.exe <env> <Statistics_Detail_Key> <config filepath>

Single Env example : criticalComponentsStats.exe QA 20221105 C:\config.properties 

Multiple Env example : criticalComponentsStats.exe QA,PERF 20221105 C:\config.properties
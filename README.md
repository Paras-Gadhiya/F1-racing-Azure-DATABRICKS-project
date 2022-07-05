# F1-racing-Azure-DATABRICKS-project
In this project, we used the Azure cloud services to get done data engineering operations (Ingestion, Transformation, Analysis, Load) on Formula-1 Racing Dataset Available from 'eargst developer API' which includes both 'CSV' and 'JSON' (single and also split) files. we also manage the incremental load and full load approach to dealing with some of that files and the notebook workflow via Azure Data Factory pipelines and  Azure Databricks Itself. we schedule that pipelines with tumbling window trigger to get execute that pipeline. but let's discuss this in a more granular manner.

Try to address these Problems:
----------------------------------
1. Need an Automated system that can handle hybrid load (full + Incremental).
2. update and delete certain data and also can restore that data as original state.
3. Data comes periodically (i.e. every sunday)

Objective:
--------------------
1. To provide a solution that can handle a large amount of periodic data with 'incremental load' and 'full load' support with Azure Databricks to do some of the        data engineering operations(ingestion, transformation, analysis, load) and also Utilize Azure Data Factory to schedule these Activities in form of Pipelines.
2. Implement the "Delta lake" solution for this project in order to achieve update and delete support or we can say, history and Versioning support via keeping        transaction logs of all aggregated activities that we perform on our delta tables.  

Used technologies:
-------------------------
1. Azure Databricks (Pyspark, SparkSQL)
2. CLI (For Access Databricks File System)
3. Azure Data Factory
4. Delta Lake

Solution
---------------
Step-1: Get your Data from "http://ergast.com/mrd/db/#csv" and Store it Into DBFS via CLI.
------------------------------------------------------------------------------------------------------------------------------------
Step-2: Ingest 4 Fies with Fully loaded and other 4 Files "Incrementally Load"  via Pyspark notebook into spark Dataframe.

 * CSV (Single File, Multiple Files)
 * JSON (Multi-Line, Single-Line  && Single File, Multiple Files)

> Note: Here, we Ingest data From Multiple formats and types.

Step-2: Transformation 
------------------------------------------------------------------------------------------------------------------------------------
 * Combine columns i.e. 'forename' and 'surname'.
 * Filter Columns data i.e. 'points'>=0 and others.
 * Window, Grouped, Simple Aggregation i.e. windows RANK() (give ranking to Drivers and Teams)
 * Join multiple data frames to make Ideal Data.
 * Add Audit columns i.e. current_timestamp().
 * Create Dependency between columns i.e. 'points' Dependent on 'positions'.
 * Add a column for storing data received via notebook parameters i.e. 'file_source', 'file_date'.
 * Drop Unwanted columns i.e. ~~'URL', 'altitude', 'longitude'.
 * Rename columns for better Understanding 'DriverID' =>'driver_id' (More Pythonic manner)

Step-3: Load Transformed data into different formats (.parquet & .delta)  
------------------------------------------------------------------------------------------------------------------------------------
 * External Tables.
 * Managed Tables.
 * Delta lake tables.
 
 > Note: Here, we store that data into all above 3 in separate locations.

Step-4: Analysis 
------------------------------------------------------------------------------------------------------------------------------------
 * Top-5 drivers.
 * Top-5 Teams.
 * Top-5 races.
 * Popular Circuits(race tracks).

Step-5: Schedule and execute Databricks Notebook with Aure Data Factory.
------------------------------------------------------------------------------------------------------------------------------------
 * Develop parameterized Pipelines.
 * Schedule tumbling window trigger for specify time for execute Pipeline.
 * Handle Pipeline Failure with other data factory activity i.e. getMetaData, if..else.



Thank You!
------------


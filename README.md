# ADF_with_Databricks

Databricks Data Engineering End-To-End project, developed to meets enterprise production standards

1. Modular & Reusable
   Cleanly separated into reusable functions:
   read_data block,
   enrich_data block,
   write_to_table block,
   Orchestration block,
   Accepts parameters (from ADF widgets), which is crucial for dynamic workflows

2. Auto Loader for Incremental Load : 
   Uses cloudFiles with .trigger(once=True) for batch-style streaming, 
   Uses checkpointLocation — critical for incremental tracking and fault tolerance, 
   Supports schema evolution 

3. Corporate-Grade Logging: 
    Logger initialized with both console and file handlers, 
    Logs written to Unity Catalog volume for traceability, 
    All stages log start, success, and errors clearly, 
    Includes full traceback in logs for error troubleshooting,   

4. Error Handling & Recovery: 
   Uses try-except blocks around all critical functions, 
   Catches both Exception and AnalysisException (for schema/table errors), 
   Errors raise RuntimeError to fail ADF pipeline if necessary  

5. ADF Compatibility:  
   Parameters are passed using dbutils.widgets, 
   Notebook is restart-safe, restartable, and rerunnable, 
   Failures propagate properly back to ADF  

6. Streaming and Batch Compatible:  
   write_to_table() gracefully handles both streaming and batch DataFrames, 
   Auto Loader works well in both high-volume production and small-scale testing 

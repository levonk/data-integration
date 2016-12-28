# data-integration

## Implementor Guidelines

Given the information from the other two sections

 * Requestor
 * Supplier

Implement the system with these guidelines


### Data Implementaion Guidelines

  * Loads
	* Prefer paritions with latest pointer in meta-store instead of droping data
    * Do not drop tables unless successful load to partition/temp table has happened
	* Perform validations before load
	* Have standardized file naming 
	* raw data should be ingested without any transformations
	* ingest date should be parameterized
	* ingest should probably include some amount of rolling load in case there was an issue
	* Schedule early in the work day for any data which is sensative to data collection sampling
  * Transformations
    * Use static/mock data tests for positive/negative tests of all transformations
	  * Must have test input data
	  * Must have expected output data (incl. exceptions file)
	* Have preconditions, postconditions and invarients in data load
    * Standardized Date Representation
	  * Standardized Time Zone
    * Assure compressed: Parquet uses native compression
    * Assure splittable: Parquet is splitable
    * Assure block size
    * Assure Encoding is standardized
    * Partition for performance
    * Standardized file and column naming
    * Convert to storage format: Parquet
	* Register with meta data store
	* Register with schema registry
	* Publish versioned schema
	* Publish documentation
	* Assure has primary key
	* Assure has ingest datestamp
	* Assure has created_ts, last_updated_ts and deleted_ts timestamps
	* Assure Primary Key balances well across MPP/Hash
	* Assure has master data mapping as opposed to unique IDs
  * Workflows
    * Assure meta data
	  * data from Requestor/Supplier regarding who, what, when, where, how
	  * Technical in-team Subject Matter Expert for this workflow
	  * details about need for sampling time accuracy
	  * Support level
	  * Who to charge for work/load/issues



Copyright (C) 2016 Levon Karayan

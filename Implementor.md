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
	* Have standardized file naming that specifically avoids lexographic order to allow better performance
	* raw data should be ingested without any transformations
	* ingest date should be parameterized
	* ingest should probably include some amount of rolling load in case there was an issue
	* Schedule early in the work day for any data which is sensative to data collection sampling
	* typical use case is to alter table to add partions, msck can be run to assure all partitions are accounted for occassionally or overnight
	* Gzip for data that does not need to be splittable since it compresses better, snappy for when it does need to split at the cost of data size
	* Annotate Country of Origin of the data to fullfill compliance requirements
	* Automated Alerts
	  * Look for decreases in cumulative fields over days
	  * Linear Regression + Thresholds for low varience data ingests
	  * Look for misspellings
	  * Look for duplicate data
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
	* typical use case is to alter table to add partions, msck can be run to assure all partitions are accounted for occassionally or overnight
  * Workflows
    * Assure meta data
	  * data from Requestor/Supplier regarding who, what, when, where, how
	  * Technical in-team Subject Matter Expert for this workflow
	  * details about need for sampling time accuracy
	  * Support level
	  * Who to charge for work/load/issues

### Data Storage Layers

  * Layer 0 - Sensitive Data Only
     * Data as ingested
     * Accessible only via service accounts for ingest
     * Delete super sensitive data after ingest
  * Layer 1 - Schemaless/unstructured/semi-structured layer
     * Goals
	   * Communication checkpoint about where data is
	   * an option for really advanced users
	   * Make it accessible without schema
	   * Validate what they said they are going to send is what they sent
     * Notes
	   * no transformations other than security hash/encryption/homomorphic
	     * PII
		 * PCI
		 * etc...
	   * md5 or other checksum validation
	   * Pattern matchers for
	     * Credit card numbers
		 * social security numbers
		 * phone numbers
		 * street addresses
		 * email addresses
		 * high resolution GPS Coordinates
		 * IP Addresses
		 * First names & Last Names
	   * File format compliance validations
	     * csv, vs. tsv, parquet, avro, etc...
     * Risk
	   * end users will need to deal with all changes and unexpecte breakages
	   * poor performance
	   * system wide impact
	 * Persona
	   * Very strong Java, Scala, Python, R, AWS, Linux, Data skills
	   * Willing to deal with upstream data problems
  * Layer 2 - High Granular Queryable
     * Goals
	   * Address security
	   * Performance for querying
	   * Convert to schema-ized
     * Notes
	   * Source of truth
	   * Parquet format
	   * limited access only to people that understand risks of big data
	   * Partitioned by Ingest datetime
	   * Critical to backup this bucket above all
	   * Minimal if any Transformations
	   * Field level SPI/PII Encryption (hopefully done at source)
	   * Documentation from Requestor / Supplier
	   * Standardize Times here (be consistent)
	   * Should have AVDLs that represent data even if data is not stored as parquet/avro
	   * file format is valid
  * Layer 3 - Hard Business Rules
     * Quality - Parquet
	 * Notes
	   * Data Domain Alignment (Data Type Matching)
	   * Normalization
	   * System Column Computation
	   * Data Cleansing
	   * Profiling
	   * Partitioned better for query
	   * Aggregated / Cubed / Widened aka de-normalized
	   * Handles deletes and updates - Merge Pattern
	   * Should have AVDLs that represent data
  * Layer 4 - Multiple Data Sources Joined, soft business rules
     * Integrated
	 * Notes
	   * Any requirement that the business user states that changes the data or changes the meaning of the data
	     * The grain or interpretation
	   * Integrate data from multiple systems
	   * Model based on Data Vault Pattern 2.0
	   * Should have AVDLs that represent data
  * Layer 5 - Clean Reference Tables and Lookups
     * Reference
	 * Notes
	   * Conformed, Master & Reference Data
	   * Should have AVDLs that represent data
  * Layer X - Data Lab for users transient tables / views

### Shared Metadata

  * See Data Vault 2.0 overview
  * Attributes
    * *_sqn - Sequence
	  * The inertion order into the table
    * *_ldts - Load Date
	  * When the warehouse first saw the data
    * *_rsrc - Record Source
	  * System + App where the data originated
    * *_ledts - End of lifecycle
	  * Used for superceded records
  * Tables
    * Hubs - business keys
    * Links - Associations / Transactions
    * Satellites - Descriptors


Copyright (C) 2016 Levon Karayan

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

  * Layer 0 - Pre Sensitive Data Screen - Extract
     * Data as ingested (except if needs encrypted)
     * Accessible only via service accounts for ingest
     * Delete super sensitive data after ingest if necessary
     * Non-published staging area
     * "Deny unless" ruleset
     * Use source database encryption algorithm on the way into this bucket if possible
	 * {dev,qa,stage,prod}.{ds,LoB}.L0.{DOMAIN}
  * Layer 1 - Schemaless/unstructured/semi-structured layer - Loaded / Encrypted
     * Goals
	   * Communication checkpoint about where data is
	   * an option for really advanced users
	   * Make it accessible without schema
	   * Validate what they said they are going to send is what they sent
	   * Address security
     * Notes
	   * {dev,qa,stage,prod}.{ds,LoB}.L1.{DOMAIN}
	   * no transformations other than security hash/encryption/homomorphic
	     * PII
		 * PCI
		 * etc...
	   * md5 or other checksum validation iff available
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
	     * csv vs. tsv, parquet, avro, etc...
     * Risk of direct use
	   * end users will need to deal with all changes and unexpecte breakages
	   * very poor performance
	   * system wide impact of improper use of data
	   * Willing to deal with upstream data availablity problems
	   * Willing to deal with upstream data quality problems
	 * Persona
	   * Jane the Data Wizard (Data Scientist with programming skills)
	   * Very strong programming (beyond SQL) skills: Java, Scala, Python, R
	   * Very strong ELT skills: ingest, bandwidth
	   * Very strong operations skills: AWS, Linux, performance, stability
	 * Use Case
	   * Need data as soon as available
	   * Not sure if there will be an ongoing use of this data to warrent further work.
	   * status upate on the way to higher data layers
  * Layer 2 - High Granular Queryable - strict Transforms
     * Goals
	   * Performance for querying
	   * Convert to schema-ized
     * Notes
	   * {dev,qa,stage,prod}.{ds,LoB}.L2.{DOMAIN}
	   * Source of truth
	   * Parquet format
	   * limited access only to people that understand risks of big data
	   * Partitioned by Ingest datetime
	   * Critical to backup this bucket above all
	   * Minimal if any Transformations
	   * Field level SPI/PII Encryption (hopefully done at source)
	   * Documentation from Requestor / Supplier
	   * Standardize Times here (be consistent within the Datalake)
	     * All dates in YYYY-MM-dd format
	     * All times in UST
	     * 12/24 hour correctly to datetime object in 24h format
	   * Standardize units here
	   * Semantic views and data glossary
	   * Should have AVDLs that represent data even if data is not stored as parquet/avro
	   * Field level validations
	   * Data Domain Alignment (Data Type Matching)
	 * Persona
	   * Need to understand data to communicate higher level requirements
	   * Strong SQL skills in optimization.
  * Layer 3 - Hard Business Rules - normalization transforms
     * Quality
	 * Notes
	   * {dev,qa,stage,prod}.{ds,LoB}.L3.{DOMAIN}
	   * System Column Computation
	   * Data Cleansing
	   * Handles deletes and updates - Merge Pattern
	   * Normalization
	   * Foreign Keys / Dedupe / Explode logic standardized
	   * Profiling
	   * Partitioned better for query
  * Layer 4 - Multiple Data Sources Joined, soft business rules - widening transforms
     * Integrated
	 * Notes
	   * {dev,qa,stage,prod}.{ds,LoB}.L4.{DOMAIN}
	   * Any requirement that the business user states that changes the data or changes the meaning of the data
	     * The grain or interpretation
	   * Integrate data from multiple systems
	   * referential level validations
	   * Aggregated / Cubed / Widened aka de-normalized
	   * Model based on Data Vault Pattern 2.0
	   * Should have AVDLs that represent data
  * Layer 5 - Clean Reference Tables and Lookups
     * Reference
	 * Notes
	   * {dev,qa,stage,prod}.{ds,LoB}.L5.{DOMAIN}
	   * Conformed, Master & Reference Data
	   * Should have AVDLs that represent data
  * Layer X - Data Lab for users transient tables / views
	 * Notes
	   * adhoc.{ds,LoB}.lab.{DOMAIN}
	   * Not backed up
	   * may be lost
	   * For short term experimentation

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

### Maturity of Ingests
  * Manual
    * Data is assured not to have PCI, PII, Confidential Sensitive, Confidential
    * Data is loaded and made accessible to end user at Layer 1 or Layer 2
    * Data is Smoke tested before exposed to user
    * Data is Loaded into temp space
    * Access credentials are stored in data services Vault from hashicorp
  * Automated
    * SDLC
      * Git repository containing all code
      * Feature document with requirements and tech design created, code reviewed, and merged
      * Job is created in git repository to load data into sensible schema
	    * Job references environment for
		  * Processing Engine
		  * destination/S3 buckets
		  * source system info
		  * Hashicorp Vault host
		  * Alert Channel
		  * Phase (dev, qa, uat, stage, prod
	    * Job is parameterized for
		  * start_{date,hr,yr,month,etc..} it should start processing for (inclusive)
		  * end_{date,hr,yr,month,etc..} it should stop processing (inclusive)
      * if Job is an update, enhancement, bugfix, previous data is migrated
      * Job is smoke tested for functionality
      * Job is tested and validated via dev, qa, uat, prod
      * Job metadata of downstream job updated to include new job for lineage purposes
      * Jenkinsfile for continuous delivery
      * Jenkinsfile tested and validated
      * If the job is currently running in an enviornment that isn't the latest in-production cluster, then it must be upgraded.
    * AVDLs explaining data model, comments, documentation
      * Data stored as Parquet
      * Data model documentation created
	  * Data is annotated
	    * _uid (GUID) unique id added
	    * _sqn (Sequence) number added
	    * _ldts (Load) datetime UST added
	    * _rsrc (Resource) source system identifier added
	    * _exts (Expire) datetime UST added iff necessary
	    * Standardize Times here (be consistent within the Datalake)
	      * _All datetimes in UST if that is not the case, create an annotated column that contains the time in UST
	      * 12/24 hour correctly to datetime object in 24h format
        * Standardize units
      * POJO object library created of data model
      * Maven module that puts dependendency into a maven repository that the job depends on
    * Architecture
      * Data is retrieved from farthest accessible upstream point in-the-realm-of-possibility unless there is an exception
	  * Data is compressed via snappy
      * Partitions are reasonably sized
      * Files within partiion are reasonably sized
	  * All file parts have appropriate file extension
	  * Partitioned by Ingest datetime
	  * md5 or other checksum validation iff available
	  * control file asserted iff available
      * Full loads should come in under a different partition and the table pointer should be changed
	* Data quality
      * All cumulatives should be increasing
      * outputs follow naming standards for underlying *.parquet files and within metastore
  * Scheduled
    * Has been tested to have at least 5 cycles of scheduled frequency of success
    * Slack alerts have been set up to inform user (based on preference) start/success/fail/issues
    * Recovery job created that does only data validation without data movement on a different orchestration server
    * Recovery job is smoke tested for functionality
    * Recovery job is tested and validated
	* Alerting is setup if backups are inconsistant
    * Schedule is added to support the above job
    * No false alarms
  * Derived / Aggregated
    * Mock data static integration tests are created
	* derived job stores data in a different bucket
  * Validated
  * Monitored
  * Alertable
  * Seasoned
    * Backups are scheduled
    * Backups are validated
    * Restores are tested and validated
    * Secondary orchestration server validation to validate the first

Copyright (C) 2016 Levon Karayan

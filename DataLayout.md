# data-integration

## Implementor Guidelines


### Data Storage Layers

There are many reasons why we want to separate our data into layers.
  * Blob storage providors might need to partition the data, and we could have scalability problems if we don't help them avoid skew.
  * The system impact (load, stability) of using the data at a specific layer could be coursely identified
  * The refinement of data for analyst usability and capability could be coursely identified
  * The backup tolerance can be coursely identified per layer
  * The team can inherit flexibility to create silo datamarts or specialized ELT easier
  * The standardized naming scheme can help orient data engineers and data analysts
  * Isolating data by enviroment could prevent cross-contamination

Here is an initial proposal

  * Layer 0 - Pre Sensitive Data Screen - Extract
     * Data as ingested (except if needs encrypted)
     * Accessible only via service accounts for ingest
     * Delete super sensitive data after ingest if necessary
     * Non-published staging area
     * "Deny unless" ruleset
     * Use source database encryption algorithm on the way into this bucket if possible
     * Partitioned by date time of ingest foo/DATE=2017-02-30/...
     * {dev,qa,stage,prod}.{ds,LoB}.l0.{DOMAIN}
  * Layer 1 - Schemaless/unstructured/semi-structured layer - Loaded / Encrypted
     * Goals
       * Communication checkpoint about where data is
       * an option for really advanced users
       * Make it accessible without schema
       * Validate what they said they are going to send is what they sent
       * Address security
     * Notes
       * {dev,qa,stage,prod}.{ds,LoB}.l1.{DOMAIN}
       * no transformations other than security hash/encryption/homomorphic
         * PII
         * PCI
         * etc...
       * md5 or other checksum validation iff available
       * Partitioned by Ingest datetime
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
       * {dev,qa,stage,prod}.{ds,LoB}.l2.{DOMAIN}
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
       * {dev,qa,stage,prod}.{ds,LoB}.l3.{DOMAIN}
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
       * {dev,qa,stage,prod}.{ds,LoB}.l4.{DOMAIN}
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
       * {dev,qa,stage,prod}.{ds,LoB}.l5.{DOMAIN}
       * Conformed, Master & Reference Data
       * Should have AVDLs that represent data
  * Layer X - Data Lab for users transient tables / views
     * Notes
       * adhoc.{ds,LoB}.lab.{DOMAIN}
       * Not backed up
       * may be lost
       * For short term experimentation

<!--- vim: set expandtab tabstop=2 shiftwidth=2 softtabstop=2: -->

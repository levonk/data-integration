# data-integration

## Integration Paradigms

There are two Integration Paradigms that we support.   The first is Stream Integration and the second is Batch Integration.  We find our business increasingly insisting on real time data, and since the batch case can be thought of as a simplified streaming case we prefer streaming.    However, batch is by far the most prevelant integration.


### Data Questions

#### Data Questions (high level)
 * What options are there to ingest the data?
   * Streaming
   * Batch
 * What is the canonical / common name of the data set/product we are engaging you on?
 * Are there other similar datasets/products or "addons" that we should be aware of to avoid confusing things in our discussions?
 * Describe the Dataset
 * Is there any of the following in the data
    * Payment Card Industry (PCI) data
      * What Merchant Level is the data? - https://www.pcicomplianceguide.org/pci-faqs-2/#4
        * Level 1 - 6M+ Vendors or Visa designated Level 1 merchants
        * Level 2 - 1-6M transaction per year
        * Level 3 - 20k-1M e-commerce merchants processing transactions per year
        * Level 4 - Fewer than 20k transaction e-commerce transactions or Fewer than 1M other transactions.
   * HIPPA compliant data
   * Private Financial Information
   * Personally Identifiable Information (PII) (circle all that are appropriate)
     * Individuals below the age of 13
     * registered users
     * unregistered users
     * US users
     * International users
    * Video rental or streaming information
    * Non-public Intellectual Property Infomration
    * Other sensitive data
    * Public Data 

#### Data Questions (Transport level)
  * Transport protocol (circle all that apply, assuming all data is available on all selected transports)
    * websockets
    * Amazon S3 http://docs.aws.amazon.com/AmazonS3/latest/dev/example-walkthroughs-managing-access-example2.html
    * SFTP
    * Google Blob Storage
    * REST
    * SOAP
    * Email
    * IM
    * Other?  What?
 * Does the vendor Push the data or requires us to Pull the data?
 * How will the vendor trigger our systems to process the data?
   * API endpoint
   * AWS SNS Message
   * Push the data
   * Other? What?
 * What if any Rate Limits are there?
 * What is the server name?
 * What is the server port?
 * What is the Account/User Name?
 * What is the authentication method?
   * Oauth 1.0
   * Oauth 2.0
   * username / password
   * private / public key
   * Basic Auth
 * Is access locked down by IP?


#### Data Questions (Dataset level)
  * Does the Data need to be a point in time snapshot?  
    * Do we have to pull the data at the same time each day to prevent erroneous trends?
  * How often is data updated?
    * realtime <50ms
    * near-realtime 50ms-15 minutes
    * Hourly
    * Bi-Hourly
    * Daily
    * Weekly
    * Monthly
    * Quarterly
    * Yearly
    * Other? What?
 * Approximate size in bytes of the data transfer:
 * Approximate size in records of the data transfer:
 * Approximate number of files in the data transfer:

#### Data Questions (Answer for each File)
 * What is the file & directory name format? 
   * YYYY/MM/DD/YYYMMDDHHmmss<DATA_NAME>.*
   * Other? What?
 * What is the format of the file being transfered?
    * Avro wapped Parquet
    * Avro
    * BSON
    * JSON
    * RDF
    * XML
    * serialized protobufs
    * TSV
    * CSV (please no)
      * Excel is a notoriously bad tool  https://support.microsoft.com/en-us/kb/291296
      * Will fields be properly quoted?
    * XLSX (please no)
 * Is the file archived?
   * Not Archived
   * Tar
   * Zip
   * other
 * Is the file compressed?
   * gzip
   * bzip2
   * zip
   * squash
   * lzh
   * other
 * Describe (format & count) any footer/header rows in the file
 * Describe any validation or control records present in the file
 * Supply the schema file for the dataset
   * AVSC http://avro.apache.org/docs/current/spec.html
   * RDFS https://www.w3.org/TR/rdf-schema/
   * JSON-LD http://json-ld.org/
   * JSON Schema http://json-schema.org/
   * SQL Schema
   * Sample CSV
* Do you have a Data Glossary or other documentation that can help us understand the data within the schema?
* Type of Integration
  * Full Load
  * Incremental
    * Describe how you handle
      * New records
      * Updated Records
      * Deleted records
* Describe the reconsilation/restatement process.
* What CODEC is the file encoded in?
  * UTF8 w/ BOM
  * UTF8
  * UTF16 w/ BOM
  * UTF16
  * ISO9660 (no please)
  * Other? What?
* Encryption
  * encrypted first then compressed/archived
  * archived/compressed first then encrypted
  * None
* What validations are expected on the data?
  * Domain Integrity Constraints
    * Not null
    * Check
  * Entity integrity Constraints
    * Unique
    * Primary Key
  * Referential Integrity Constraints
    * Foreign Key
  * High / Low water record thresholds
  * High / Low water field thresholds
  * Date Formats, Timezones
  * Mean/Avg/Variance data and period WoW, (MoM, Daily, etc..)
  * Validation against control file
  * CRC Validations
    * MD5
    * SHA1
    * SHA256
    * Other? What?
  * Chance of duplicated records?
  * What are cumulative numbers that are not expected to decrease.


#### Data Questions (Detailed level, repeat for each field as appropriate)
  * Type of Data
    * Event Data
    * State Data
    * Session Data
    * Aggregated Data
      * hourly aggregated
      * daily aggregated
      * weekly aggregated
      * monthly aggregated
      * quarterly aggregated
  * Primary Keys and unique keys
    * Please specify strategy
  * Date/Time Formats
    * UTC
    * TimeZone
    * DST handling (please no)
      * How do you handle
        * Gaining an hour
        * Losing an hour
  * Fields & Units
    * Do field columns include unit specifier
    * What units is the column in
    * Can we ever except NULLs and how are they represetnted?
    * Can we ever except blanks and how are they represented?
    * Is there a defaul?
  * Field Type
    * free form
    * ordinal
    * categorical
      * Are leading zeros important (e.g. zipcodes)
    * numeric
      * incremental / delta e.g. + something or - something
    * GUID
  * Field Data types (not necessary if this is schema)
    * unsigned int
    * signed long
    * currency
    * etc...
  * Currency
    * Is it adjusted in any way inflation, etc..
    * Does it include VAT, taxes, etc...
    * Is it Gross or Net
  * Is the field derived and how?
  * Is the field master data and what is it's source/lineage?
    * What standard?
    * Where is it sourced from?
    * How is it refreshed?
  * Is there any content like test data we should filter?

### Data Supplier Questions
* What Service Level Agreement (SLA) is provided with the data?
  * What are the company Holidays and their expected date ranges?
  * Support Times
   * Next business day
   * 8/5/249 - Business Hours
   * 24/5/249 - Business Days
   * 8/7/365 - Waking Hours
   * 24/7/365 - All Hours
  * Time to first response
  * Time to escalation
* What validations is performed on the data before being dropped off?
* Will you inform us before?
  * Expected non-delivery
  * Expected delivery changes
  * Expected data schema changes
  * Expected data quantity changes
* Supplier Company
  * Background
    * Years in business:
    * Years in data supply business:
    * Years supplying this data:
    * Number of large customers consuming this data:
    * DUNS Number:
    * URL:
    * Front Office Number:
    * LinkedIn.com:
* Our Account Information
  * How do you refer to our account canonically / commonly?
  * How do you refer to our account in your systems?
* The Adminitrative Contact of the integration? (accounts payable, legal, escalation, etc..)
   * Contact Information
     * Name:
     * Title:
     * Company:
     * Email:
     * Phone:
     * IM:
     * LinkedIn.com:
* The Sales Contact of the integration?
   * Contact Information
     * Name:
     * Title:
     * Company:
     * Email:
     * Phone:
     * IM:
     * LinkedIn.com:
* The Primary Technical Subject Matter Expert (SME) of the integration? (Capable of debugging the integration for data quality or data availability)
   * Contact Information
     * Name:
     * Title:
     * Company:
     * Email:
     * Phone:
     * IM:
     * LinkedIn.com:
   * How are we to contact the Technical SME
     * inaccurate, broken or missing data via  (circle one or more)
       * IM
       * Email
       * Phone
       * Incident Management system: URL
     * non-emergency questions via  (circle one or more)
       * None
       * IM
       * Email
       * Phone
       * Incident Management system: URL
* The Secondary Technical Subject Matter Expert (SME) of the integration? (Capable of debugging the integration for data quality or data availability)
   * Contact Information
     * Name:
     * Title:
     * Company:
     * Email:
     * Phone:
     * IM:
     * LinkedIn.com:
   * How are we to contact the Technical SME
     * inaccurate, broken or missing data via  (circle one or more)
       * IM
       * Email
       * Phone
       * Incident Management system: URL
     * non-emergency questions via  (circle one or more)
       * None
       * IM
       * Email
       * Phone
       * Incident Management system: URL



Copyright (C) 2016 Levon Karayan
<!--- vim: set expandtab tabstop=2 shiftwidth=2 softtabstop=2: -->

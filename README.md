# data-integration

## Integration Paradigms

There are two Integration Paradigms that we support.   The first is Stream Integration and the second is Batch Integration.  We find our business increasingly insisting on real time data, and since the batch case can be thought of as a simplified streaming case we prefer streaming.    However, batch is by far the most prevelant integration.



### Stream Integrations

#### File/Blob Formats in order of preference

Apache Avro




### Batch Integrations

#### File Formats in order of preference

Apache Avro wrapping Parquet

##### Share via Amazon S3 Buckets

Please reference the documentation at:  http://docs.aws.amazon.com/AmazonS3/latest/dev/example-walkthroughs-managing-access-example2.html

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
    * Amazon S3
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
   * AVSC
   * SQL Schema
   * Sample CSV
* Describe how you handle record deletions. 
* Describe the reconsilation/restatement process.
* What CODEC is the file encoded in?
  * UTF8 w/ BOM
  * UTF8
  * UTF16 w/ BOM
  * UTF16
  * ISO9660 (no please)
  * Other? What?


#### Data Questions (Detailed level)

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


### Business Questions

## Business Questions which are optional

 * When do you need the data to which phase (see the required section) of completion?
 * What are critical periods for data availablity
   * Monday's 
   * Tuesday's
   * Wednesday's
   * Thursday's
   * Friday's
   * Work Week
   * End-of-month
   * End-of-quarter
   * End of fiscal year
   * End of calendar year
 * What Service Level Agreements (SLA) will you be paying for? (Note: we're limited from downstream providors)
   * Backlog / when it's conveniant (default)
   * Next business day
   * 8/5/249 - Business Hours
   * 24/5/249 - Business Days
   * 8/7/365 - Waking Hours
   * 24/7/365 - All Hours
 * Agreement Information
   * Statement of Work identifier / doc number
   * Statement of Work Term
     * Start date
     * End date
     * Renewal/renogotiate/change Lead time
   * Is the Provenance/Rights of the data clear within the SOW ?
     * When to purge the data? etc...
   * Can you supply the SOW/MSA to the Data Services team?
   * Legal Contact
     * Name
     * Title
     * Email
     * Phone
     * IM
* What validations are expected on the data?
  * High / Low water record thresholds
  * High / Low water field thresholds
  * Date Formats, Timezones
  * Mean/Avg/Variance data and periods
* The Administrative Contact of the integration (the person paying the invoices, assuring paperwork is cleared)
  * Contact Information
    * Name:
    * Title:
    * Email:
    * Phone:
    * IM:
    * LinkedIn.com:
 * The Business "owner" of the integration? (typically the lead of the group)
   * Contact Information
     * Name
     * Title
     * Email
     * Phone
     * IM
     * LinkedIn.com:
   * What is your interest in being made aware of
     * data source changes via (circle one or more)
       * None
       * IM
       * Email
     * data availability via (circle one or more)
       * None
       * IM
       * Email
     * data validation via (circle one or more)
       * None
       * IM
       * Email
     * data accesses via  (circle one or more)
       * None
       * IM
       * Email
       * Phone

## Business Questions which are *required*

 * What is the Group requesting the integration?
 * What is the common or canonical name for this dataset?
 * Where do you wish to access the data from?
 * What is in the data?
 * What is the business purpose of the integration?
 * Will the data be used for
   * Targeted Advertising
   * Direct Marketing
   * Content Personalization
   * Analytics
   * Major Financial decisions
   * Major business strategy decisions
   * Something else?
 * Phased Delivery
   * manual
   * automated
   * scheduled
     * This is typically where we stop work, unless more is requested.
   * Derived / Aggregated
   * validated
   * monitored
   * alertable
   * seasoned
* The Business Subject Matter Expert (SME) of the integration? (day-to-day user of the data, probably the person filling out this form)
   * Contact Information
     * Name:
     * Title:
     * Email:
     * Phone:
     * IM:
     * LinkedIn.com:
   * What is your interest in being made aware of
     * data source changes via  (circle one or more)
       * None
       * IM
       * Email
     * data availability via  (circle one or more)
       * None
       * IM
       * Email
     * data validation via  (circle one or more)
       * None
       * IM
       * Email
     * data accesses via  (circle one or more)
       * None
       * IM
       * Email
       * Phone
  



Copyright (C) 2016 Levon Karayan

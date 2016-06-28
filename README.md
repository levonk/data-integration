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


### Vendor Questions


### Business Questions

 * What is the Group requesting the integration?
 * What is the common or canonical name for this dataset?
 * What is in the data?
 * What is the business purpose of the integration?
 * Is there any of the following in the data
   * Payment Card Industry (PCI) data
     * What Merchant Level is the data? - https://www.pcicomplianceguide.org/pci-faqs-2/#4
       * Level 1 - 6M+ Vendors or Visa designated Level 1 merchants
       * Level 2 - 1-6M transaction per year
       * Level 3 - 20k-1M e-commerce merchants processing transactions per year
       * Level 4 - Fewer than 20k transaction e-commerce transactions or Fewer than 1M other transactions.
   * HIPPA compliant data
   * Child data
   * Personally Identifiable Information (PII)
     * registered users
     * unregistered users
     * US users
     * International users
    * Private Financial Information
    * Non-public Intellectual Property Infomration
    * Other sensitive data
    * Public Data 
 * Will the data be used for
   * Targeted Advertising
   * Direct Marketing
   * Content Personalization
   * Analytics
   * Major Financial decisions
   * Major business strategy decisions
 * Agreement Information
   * Statement of Work identifier / doc number
   * Statement of Work Term
     * Start date
     * End date
     * Renewal
   * Legal Contact
     * Name
     * Title
     * Email
     * Phone
     * IM
 * Phased Delivery
   * manual
   * automated
   * scheduled
     * This is typically where we stop work, unless more is requested.
   * validated
   * monitored
   * alertable
   * seasoned
 * What Service Level Agreements (SLA) will you be paying for? (Note: we're limited from downstream providors)
  * Backlog / when it's conveniant 
  * Next business day
  * 8/5/249 - Business Hours
  * 24/5/249 - Business Days
  * 8/7/365 - Waking Hours
  * 24/7/365 - All Hours
 * The Business "owner" of the integration? (typically the lead of the group)
   * Contact Information
     * Name
     * Title
     * Email
     * Phone
     * IM
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
* The Business Subject Matter Expert (SME) of the integration? (day-to-day user of the data, probably the person filling out this form)
   * Contact Information
     * Name:
     * Title:
     * Email:
     * Phone:
     * IM:
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

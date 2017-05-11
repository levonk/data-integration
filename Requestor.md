# data-integration - Requestor Questions

## Requestor Questions which are *required*
NOTE: required with exceptions to be discussed.

 * What is the Group requesting the integration?
 * Which groups would require access to the data? 
 * Would you want additional applied security to the data? 
 * What is the common or canonical name for this dataset?
 * Where do you wish to access the data from? (Domain Names of the tooling)
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
 * Do you need a schema exposed? - to make SQL queries
   * yes
   * no
 * Phased Delivery
   * manual - You are not sure whether you want a repeat load
   * automated - you need a reproducable data load but there is no schedule
   * scheduled - you want the automated load to happen on a schedule and will help the team improve the reliability as issues are uncovered
   * Derived / Aggregated - You want reasonable transformations of the data to support reporting
   * validated - You know some validations that need to occur on the data before you rely on it
   * monitored - you want history about how the data load performs as far as reliability and status
   * alertable - you need a higher than next business day SLA
   * seasoned - you need a hypercare period that will assure high reliablity on the data feed without a lot of attention
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
  * Who can we go through for the upstream providor of this data to fill out additional information?
    * Contact Information
      * Name:
      * Supplier/Vendor:
      * Email:
      * Phone:
      * IM:


## Requestor Questions which are optional

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
   * Other: _______________________________________________________

 * For your critical reporting, what is the earliest we can grab the data?
   * NOTE: This is pertinant because this is when we will try to ingest the data to permit recovery time should there be any problems.  It identifies the "staleness" of the data you can tolerate.
 * What Service Level Agreements (SLA) will you be paying for? (Note: we're limited by upstream providors)
   * Backlog / when it's conveniant (default)
   * Next business day
   * 8/5/249 - Business Hours
   * 24/5/249 - Business Days
   * 8/7/365 - Waking Hours
   * 24/7/365 - All Hours
   * Other: _______________________________________________________
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
		* Mean/Avg/Variance data and period WoW, (MoM, Daily, etc..)
	* What is the data retention policy we should enforce? (days, weeks, months, years, none)
		* On the raw data 
		* On the derived data
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


Copyright (C) 2016 Levon Karayan
<!--- vim: set expandtab tabstop=2 shiftwidth=2 softtabstop=2: -->

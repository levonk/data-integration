# Data Products

A stong Data Services team has a comprehensive capability set.   These are some of the outputs from the team.

  * [Workflows](#data-workflows) - multi-task processes to manipulate data.
  * [Components](#data-components) - tools to support a task in a workflow
  * [Orchestration](#data-orchestration) - a mechanisim to trigger or schedule workflows.
  * [Integration](#data-integration) - a platform to support moving data around
  * [Persistence](#data-persistence) - a platform to store data
  * [Analysis](#data-analysis) - an effort to answer a question using the above data and platforms.
  * [Applications](#data-applications) - a more refined implementation of a tool, process or analysis.
  * [Practices](#data-practices) - processes that support data teams or the customers of data services.

##  Data Workflows
This is the bulk of what the team does.  Within this repository are questionaires for the various players involved in sourcing the data.   Often times these are stiched together data tasks that are involved in ingestion, loading or transformation (ELT).   The ELT is often supported by packaged [components](#data-components), run through an [orchestration](#data-orchestration) service against a [persistence](#data-persistence) engine or a [data product](#data-product)

The challenge with this work is that the quality of the source data and up stream delivery efforts vary drastically between the different data sources.
	* Examples
      * Double Click Ingest
      * Omniture Ingest

##  Data Components
    * Sqoop Ingestor
    * (S)FTP Ingestor
    * Parquet Mapper

##  Data Orchestration
	  * Batch Processes
	    * Azkaban

##  Data Integration
	  * Message Bus
	    * Confluent platform

##  Data Persistence
Some of the challenges associated with this function is the unpredictable nature of the queries coming into an analytical system and the varied skillsets of the users.
      * Data Lakes
        * Apache Spark
      * Data Warehouses
        * Teradata
      * Data Marts
        * PostgreSQL

##  Data Analysis

	  * Adhoc Notebooks
	    * Functions
	      * Collaborative working
	      * Data Cleaning
	      * Machine Learning
	      * Clustering
	      * Classification
	      * Regression
	      * Data Cleaning
	    * Platform
	      * Zeppelin
	    * Examples
		  * Microdemographics from subset of tweets
	  * Graphical reports & Dashboards
	    * Functions
	      * visualization guidence
	      * leightweight regressions
	      * limited computed fields
	      * visualization
		  * Create data extracts
	    * Platform
	      * Tableau
	    * Examples
		  * Comparison Report
		  * Advertising Dashboard
	  * Pixel perfect or tabular reports & dashboards
	    * Functions
		  * Print Reports
		  * Override data in Excel
		  * Have presentations updated
		  * Create mini cubes
	    * Platform
		  * MicroStrategy
	    * Examples
		  * record of transactions

##  Data Applications
    * Tools
	  * RDBMS Mapper
	  * Google Sheet Ingestor
	  * DamFingers
	  * cd.wdsds.net
	  * Maven Archetypes
    * Services
	  * URLShortener
	  * Search
	  * Recommender
	  * Merchandiser
    * User Facing
	  * DataPortal - Central user interface to access the rest of the tools
	  * DataLink - Record Linking product that allows a person through a user interface to approve fuzzy matching assessments
	  * CRM - Proposed customer relationship management system

## Data Practices
    * Documentation
    * Processes
    * Training
    * Advice / Consulting

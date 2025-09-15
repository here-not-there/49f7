# bigE learning notes

#PART I

BIG DATA

- Data Transformation
  - AWS course
- Data Modelling Methodology - Data Warehouse - Data Lake
  - bigE **Data Modeling Basics**
- Data Modelling Approaches - ER - Dimensional
  - bigE **Data Modeling Basics** 
  - Claude
  - AWS course
- CI/CD
  - bigE CI/CD overview

- Leftovers
  - bigE Jenkins Overview

White spots:
  software development methodology
  cloud overview (including Containers)


# CI/CD

## **DevOps**

What it does:
- emphasizes collaboration and communication among IT professionals
- automates software delivery
- automates infrastructure changes.
- build, test, release

DevOps benefits:

- transparent communication
- continuous feedback
- faster delivery
- improved quality
- lower costs
- faster resolution of issues
- higher overall productivity
  
**Core practices**

- automation
- version control
- continuous integration
- continuous delivery
- configuration management
- monitoring and logging
- communication
- collaboration

## **Continuous Integration**

- frequents merge of smaller code updates into a central repository or version control system
- automated development and testing are performed
- aims
    - to find and manage bugs faster,
    - improve software quality,
    - reduce the time needed to validate and release changes
    - **create deployable artifact**

- Ends with publishing vierified artifact
  - artifact repository
    - storage
    - mangement / version control

## **Continuous Delivery**

Continuous Delivery 
- extends Continuous Integration
- deploy to testing environment & test
- deploy to staging environment & test
- create release candidate
- release

Staging environment
- a pre-production environment that closely mirrors production setup
- used as the final testing phase before deploying code to live users

Test coverage is as complete as possible, including:
- unit tests
- acceptance tests
- performance / stability tests

Continuous deployment
- automation of release to production

CI/CD pipeline
- a set of steps that must be followed to deliver a new version of the software

## **Infrastructure as a Code**

- code configurations are reused
- instant deployments
- deploy setups are stored in version control
- rollbacks are fast and simple

### CI/CD cons:

- more processes—more complication
- more time to create good tests and automation
- more work to define pipelines
- requires constant support

## ETL / ELT pipelines

### Extract

- Retrieve data from source systems
    - db, CRMs, files, API
    - batching or streaming
- ensure data integrity

### Transform

- convert data to format suitable for target warehouse (data lake: on demand)
- cleansing (duplicates, errors)
- enrichment (adding from other sources)
- handling missing data
- format changes (types conversion, date formatting)
- aggregations or computations
- encoding or decoding

### Load

like the opposite of extract

- move data to another target
    - batching or streaming
- ensure integrity

### Managing pipelines

- AWS Glue
- Orchestration services
    - EventBridge
    - Amazon Managed Workflows for Apache Airflow
    AWS Step Functions
    - Lambda
    - Glue Workflows

## Data Sources

### JDBC

Java Database Connectivity - Java related

### ODBC

Open Database Connectivity - language independent

### Raw logs

### APIs

### Streams (Kafka etc)

## Common Data Formats

### CSV

human readable

import-export (universal)

handling - sequel-based, languages (Python), other

### JSON

js object notation

common for web data / configuration / any other nested structures

human readable

handling - languages, No-SQL

### Avro

binary

data + schema
good for big data

good when schema evolution expected

efficient serialization for data transport between systems

handling: Hadoop (part of it), Kafka, Spark, Flink

### Avro Main Concepts

**Schema-Based Serialization:**
Avro uses JSON schemas to define the structure of data before serialization. These schemas specify field names, data types, and constraints, ensuring data consistency and enabling validation during read/write operations.

**Compact Binary Format:**
Data is serialized into a space-efficient binary format that's smaller than JSON or XML. The schema is stored separately from the data, reducing redundancy since field names aren't repeated in every record.

**Schema Evolution:**
One of Avro's key strengths is its support for schema evolution - the ability to modify schemas over time while maintaining compatibility with existing data. This is crucial for long-term data storage and system evolution.

### Parquet

columnar storage format optimized for analytics
efficient compression and encoding

good for analytical systems
good for distributed systems (split things out)

handling: Hadoop, Spark, Hive, Impala, Redshift Spectrum

### Data Modelling Approaches

database

**organized collection** of dat stored and accessed electronically from a computer system

Non-relational database 

storage model optimized for a specific type of data

- Document type: Azure Cosmos DB, Mongo DB
- Columnar type: Cassandra, HBase
- Key/value type: Redis, Azure Table storage
- Time series type: Azure Time Series Insights
- Object type: Azure Blob/File Storage, Azure Data Lake
- External index type: Azure Search
- Graph type: Azure Cosmos DB Gremlin, GraphDB

Non-relational ≠ NoSQL 

Modern NoSQL databases are minimizing the gap with relational databases

Relational DBMS 

stores data in tables and uses SQL 

can be either operational or analytical, based on the needs the DBMS serves

- An operational database is used when you need data to be organized quickly
    - is of the OLTP kind
    - can create or update a lot of data in real time
    - usually transactional, row-based, and table-oriented
    - Examples: Oracle, MS SQL Server, DB2, MySQL
- An analytical database
    - is of the OLAP kind
    - used when you need to analyze data, build graphics, etc.
    - supports massively parallel processing (MPP) and columnar storage
    - Examples: Snowflake, BigQuery, Spectrum Redshift, Oracle Exadata, Teradata, IBM Netezza

Database management system (DBMS)

software that interacts with end users, applications, and the relational database itself to capture and analyze data

### ER

- entity-based
- ‘entity-relationship’

An entity is any identifiable object that can be differentiated from others and the information that needs to be stored in the database. 

A relationship is a logical rule by which entities relate to each other. 

**3NF** 

form of ER modeling

part of the technique for normalizing database design

NF helps reduce repetitive data and ensures data is stored logically

involves three basic concepts: 

entities, 

attributes, 

and the relationships between them

is more related to building operational data storage

### ER Design Process

**Requirements Analysis:**
what data needs to be stored and how it will be used. 

understanding business processes

user needs

data sources

**Conceptual Design:**
high-level ER diagram -  the conceptual schema

focus on business logic and data relationships

**Logical Design:**
a detailed logical schema

intended for: architects, business analysts

entities + attributes + keys

**Physical Design:**
actual database and tables

intended for: architects, developers

naming conventions

normalization rules

data types

full constraints

performance optimization

indexing strategies

platform-specific features

roles

## Relationship Types and Cardinality

**One-to-One (1:1):**
Each instance of Entity A relates to exactly one instance of Entity B, and vice versa. Example: Employee to Employee_Profile, where each employee has exactly one detailed profile record.

**One-to-Many (1:M):**
One instance of Entity A can relate to multiple instances of Entity B, but each B instance relates to only one A instance. Example: Customer to Orders - one customer can place multiple orders, but each order belongs to one customer.

**Many-to-Many (M:M):**
Multiple instances of Entity A can relate to multiple instances of Entity B. Example: Students and Courses - students can enroll in multiple courses, and courses can have multiple students. This requires a junction table in implementation.

## ER Diagram Notation

ER diagrams use standardized symbols to visualize the model:

- **Rectangles** represent entities
- **Ovals** represent attributes
- **Diamonds** represent relationships
- **Lines** connect entities to relationships and attributes
- **Underlined attributes** indicate primary keys

Different notation styles exist (Chen, Crow's Foot, UML), but all convey the same fundamental concepts.

### Dimensional

- facts-based
- schema patterns: star / snowflake / galaxy
    - central table: **facts (main business value)**
    - peripheral: **dimensions** (descriptions of facts’ columns)
- denormalization
    - more intuitive from business perspective
    - avoiding multiple joins
- read performance is prioritized over write efficiency
- supports OLAP operations
    - drilling down
    - rolling up
    - slicing data across different dimensions

To build a dimensional model, you need to:

1. Select a business process
    1. what you are going to measure with the data you store. 
    2. The business process will determine the grain, facts, and dimensions.
2. Determine the grain, or the level of detail, to see what a row in the fact table will represent
    1. e.g., product delivery information by location by day.
3. Identify the dimensions (product, delivery, location, time, etc.)
    1. they describe where all additional/supportive data should be stored.
4. Identify facts, or the numerical results of the business process, which is an observable event (e.g., delivery by product/location/time).

The dimension table usually contains one descriptive field and a surrogate key for unique identification within the database. 

Dimensional tables serve three primary functions:

- filtering
- grouping
- labeling

Data growth in the dimensional table must be insignificant compared to fact tables. 

Types of dimensions

Conformed

Several facts can refer to this type of dimension using the same key with the same meaning—for example, the Date dimension or PostOffices dimension shared across at least two fact tables.

Junk

This type of dimension combines attributes of the same data type into one numbered set. If the attributes do not belong to any dimension, you can store them in one junk dimension. These attributes can be a collection of random transactional codes, flags, and/or text attributes.

Degenerate

This is a dimension key that often provides business value, like ClaimID, OrderID, etc. It is stored in the fact table as it doesn’t have attributes, and you can use it to organize groupings in the fact table directly.

Role-playing

This type of dimension is used for many facts, but with a different meaning. For example, the date dimension is used as a reference to dates with different meanings (roles) for the fact like OrderDate, ShipDate, or CloseDate.

SCD

Data in dimensional tables can change with time. Sometimes these changes may happen slowly and unpredictably. You will often need to track such changes in attributes inside dimensional tables to report historical data. Dimensions with such data are called slowly changing dimensions (SCDs). There are five types of SCDs. When implementing an SCD, you add the dimension’s attribute value for a given date.

SCD Type 0 

- the starting point. No changes are applied to the existing attributes of the dimension; only new records are added, so no history is stored or tracked in such a case for one attribute, e.g., DateOfBirth.

Key features:

- Type 0 applies to most date dimension attributes.
- The dimension attribute value never changes, so facts in the fact table are always grouped by this original value, and the attribute does not have a history, for example, names of countries and continents.
- Natural keys are used in type 0 dimensions.
- You can add new rows while keeping existing rows unchanged.

An example of a type 0 dimension is the date dimension.

SCD Type 1 

overwrites the old value with the new one in the same record to track the current state. No history is stored here either.

SCD type 2 

adds a new record. Usually Start Date, End Date, and Is Current Flag are used to identify old and new records. You may change the ID in this case. If you do, place the new one in the corresponding fact table. 

You will have two IDs—the old and the new. The old ID will still be constrained to the End Date. Please note that if the ID changes, you will need some other unique identifier for the row to track the history of the attribute’s changes. It would be great to use Customer Name in this case. However, you should avoid changing the Customer ID to maintain transparency.

SCD type 3 

uses an additional column to store the previous value or initial value. Type 3 stores only two values for the same attribute.

SCD type 4 

is a combination of types 1 and 2 that uses a historical table. In this type, the main dimension contains the current state only. The historical table contains a history of all the changes. For example, the fact table references the main dimension for query productivity. In this case, you need some historical information, so you add the history table to the query.

SCD type 6 

is a combination of types 1, 2, and 3.

Types of Fact Tables (names are self-explaining):

Transactional
Accumulating Snapshot
Periodic Snapshot
Factless

Factless fact tables do not contain any measurable facts associated with the transaction. Usually, this is a simple collection of dimensional keys.

**Facts**

A fact is a piece of quantitative information like sales price

types

additive
non-additive
semi-additive (additive for some dimensions)

The precision of data for facts that need to be measured determines **the granularity of fact tables.** For example, you need to store information about sales every day. Price quotes, however, are updated monthly, quarterly, or yearly. In this case, the Date–Time dimension must contain appropriate levels of granularity—at the day, month, quarter, or year levels. The fact table should have the same level of granularity. In some cases, you may not need to store every sale.

**Dimensional Models, Hadoop, and Big Data**

!!! Examples

1. Hadoop uses SCD type 2. As HDFS is immutable, you are adding more and more records to store the most recent value for the field while leaving all the previous values as well.

To efficiently query the most recent value, here are a few tips and tricks:

- Create a representation layer using views and windowing functions that retrieve the required info.
- Run a compaction service in the background that recreates the latest state.
- Use mutable storage such as HBase for dimensional tables to federate queries across the two types of storage.
1. When working with two or more large tables in Hadoop, you must JOIN them just like you would typically do with the entities in the relational model by the PKs, which join the rows based on relationship cardinality. JOIN operation of large tables is usually expensive as data on HDFS is split into big chunks and distributed across the nodes on the cluster. Use denormalization to reduce the spread of data across the network. You can extract data as-is from storage and join the records at run time as well.

## Normalization

The database is considered normalized if it reaches at least the 3NF stage.

**1NF**

- Each attribute in each row of the table is atomic.
- There are no repeating rows in the table—each row is unique.
- Attributes and rows are not sorted.

2NF

no columns are partially dependent on the composite primary key

3NF

every non-prime attribute in the table is dependent on the primary key non-transitively

3.5NF = Boyce-Codd normal form—**BCNF**

4,5,6 NF

## Which model when

### **3NF**

- great for storing operational data for ERP and CRM
- typically very fast
- used for controlling and running fundamental business tasks
- great for relatively simple queries and small result sets
- supports incremental loads thanks to easy delta detection between the source system and the version table
- great for DML (INSERT, UPDATE, DELETE, MERGE) operations

### **Dimensional Modeling**

- great for retaining consistency when consolidating disparate data from multiple sources into DWH
- used for planning, problem solving, and decision support
- usually denormalized with fewer tables than in source OLTP
- contains historical data for a long period
- supports incremental loads thanks to easy delta detection between the source system and the dimension table
- great for SELECT operations




## CLoud Overview

**cloud** 
  abstracting, pooling, and sharing
  computing resources
    servers, switches, routers, operating systems, and security software
  across a network of devices
  on or off the premises
  typically, with higher-level services
    analytical
    recovery etc

mixture of technologies
  operating system
  management platform
  APIs

Benefits
  cost efficiency
  scalability
    vertical scaling
      increasing the size of each resource
    horizontal scaling
      adding more resources to your existing clusters
  elasticity
    asutomatic scalability on demand
  service variety
  reliability
  security

Deployment models
  public
  private
  hybrid
    on-premises + private cloud + 3rd party public cloud
  multi-cloud


Types of consumer needs
  personal/consumer
  vertical
    usually in orgainzations with rigid hyerarchy
      healthcare
      governmental
  external
  internal


Cloud service models

Infrastructure as a Service (IaaS)
  infrastructure
  examples
    Cisco
    Microsoft Azure
    Amazon Web Services (AWS)
    Google Compute Engine (GCE)
    Digital Ocean
Platform as a Service (PaaS)
  platform layer
    operating system
    pre-built development tools
    testing
    runtime
    middleware
    and databases
  examples
    Azure App Service
    Salesforce.com
    Google App Engine
    AWS Elastic Beanstalk
    OpenShift
Software as a Service (SaaS)
   complete solution, no-code, no-infrastructure
   examples
     Google apps (i.e., Gmail or Google Maps)
      Dropbox
      Salesforce
      YouTube
      Concur
      GoToMeeting
      MS Office 365

Use SaaS

For standard solutions requiring a low level of customization and internet access via multiple device types
When you don't have the skills internally to install, run, and manage the software
When it's more cost effective to let a specialist run the software
When you're happy with the SaaS provider's data privacy, service and configuration/integration options

Don’t Use SaaS

When you need a high level of configuration, customization, or specialist integrations
When you can run it yourself more effectively
When you have compliance requirements that don’t permit outside hosting
When extensive experience of business process customization is required

Use PaaS

When developers are comfortable using standardized building blocks
When developers require the specialized capabilities it provides but no internal team wants to own the service
For services outside your core business area, such as automation, deployment and monitoring

Don’t Use PaaS

If your project needs proprietary building blocks
When you are using low level or legacy languages for development
If the application requires you to customize hardware and software
When applications generate a transaction volume that might make PaaS services cost prohibitive

Use IaaS

When you need control over your high-performing applications
When you don’t have the finances to invest in hardware
When you want to purchase only what you consume or need
When you need to be able to change out specific hardware and software easily

Don’t Use IaaS

If you are not interested in or able to handle the management of a virtual machine
If the vendor does not meet your security standards


## Containers

**container**
  a standard unit of software 
    code and all its dependencies

**container image**
  a lightweight, stand-alone, executable package of software
  includes everything needed to run an application
    code, runtime, system tools, system libraries and settings

#PART II

##Data engineering
  a set of operations aimed at creating interfaces and mechanisms for the flow and access of information

**Data engineers** set up and operate the organization's data infrastructure, preparing it for further analysis by data analysts and scientists.

###Responsibilities
- Business responsibilities
- Technical responsibilities
---
- Speaking With Technical and Nontechnical People
- Scoping and Gathering Business and Product Requirements
- Applying Common Software Methodology (e.g., Agile, DevOps, and DataOps)
- Controlling Costs
- Learning Continuously
- constructing architectures with high-level cost and performance optimization using commercially available or custom-made components.

##Data Engineering Lifecycle
- Generation
- Storage
- Ingestion
- Transformation
- Serving data

### Stage 1: Generation
The source system is the data engineering lifecycle's data origin. A source system may be:

An IoT device
An application message queue
A transactional database

####Source System Evaluation Checklist
- What are the primary attributes of the data source?
- How is source system data persisted? Is data stored permanently, or is it transient and rapidly discarded?
- How fast is data created? How many occurrences are there per second? How many gigabytes per hour can be transferred?
- How consistent can data engineers anticipate the output data to be? How often do data inconsistencies—unexpected nulls, poor formatting, etc.—occur when you do data-quality checks on the output data?
- How often do mistakes occur?
- Will there be duplicated data?
- Will certain data values come late (i.e., significantly later than other concurrently generated messages)?
- What is the schema of the data that was ingested? Would data engineers need to link multiple tables or systems to get a comprehensive view of the data?
- How are schema modifications (e.g., the addition of a new column) handled, and how are downstream stakeholders notified about this?
- How often must data be extracted from the source system?
- For stateful systems (e.g., a database that tracks customer account information), is data given as periodic snapshots or change data capture (CDC) update events?
- What logic governs the implementation of modifications, and how are they recorded in the source database?
- Who or what is the data provider that will transfer information for use downstream?
- Will reading from a data source affect system performance?
- Does the source system rely on upstream data? What qualities do these upstream systems have?
- Are there data quality measures in place to detect late or missing data?

###Stage 2: Storage

**Storage System Evaluation Questions**
- Is this storage option compatible with the architecture's requisite write and read speeds? Will storing cause bottlenecks in subsequent processes?
- Do you understand how this storage technology operates?
- Are you using, for example, a high rate of random access updates in an object storage system? (This is an antipattern with a substantial performance cost.)
- Can this storage system accommodate expected future growth? (Consider all storage system capacity limitations, including total available storage, read operation rate, write volume, etc.)
- Can downstream users and processes retrieve data according to the appropriate service-level agreement (SLA)?
- Is this a storage-only solution (object storage), or does it enable complicated query patterns (e.g., a cloud data warehouse)?
- Is the system schema-independent (object storage)? Is the schema flexible, e.g., based on Cassandra? Does it have a mandatory schema (a cloud-based data warehouse)?
- How do you monitor master data, the data quality of golden records, and data lineage for data governance?
- How are regulatory compliance and data sovereignty managed? For instance, can you only keep your data in certain geographical locations?

**Data temperature** is determined by the frequency of data access.

###Stage 3: Ingestion

Ingestion Checklist

What use cases exist for the data being ingested?
Can this data be repurposed to avoid creating several copies of the same dataset?
Are the systems producing and consuming this data reliably, and do I have access to it when necessary? Where does data go when it is ingested?
How often will data access be required? How often will the data usually arrive?
What is the format of the data?
Can the storage and transformation systems handle this format?
Is the source data suitable for immediate use downstream? If so, for how long, and what factors might render it unusable?
Does the streaming source's data need to be transformed before reaching its destination?

**Batch vs. Streaming**

###Stage 4: Transformation
data to be converted from its original format into a format suitable for subsequent use cases. A significant driver of data transformation is business logic. 
 
####happen immediately after data intake:

Mapping data into the correct types (e.g., converting text data into numeric and date types)
Formatting records in standard formats
Removing invalid entries

####Later phases of transformation may include:

Schema transformation
Schema normalization
Reporting or transforming data for downstream ML procedures using large-scale aggregation

####Transformation is often intertwined with other stages of the lifecycle.
Transformation in Generation and Ingestion
Transformation and Storage
Other Phases (Data preparation, data manipulation, and data cleansing)

**Featurization** aims to identify and improve data characteristics that are important for training ML models.

###Stage 5: Serving Data
BI
ML

###Undercurrents
- security, data management, DataOps, and orchestration

Security
  common approaches

####Data Management
- involves creating, implementing, and overseeing plans, policies, programs, and practices that provide, control, safeguard, and increase the value of data and information assets throughout their lifespan

Role of the data engineer in data management:
- use a collection of best practices to manage data effectively.
- use data management frameworks to go beyond technical responsibilities and implement a properly structured data management plan.
- know how data brings value across the company at all levels, from analysts to the CFO or CEO.

Aspects:
Data Modeling and Design
Data Lineage (what did what, when)
Data Integration and Interoperability (solutions diversity)
Data Lifecycle Management (tech level, automation, tiers)
Data Governance (who what when)

Data Lineage
- Record data's audit trail throughout its lifespan
- Document systems that process data and the downstream data it relies on
- Track errors
- Ensure accountability
- Debug data and processing systems
  
**Data observability–driven development (DODD)**
In data observability–driven development (DODD), data is collected throughout its entire ancestry. This method is used throughout the development, testing, and manufacturing phases to ensure quality and adherence to specifications. The DODD technique offers an appropriate foundation for considering data observability. DODD is similar to test-driven development (TDD) in software engineering.

**Data Lifecycle Management**
DLM products automate lifecycle management procedures. Typically, they split data into tiers in accordance with predetermined policies. According to standards such as the General Data Protection Regulation (GDPR) and the California Consumer Privacy Act (CCPA), they automate data migration from one layer to another.

Data Governance
 categories of data governance are:

Discoverability (including data quality)
Security
Accountability

###DataOPS
primary components:
Automation
Monitoring and observability
Incident response

Automation:
Change management (environment, code, and data version control)
Continuous integration/continuous deployment (CI/CD)
Configuration as code

Monitoring:
 frequently comparing vital company data to quality control criteria

Observability:
 supports the five major pillars of data health—freshness, distribution, volume, schema, and lineage—to improve data quality and decrease data downtime

###Orchestration
schedulers
orchestration engines

Airflow for Orchestration

##BIG DATA

###Data characteristics

Types of Data – Structured and Unstructured

Structured Data:
Structured data is information that is highly organized and can be neatly uploaded into a relational database. You may want to think of traditional row database structures to get an idea. The data lives in fixed fields and can be easily detected by an algorithm or through a search operation. It is easy to enter, store, find and analyze. However, this data must be strictly defined when it comes to field name, type (whether it is alpha, numeric, date or currency). Consequently, it is frequently restricted by character numbers or some specific terms. Usually, analysts use Structured Query Language, or SQL to perform searches among the vast amounts of structured data within relational databases.

Examples of structured data are: CSVs; TSVs files; database tables.

Semi-Structured Data:
Semi-structured data still has the internal tags and markings that help you identify separate data elements that let you group information and establish a hierarchy. Documents and databases may be semi-structured, representing only 5-10% of the structured, semi-structured or unstructured data. However, the information within that data may prove crucial to the business.

Examples of semi-structured data are: logs files; xml; json.

Unstructured Data:

Unstructured data does not conform to a spreadsheet or database, even if there is some structure within. Current data mining techniques often leave out important information, thus, making it expensive and difficult to analyze unstructured data.

Examples of unstructured data include: videos and image; word 
processing documents.

Schema on Read & Write

**Schema on read** - structure is applied to the data only when it's read, this allows unstructured data to be stored in the database. 
Since it's not necessary to define the schema before storing the data, it makes it easier to bring in new data sources on the fly.
The exploding growth of unstructured data and overhead of Extract Transform Load (ETL) for storing data in RDBMS is the main reason for the shift to schema on read. 
Frequently, analysts aren't sure what types of insight they will gain from new data sources, which explains why getting new data sources is time-consuming. 
Think of this as a schema on demand! (Data modeling is still required!)

What is Schema on Write?
Schema on write is creating a schema for the data before it is written into the database. If you tried to work with a database, then you used Structured Query Language (SQL) to read data from the database and understand the structured nature of a Relational Database (RDBMS).
Extract-Transform-Load work in an RDBMS is time-consuming. Most of the data in the world is unstructured. If it is, it means someone has already structured it before you. You have to define the schema for the data and structure it based on that specific schema to get information out of the bulk of data in your possession.

Speed of Data

Stream Processing:
In stream processing, each new piece of data is processed when it arrives. In contrast to batch processing, it does not imply waiting until the following batch processing interval. In this case, data is processed as separate pieces and not being processed as a batch at a time.

Micro-batch Processing:
In micro-batch processing, you run batch processes on much smaller accumulations of data - typically less than a minute's worth of data. This means data is available in near real-time. Micro-batch processing is useful when you need very fresh data, but not necessarily in real-time. In other words, you can't wait an hour or a day for batch processing to run, but you also don't need to know what happened in the last few seconds.

Batch Processing:
Batch processing is when the processing happens to blocks of data that have already been stored over a period of time. For example, processing all the transactions that have been performed by a major financial firm in a week.

Storage & Formats of Data
Working with large scopes of raw data brings you to the question how to store all this data effectively. The key requirements of big data storage are that it can handle very large amounts of data and keep scaling to keep up with growth. Nowadays, there are lots of storages on the market, so you it can be confusing to choose.
Click on tabs to learn more about storage of Data.

File Storage

HDFS (the Hadoop distributed file system) is a distributed, scalable, and portable file system written in Java for the Hadoop framework.

ZFS is an advanced file system. It has some interesting features: pooled storage, copy-on-write, snapshots, RAID-Z, data integrity verification and automatic repair.

No-SQL
There are lots of types of no-SQL databases.

Column: in such databases data is stored in a columnar form. Main examples include: Accumulo, Cassandra, Druid, Vertica etc.

Key Value: such databases are organized as key value pairs, where each key appears exactly once. The keys are usually arranged in a sorted fashion. Examples of key-value databases are: Aerospike, ArangoDB, Dynamo etc.

Graph: these databases are arranged in the form of a graph with the elements connected using the relations between them. Examples include AllegroGraph, InfiniteGraph, MarkLogic etc.

Document: this type refers to the databases are stored in the form of documents that are accessed using a unique key. A single key references a document. Examples of Document databases are: Apache CouchDB, BaseX, Clusterpoint erc.

Traditional DB
MySQL is an open source relational database management system. It has stand-alone clients allowing for interfacing directly with a MySQL database through SQL. Nonetheless, this database management system is primarily used in a bundle with other programs to design applications that require relational database capability.

Raw Data Formats & Processed Data Formats

There are multiple storage formats, which are suitable for storing data in HDFS, such as plain text files, rich file formats, like Avro and Parquet, and Hadoop specific formats, like Sequence files. These formats have their own pros and cons depending on the use cases.

Let's classify the stored data formats into two simple categories: Raw Data Formats; Processed Data Formats.

RAW File Formats

Typical access Pattern:
Use all the fields to validate, enhance, join data
Read through whole data set

Formats:
Plain Text (Unstructured)
Structured Text Data (Rows - CSV, TSV, JSON)

Processed File Formats
Typical access Pattern:
Use limited fields to aggregate data or run other analytical queries
Read filtered subset

Formats:
Parquet (Columnar oriented)
ORC
Sequence

Since you only access a few columns of processed data in an analytical query, the storage system is probably going to be able to process the request efficiently, at least in terms of disk I/O and so on.

Raw Data Formats
Raw data is any data that hasn't been processed. This means both manual and automated processing. Other names for raw data are tidy data, flat data, primary data, atomic data and unit record data. Each row in a raw data table has an observation and each column represents a variable that describes properties of every observation.

Plain Text File
A very common use case of the Hadoop ecosystem is to store log files or other plain text files with unstructured data, for storage and analytics. These text files could easily take up all of the disk space, so proper compression is required depending on the use case.

Structured Text Data
There are more sophisticated forms of text files with data in some standardized form, such as CSV, TSV, XML or JSON files.

Processed Data File Formats
Speaking about a column-oriented format, the rows are divided into row splits. Afterward, each of these splits is kept in the column-oriented fashion. Specifically, each row's values in the first column are stored in the first place. Then, the values are followed by those of each row in the second column, and so on.

A column-oriented layout allows for skipping columns that cannot be accessed in a query. Let's take a look at a query of the table that processes only 1 column with row-oriented storage, for instance, a sequence file. In such case, the entire row is loaded into memory but the second column is the only one that is actually read.


Processed data file formats.

Columnar Formats
They eliminate I/O for columns that are not part of the query. This works well for queries, which require only a subset of columns. Also, it provides better compression as similar data is grouped together in columnar format.

Sequence File
Sequence File is a row-based file consisting of binary key-value pairs. As an input-output format, it is frequently utilized in MapReduce. In addition, it is worth noting that, internally, the temporary outputs of maps are stored using Sequence File. Moreover, sequence files provide faster read/write than that of the text file format. However, they are not efficient for querying and analytics, have limited compression capabilities and support splitting even when the data is compressed.

Parquet
Parquet is a columnar format. Columnar formats work well where only few columns are required in query/analysis. Hence, nothing but required columns would be fetched or read, which reduces the disk I/O. Parquet is well suited for data warehouse solutions where aggregations are required on certain columns over a huge set of data. This format provides very good compression, up to 75% when used with compression formats like snappy.

Avro
Avro file is widely used one as a serialization platform. AVRO is a row-based file format, which offers compact and fast compressing format. Avro has a schema-based system. A language-independent schema is associated with its read and write operations. Avro depends heavily on its schema. It serializes the data into a compact binary format, which can be deserialized by any application. Avro allows every data to be written with no prior knowledge of the schema. Resulting serialized data is lesser in size. Schema is stored along with the Avro data in a file for any further processing. Avro schemas are defined with JSON that simplifies its implementation in languages with JSON libraries.

Columnar vs Row OR Parquet v/s Avro
Columnar formats are utilized when it is necessary to issue a query focused on a few columns rather than the entire row. The column-oriented storage pattern is suited for columnar formats, whereas Row formats are used when you need to access all of the fields within the row. On the other hand, Avro is used to store raw data because, more often than not, all of the fields are necessary.

Formats of Data: Row & Columnar

In general, column-oriented formats work well when queries access a small number of columns in the table. On the contrary, row-oriented formats are suitable when numerous columns of a single row are required for simultaneous processing.

Column-oriented formats need more memory to do writing and reading operations because they have to buffer a row split in memory, not simply a single row. Besides, in most cases, it is impossible to control when writes occur (by sync or flush operations). Consequently, column-oriented formats are not a good fit for stream writes because the current file is unable to recover if the writer process breaks. At the same time, row-oriented formats, such as Avro datafiles and sequence files, can be read up to the latest sync point after a writer failure.

Data Compression
Big data solutions are developed to process a large amount of data fast. Compressing the data speeds up the I/O operations and saves storage space; however, it may increase processing times and load up the CPU to decompress the data. One must find a balance between compressing data, processing data and utilizing the CPU. In order to support parallel processing, compressed files must be splittable. This will allow for inputting the data with multiple tasks running in parallel. If a file is not splittable, advantages of parallel processing frameworks are lost, as the file cannot function as input for multiple tasks.


##Big Data Solutions
Eight Characteristics of Ideal Big Data Solutions

Scalable: Must handle predictable growth in storage, throughput, and access speed without requiring massive staff increases
Fault Tolerant: System operation continues even when components fail
High Availability: Services continue working despite infrastructure crashes through redundant nodes and automated failover
Accessible but Secure: Implements the CIA Triad (Confidentiality, Integrity, Availability) for data protection
Extract Knowledge: Enables fact-based decision making through data insights
Workflows as Code: Makes workflows collaborative, versionable, testable, and maintainable
Integrate: Must accommodate legacy systems containing valuable business logic
Self-Healing: Automatically recovers from component failures through data processing operations

Five Base Functions of Big Data Platforms
1. Data Collection/Ingestion

Continuously ingesting data from enterprise applications
Streaming data from third-party systems and social media
Data collection from IoT platforms

2. Data Storage

Universal storage for heterogeneous data and multimedia
Real-time access to ingested data streams
Support for on-premise, cloud, and geographically distributed storage

3. Data Exploration

Data product design and prototyping
Access to full range of data in original format for analysis
Comprehensive toolset for data discovery, machine learning, and collaboration
Data enhancement processes: enrichment, filtering, cleansing, verification

4. Data Governance

Data catalogization
Data quality and lineage management
Data access control

5. Data Product

Data product manufacturing
Data product delivery
Enterprise integration

General Architecture
The architecture includes twelve logical components/layers:

Edge/Ingestion: Automated data extraction and loading
Data Storage: Flexible, scalable long-term storage
Analytics Production: Scalable ETL for consumable data
Management: Data catalog, models, job monitoring/scheduling
Exploratory: Analytical toolset for data mining and statistical analysis
CI/CD Pipelines: Secure, multi-tenant automation toolset
ML Training: Multi-tool chain training environment
AI Services: Scalable AI services environment
Data Product Storage: Flexible storage with reliable transfer
Data Access: Consumer-facing interfaces for published data
AI Products: Marketplace of AI product families
AI Access: Consumer interfaces for AI products

Key Architecture Features

Unified ingestion approach via ingestion factories
Dedicated data factory instances per organizational unit
Limited raw data source access through specific data factories
Data product marketplace for advertising and access
API-level redirection without physical data movement
Enterprise data factory templates and shared products

Data Assets: Sources vs. Products
Data Sources

Data originally loaded from internal or external systems
Examples: Operational database tables, system-generated files, message flows
Raw data requiring transformation

Data Products

Result of transforming company data into value-generating assets
Examples: Business dashboards with KPIs, financial reports, enriched datasets
User-friendly tools providing analytics to non-data scientists

Data Modeling Methodologies
Data Lakes

Massive collections ranging from raw to curated data
Ideal for data science, AI, and machine learning
Stores vast amounts without expensive ETL processes

Data Warehouses

Integrated central repositories from multiple sources
Carefully selected, cleaned, and categorized data
Automated data management for business user access

Data Marts

Specific subsets of data warehouses
Focused on single topic areas
Faster and less expensive than full warehouses

Data Vaults

Comprehensive system for evolving business requirements
Doesn't predetermine data usefulness
Provides "single version of facts" rather than "single version of truth"

Example Architecture Implementation
The course includes a practical example showing:

Ingestion: Multiple data sources (Oracle DB, Elastic Filebeat, Kafka) → Kafka topics
On-premise Hadoop: Data replication → HDFS storage → Spark processing → delivery DB
Public Cloud: AWS S3 storage → Jupyter Notebook processing → ML model training → Nexus Repository
Product Delivery: Tableau visualization and API layers for ML model evaluation

##Data Platform Deployment Options

Hadoop as a Big Data Tool
What is Hadoop

Open-source framework managed by Apache Software Foundation
Designed for storing and processing big data effectively
Handles structured and unstructured data with flexibility for collection, processing, and analysis

How it works

Two main systems: Hadoop Distributed File System (HDFS) for storage and MapReduce engine for processing
HDFS splits data into blocks and distributes them across cluster nodes for parallel processing
Closely coupled with MapReduce for efficient data transfer and processing

Hadoop-Based Cloud services

Amazon EMR and GCP Dataproc are managed Hadoop and Spark services
Used for big data processing, streaming, interactive analysis, and machine learning
Support installation of Apache Hadoop ecosystem components including Spark, Pig, Hive, and Presto

Data Platform Cloud Deployment Evolution
The evolution over the last decade moved from on-premise to multi-cloud deployment:
On-Premise Challenges:

Must be managed by the company running the premises
Difficult availability and durability during deployment
Hardware acquisition requires advance planning and budgeting
Need for deep expertise in platform management
Scalability challenges - expensive and time-consuming
Moving large datasets can be problematic

Hybrid Cloud:

Stores sensitive data in private datacenters while keeping other data in cloud
Only small portion of data is typically sensitive
Cloud can be more expensive but allows faster scaling and movement

Multi-Cloud Trend:

About a decade ago, most deployments were on-premise
Three years ago, most big enterprises had some cloud presence
Recently, companies diversify across multiple clouds due to technology availability

Cloud Market Statistics 2022
Microsoft's Rise:

For the first time, Microsoft Azure surpassed AWS in adoption
80% of respondents use Azure vs 77% using AWS
For companies spending over $12 million annually, AWS maintains slight advantage (53% Azure vs 52% AWS)

Top Cloud Challenges:

Security (top concern)
Cost management
Managing software licenses (76% find challenging)
Understanding Bring Your Own Licensing (BYOL) implications (39% find challenging)

Multi-Cloud Strategy:

99% of enterprises use multiple clouds
80% use hybrid strategy combining public and private clouds
Multi-cloud remains the standard approach for enterprises

Hadoop Distributions
Native Hadoop:

"Vanilla" Hadoop provided by Apache Software Foundation
100% community-driven with binary versions available
Labor-intensive to tie components together

Major Players in 2019:

Cloudera: Software platform for data engineering, warehousing, ML, and analytics
Hortonworks: Developed open-source software support around Apache Hadoop (merged with Cloudera)
MapR: Provided access to Big Data Workloads from single cluster (acquired by HPE after funding issues)

Market Changes:

Cloudera acquired Hortonworks while MapR faced bankruptcy
Companies moved toward cloud deployments and cloud-native services
Businesses prefer cloud service advantages without server maintenance
These factors impacted stock prices, with Cloudera's stock declining from March 2019

Major Cloud Providers Comparison
Amazon Web Services (AWS):

Storage: S3, EBS, EFS, Storage Gateway, Snowball series
Database: Aurora, RDS, DynamoDB, ElasticCache, Redshift, Neptune
Backup: Glacier

Microsoft Azure:

Storage: Blob Storage, Queue Storage, File Storage, Disk Storage, Data Lake Storage
Database: SQL Database, MySQL, PostgreSQL, Data warehouse, Cosmos DB, Table storage, Redis cache
Backup: Archival Storage, Recovery backups, Site recovery

Google Cloud Platform (GCP):

Storage: Cloud Storage, Persistent Disk, Transfer appliance, Transfer Service
Database: Cloud SQL, Cloud Bigtable, Cloud Spanner, Cloud Datastore
Backup: Nearline (frequently accessed), Coldline (infrequently accessed)

Databricks Platform

Apache Spark-based analytics platform optimized for cloud services
Enables data team collaboration for solving complex problems
Adds enterprise-grade functionality to open-source innovations
Fully managed cloud service with data security and software reliability
Interoperability with AWS and Azure
Used across various industries for ETL, data discovery, warehousing, and product deployment


## HADOOP

Hadoop: Introductory Manual
Table of Contents

Introduction

Lesson 1: What Hadoop Is

Lesson 2: Releases and Installation

Lesson 3: Working with Hadoop

Lesson 4: Hadoop in the Cloud

Lesson 5: Hadoop Infrastructure Architecture

Lesson 6: Hadoop in the Real World

Lesson 7: Introduction to HDFS and YARN

Glossary

References

Introduction

Data volumes today are growing at a pace that traditional relational databases cannot handle effectively. Hadoop, an open-source framework from the Apache Software Foundation, provides a way to store and process massive datasets in a distributed, fault-tolerant, and scalable way.

This manual introduces Hadoop fundamentals, installation basics, core components, and its applications.

Lesson 1: What Hadoop Is

Hadoop is an open-source framework designed for distributed storage and parallel processing of large datasets across clusters of computers.

Key Points:

Inspired by Google’s MapReduce and Google File System (GFS).

Runs on clusters of commodity hardware.

Designed for fault tolerance and scalability.

Core Components:

HDFS (Hadoop Distributed File System): Storage layer.

MapReduce: Original computation engine for batch processing.

YARN (Yet Another Resource Negotiator): Cluster resource management.

Lesson 2: Releases and Installation

Hadoop Release History:

Hadoop 1.x: Combined MapReduce and HDFS. Limited scalability.

Hadoop 2.x: Introduced YARN, separated resource management from computation.

Hadoop 3.x: Optimized for cloud, added erasure coding, better container support.

Basic Installation Steps:

Install Java.

Download Hadoop binaries from Apache.

Configure environment variables (HADOOP_HOME, PATH).

Edit XML configuration files:

core-site.xml

hdfs-site.xml

mapred-site.xml

yarn-site.xml

Format the NameNode.

Start Hadoop services.

Modes:

Standalone Mode (default, single JVM, for testing).

Pseudo-Distributed Mode (single machine, simulating cluster).

Fully Distributed Mode (production cluster).

Lesson 3: Working with Hadoop

Hadoop provides command-line tools to interact with HDFS and run jobs.

Common HDFS Commands:

hadoop fs -ls / → list files in HDFS.

hadoop fs -put local.txt / → upload a file.

hadoop fs -get /hdfsfile.txt . → download a file.

hadoop fs -rm /hdfsfile.txt → delete a file.

Running Jobs:
The traditional entry point is MapReduce. Example: the classic word count program.

Lesson 4: Hadoop in the Cloud

Cloud providers simplify Hadoop deployment by offering managed clusters.

Key Services:

Amazon EMR (Elastic MapReduce): Fully managed Hadoop and Spark service.

Google Cloud Dataproc: Fast, scalable cluster creation for Hadoop/Spark.

Azure HDInsight: Microsoft’s Hadoop distribution with integration to Azure tools.

Advantages:

Elastic scaling.

No manual infrastructure management.

Pay-as-you-go pricing models.

Lesson 5: Hadoop Infrastructure Architecture

A Hadoop cluster typically consists of master and worker nodes.

HDFS Architecture:

NameNode: Master server, manages metadata and namespace.

DataNodes: Store actual file blocks, respond to NameNode instructions.

YARN Architecture:

ResourceManager: Allocates cluster resources.

NodeManager: Manages resources on a worker node.

ApplicationMaster: Manages the execution of a single job.

Data Flow:

A file is split into large blocks (default 128 MB).

Blocks are replicated and stored on multiple DataNodes.

Jobs are divided into tasks, scheduled by YARN.

Lesson 6: Hadoop in the Real World

Hadoop is widely used in industries where large-scale data storage and analysis are essential.

Applications:

E-commerce: Recommendation systems and clickstream analysis.

Finance: Fraud detection and risk modeling.

Telecommunications: Analyzing massive network traffic logs.

Healthcare: Genomic sequencing and patient data management.

Government: Large-scale census and population data processing.

Lesson 7: Introduction to HDFS and YARN

HDFS (Hadoop Distributed File System):

Files are split into blocks (default 128 MB).

Each block is replicated (default replication factor = 3).

Provides high availability and fault tolerance.

YARN (Yet Another Resource Negotiator):

Manages system resources across the cluster.

Separates resource management from computation logic.

Supports multiple processing frameworks (MapReduce, Spark, Tez, Flink).

Together, HDFS and YARN form the backbone of Hadoop clusters.

Glossary

Big Data: Datasets too large for traditional systems.

Cluster: A group of networked computers working as a single system.

Fault Tolerance: The ability to recover automatically from failures.

MapReduce: Original parallel processing model in Hadoop.

Replication: Copying data blocks across nodes for reliability.

References

Apache Hadoop Official Website

Tom White, Hadoop: The Definitive Guide

AWS EMR, Google Dataproc, Azure HDInsight documentation


Hadoop: Introductory Manual (with Diagrams)
Lesson 1: What Hadoop Is

Core Components Overview:

+------------------+
|   Hadoop Core    |
+------------------+
|  HDFS   |  YARN  |
| Storage | Compute|
+---------+--------+
      |
      v
 MapReduce / Other engines (Spark, Tez, etc.)

Lesson 2: Releases and Installation

Modes of Running Hadoop:

Standalone     Pseudo-Distributed       Fully Distributed
------------   ------------------       -----------------
One JVM        One machine, simulating  Real cluster with
(no daemons)   cluster daemons          many machines

Lesson 3: Working with Hadoop

File Flow in HDFS:

Local File --> HDFS Put Command --> Blocks --> Replication --> DataNodes

Lesson 4: Hadoop in the Cloud

Cloud Deployment Idea:

          +------------------+
          |   Cloud Vendor   |
          +------------------+
             /     |     \
            /      |      \
       Amazon EMR  GCP Dataproc  Azure HDInsight

Lesson 5: Hadoop Infrastructure Architecture

Cluster Overview:

          +------------------+
          |    NameNode      |  <-- Master (HDFS metadata)
          +------------------+
                   |
   -----------------------------------
   |               |                 |
+--------+    +--------+        +--------+
|DataNode|    |DataNode|  ...   |DataNode|   <-- Stores blocks
+--------+    +--------+        +--------+


YARN Overview:

+------------------+       +------------------+
| ResourceManager  |<----->| ApplicationMaster|
+------------------+       +------------------+
        |
   ------------
   |          |
+------+   +------+
|Node  |   |Node  |   <-- Each node has NodeManager
|Mgr   |   |Mgr   |
+------+   +------+

Lesson 6: Hadoop in the Real World

Example: E-commerce Pipeline

 Customer Clicks
        |
   Web Logs
        |
     HDFS
        |
   MapReduce / Spark
        |
 Recommendations

Lesson 7: Introduction to HDFS and YARN

HDFS Data Storage:

File split into blocks (128 MB)
------------------------------------
 Block 1   Block 2   Block 3   Block 4
   |         |         |         |
Replicated across multiple DataNodes


YARN Workflow:

Job Submission
      |
ResourceManager --> Assign resources
      |
ApplicationMaster --> Manages execution
      |
NodeManagers --> Run tasks

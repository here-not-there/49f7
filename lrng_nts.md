# bigE learning notes

BIG DATA

Data Transformation
  >- AWS course
Data Modelling Methodology - Data Warehouse - Data Lake
  >- bigE **Data Modeling Basics**
Data Modelling Approaches - ER - Dimensional
  >- bigE **Data Modeling Basics** 
  >- Claude
  >- AWS course
CI/CD
  >- bigE CI/CD overview

Leftovers
- bigE Jenkins Overview

White spots:
  software development methodology
  cloud overview (including Containers)


# CI/CD

## **DevOps**

emphasizes collaboration and communication among IT professionals

automates software delivery

automates infrastructure changes.

build, test, release

DevOps benefits:

- higher overall productivity
- faster delivery
- improved quality
- lower costs
- transparent communication
- continuous feedback
- faster resolution of issues

**Core practices**

automation

version control

continuous integration

continuous delivery

configuration management

monitoring and logging

communication

collaboration

## **Continuous Integration**

- frequents merge of smaller code updates into a central repository or version control system
- automated development and testing are performed
- aims
    - to find and manage bugs faster,
    - improve software quality,
    - reduce the time needed to validate and release changes
    - **create deployable artifact**

Ends with publishing vierified artifact

artifact repository

storage

mangement / version control

## **Continuous Delivery**

Continuous Delivery extends Continuous Integration with the deployment of builds to testing or staging environments, where they pass expanded testing. 

- deploy to testing environment & test
- deploy to staging environment & test
- create release candidate
- release

Staging environment

a pre-production environment that closely mirrors production setup

used as the final testing phase before deploying code to live users

Test coverage is as complete as possible, including:

- unit tests
- acceptance tests
- performance / stability tests

Continuous deployment

automation of release to production

CI/CD pipeline

is a set of steps that must be followed to deliver a new version of the software

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


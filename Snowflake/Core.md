# SnowPro Core

## Snowflake AI Data Cloud Features and Architecture (24%)

1.1 Outline key features of the Snowflake AI Data Cloud.
- Interoperable storage
- Elastic compute
- Snowflake’s layers
- Overview of Snowflake editions
1.2 Outline key Snowflake tools and user interfaces.
- Snowsight
- SnowSQL
- Snowflake connectors
- Snowflake drivers
- Snowpark
- SnowCD
- Streamlit in Snowflake
- Cortex (AI/ML services)
- Snowflake SQL API
1.3 Outline Snowflake’s catalog and objects.
- Databases
- Stages
- Schema types
- Table types
- View types
- Data types
- User Defined Functions (UDFs)
- User Defined Table Functions (UDTFs)
- Stored procedures
- Streams
- Tasks
- Pipes
- Shares
- Sequences
1.4 Outline Snowflake storage concepts.
- Micro-partitions
- Data clustering
- Data storage monitoring

## Account Access and Security (18%)

2.1 Outline security principles.
- Network security and policies
- Multi-Factor Authentication (MFA) enforcement
- Federated authentication
- Key pair authentication
- Single Sign-On (SSO)
2.2 Define the entities and roles that are used in Snowflake.
- Overview of access control
  - Access control frameworks
  - Access control privileges
- Outline how privileges can be granted and revoked
2.3 Outline data governance capabilities in Snowflake.
- Accounts
- Organizations
- Secure views
- Secure functions
- Information schemas
- Access history
  - Tracking read/write operations
- Overview of row/column-level security
- Object tags
- Explain role hierarchy and privilege inheritance

## Performance and Cost Optimization Concepts (16%)

3.1 Explain the use of the Query Profile.
- Explain plans
- Data spilling
- Use of the data cache
- Micro-partition pruning
- Query history
3.2 Explain virtual warehouse configurations.
- Types of warehouses
- Multi-clustering warehouses
  - Scaling policies
  - Scaling modes
- Warehouse sizing
- Warehouse settings and access
3.3 Outline virtual warehouse performance tools.
- Monitoring warehouse loads
- Scaling up compared to scaling out
- Query acceleration service
3.4 Optimize query performance.
- Describe the use of materialized views
- Use of specific SELECT commands
- Clustering
- Search optimization service
- Persisted query results
- Understanding the impact of different types of caching
  - Metadata cache
  - Result cache
  - Warehouse cache
3.5 Describe cost optimization concepts and best practices in Snowflake.
- Understanding and exploring the costs of different Snowflake features and services
  - Cost insights feature in Snowsight
  - Use of different table types and sizes
  - Use of views
  - Use of search optimization paths
  - Storage costs
  - Compute costs
- Understand and explore cloud services costs in Snowflake
- Costs considerations when using serverless features
- Cost considerations when moving data among regions
  - Replication
  - Fail-over
- Monitor and control costs
  - Resource monitors
  - Snowflake Budgets service
- Attribute costs
  - Cost center tagging
  - Use of the ACCOUNT_USAGE schema

## Data Loading and Unloading (12%)

4.1 Define concepts and best practices that should be considered when loading data.
- Stages and stage types
- File size and formats
- Folder structures
- Ad hoc/bulk loading
- Snowpipe
4.2 Outline different commands used to load data and when they should be used.
- CREATE STAGE
- CREATE FILE FORMAT
- CREATE PIPE
- CREATE EXTERNAL TABLE
- COPY INTO
- INSERT/INSERT OVERWRITE
- PUT
- VALIDATE
4.3 Define concepts and best practices that should be considered when unloading data.
- File size and formats
  - Overview of compression methods
- Empty strings and NULL values
- Unloading to a single file
- Unloading relational tables
4.4 Outline the different commands used to unload data and when they should be used.
- GET
- LIST
- COPY INTO
- CREATE STAGE
- CREATE FILE FORMAT

## Data Transformations (18%)

5.1 Explain how to work with structured data.
- Estimation functions
- Sampling
  - SAMPLE command
  - /TABLESAMPLE command
  - Sampling methods
    - Fraction-based
    - Fixed-size
- Supported function types
  - System functions
  - Table functions
  - External functions
  - User-Defined Functions (UDFs)
- Stored procedures
- Streams
- Tasks
5.2 Explain how to work with semi-structured data.
- Supported data formats, data types, and sizes
- VARIANT column
- Flattening the nested structure
  - FLATTEN command
  - LATERAL FLATTEN command
- Semi-structured data functions
  - ARRAY/OBJECT creation and manipulation
  - Extracting values
  - Type predicates
5.3 Explain how to work with unstructured data.
- Define and use directory tables
- SQL file functions
- Types of URLs used to access data files
- Processing unstructured data
  - User-Defined Functions (UDFs) for unstructured data analysis
  - Stored procedure

## Data Protection and Data Sharing (12%)

6.1 Outline Continuous Data Protection with Snowflake.
- Time Travel
- Fail-safe
- Data encryption
- Cloning
- Replication and failover
6.2 Outline Snowflake data sharing capabilities.
- Account types
- Snowflake Marketplace
- Data Exchange
- Access control options
  - DDL commands to create and manage shares
  - Privileges required for working with shares
- Secure Data Sharing
  - Direct shares
  - Data listings

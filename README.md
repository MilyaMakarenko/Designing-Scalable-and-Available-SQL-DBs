# Designing-Scalable-and-Available-SQL-DBs
[course link](https://www.linkedin.com/learning/designing-highly-scalable-and-highly-available-sql-databases)

author:  [Dan Sullivan](https://www.linkedin.com/in/dansullivanpdx/)

Data Architect, Author, and Instructor 


### Lecture Notes

## Understanding Scalability Requirements

### Learning about business requirements for database scalibility

Start by understanding the specific business requirements and use cases for the database, including what data you’ll work with and how it’s structured (structured, semi-structured, or unstructured).
Consider data volume, ingestion rate, and expected growth over time to plan for scalability.
Think about the data lifecycle, including how long data needs to be retained and compliance requirements like GDPR.
Understand how the data will be used—whether for transactional processing with low latency needs or analytical decision-making with large queries.
Identify key domain entities and their attributes, keeping in mind that data models may evolve as business needs change.
<img width="600" height="300" alt="image" src="https://github.com/user-attachments/assets/ddba8247-80d0-4183-8c0c-1eff8d852bd9" />

### Identifying use cases for data
    
- Data use cases involve understanding the data lifecycle—how data is created, processed, analyzed, archived, reused, or deleted—and the workloads that describe how data is ingested, stored, and queried.
- Different use cases like sales transactions, equipment monitoring, and customer engagement have distinct data characteristics and access patterns, influencing database design.
- Workloads are multi-step and interdependent, involving various processes beyond just the database, such as services running in containers or cloud environments.
- This understanding is crucial for designing databases that are both scalable and highly available to meet diverse business needs.
<img width="600" height="150" alt="image" src="https://github.com/user-attachments/assets/97a81a2b-fe48-454f-ba80-f6aa399bdaa7" />

### Identifying security and compliance requirements

- Security involves managing who can access and perform operations on data through roles and permissions, following the principle of least privilege to limit access.
- Confidentiality is protected using identity and access management systems and encryption both at rest and in transit; monitoring and data loss prevention help detect unauthorized access.
- Availability ensures data is accessible when needed, supported by redundancy, replication across regions, and disaster recovery plans defined by recovery point and time objectives.
- Integrity means data remains accurate and untampered, maintained through controlled access and measures like message digests and audits.
- Compliance requires adhering to organizational, industry, and government regulations (e.g., GDPR, HIPAA, PCI DSS) that govern data handling based on data type, location, and jurisdiction.


Understanding these elements is crucial for designing databases that are secure, compliant, and reliable at scale.


### Estimating data growth


- Data growth depends on factors like the number of users or sensors generating data, new external data sources, and changes in business processes.
- Managing the data lifecycle is important—deciding how long to keep data and where to store it (hot storage vs archival) affects growth and cost.
- Increased application use and new workloads, such as ETL or machine learning, can significantly increase data volume.
- Machine-generated data can grow much faster and larger than human-generated data, requiring careful planning.
- Data augmentation from third-party sources can also add to data volume unexpectedly.
<img width="800" height="300" alt="image" src="https://github.com/user-attachments/assets/1d74cb7b-b3af-4dc6-a98e-320223ba228b" />


Understanding these factors helps design database architectures that can scale efficiently and control costs.
<img width="600" height="280" alt="image" src="https://github.com/user-attachments/assets/0dd77f9d-1f9d-4580-80d6-f65cf2d89b2f" />

### Challenge: Identify business requirements in a scenario

- Understand the variety of data types and volumes involved, as well as different use cases for the data.
- Consider both technical requirements (like specific technologies or software) and non-technical requirements (such as service level objectives).
- Architects need to collaborate closely with domain experts and business owners to clarify and expand on the initial documentation.
- Asking additional questions helps ensure the database design will meet both functional and scalability needs effectively.
<img width="550" height="400" alt="image" src="https://github.com/user-attachments/assets/a3fa7ec7-8a66-4c27-bd87-803ef571b809" />

This approach is essential for designing scalable and highly available SQL databases that align with real business needs.


### Solution: Identified business requirements
- Consider how humans and machines will interact with the system, including data ingestion methods like streaming or batch loading.
- Think about availability needs, expected user volume, and service level agreements.
- Account for machine learning requirements and the supporting cloud and analytics infrastructure.
- Evaluate growth rates, regulatory compliance, and latency requirements for both data ingestion and querying.


These factors are essential for designing scalable and highly available SQL databases that meet business and technical needs effectively.

<img width="550" height="480" alt="image" src="https://github.com/user-attachments/assets/fa54c933-93dc-44f2-8e0e-556f047c0004" />

## Database Architecture and Relational Databases

### Choosing a data store: SQL, NoSQL, or analytical?
    
- Relational databases use fixed schemas with structured tables and SQL queries, supporting ACID transactions for reliable operations. Examples include PostgreSQL, MySQL, SQL Server, and Oracle.
- 
  <img width="400" height="180" alt="image" src="https://github.com/user-attachments/assets/2a688a55-781b-4073-96ef-90242569846e" />
  
- NoSQL databases come in three types: document (semi-structured JSON-like data, e.g., MongoDB), wide-column (multi-dimensional tables, e.g., Cassandra), and graph databases (nodes and edges representing entities and relationships, e.g., Neo4j).

<img width="390" height="225" alt="image" src="https://github.com/user-attachments/assets/18dee936-cdeb-420e-9387-7e02fe92733c" />
<img width="380" height="224" alt="image" src="https://github.com/user-attachments/assets/1c58c93e-35b4-4068-b825-78f0bbbf67ef" />
<img width="370" height="225" alt="image" src="https://github.com/user-attachments/assets/1ad2313c-356b-4856-b968-55db54d3bc71" />


- Analytical databases are designed for large-scale data analysis with massively parallel scans instead of traditional indexes, like Google BigQuery.
- NoSQL databases emerged to address scalability limits of relational databases but now some relational databases also offer horizontal scalability and global distribution.
- Choosing the right database depends on your data structure, scalability needs, and query types—transactional or analytical.

<img width="600" height="280" alt="image" src="https://github.com/user-attachments/assets/6ed5ec52-3364-40ac-b209-bb230f9ef233" />

This overview helps you understand the strengths and use cases of different database types as you work toward data engineering roles.

### Identifying schemas and domains


- Schemas organize related database objects like tables, views, indexes, sequences, and triggers, usually representing a single business domain.
- A domain is a set of logically related entities that share a data lifecycle and business context, such as customers and their addresses or orders and order items.
- Determining domain boundaries involves understanding entity relationships, data usage together, lifecycle, compliance, and business processes.
- Sometimes, a domain may be split into multiple schemas due to organizational ownership, complexity, or different operational processes.


A **schema** is a collection of related database objects (tables, indexes, triggers). Typically, all of the entities that we're modeling within a schema are from a single domain.

A **domain** is a set of logically related entities (for example, a customer and a customer's address). But even logically related entities can be in different domains if they have a different data lifecycle or different business meaning. Example: a product from a sales perspective versus a product from an inventory perspective — those are different domains.

When deciding how to split things into domains, the key is understanding whether entities are used together, whether they are created and purged in similar ways, and whether they are subject to similar compliance requirements.

Ideally, there's no more than one domain per schema. But sometimes, due to size and complexity, different organizational ownership, or corporate rules, a single domain may have multiple schemas.

### Identifying key entities

Entities are logical representations of things in a domain. You can identify them by looking at the nouns you use when talking about a domain.

A small number of entities will capture most of the important information (like an 80/20 rule). Think of the solar system analogy: a few large objects (Sun, planets) and smaller objects orbiting around them (moons). In data modeling, you have larger, more important entities, and then other entities related to them.

How to find entities?

- Major entities are fairly obvious and easy to identify.

- Minor entities are often not obvious. One way to spot them is to describe a particular operation or process in detail and see what nouns show up.

Examples:

- Sales transaction: customer, product, order, payment method.
  
  <img width="512" height="320" alt="image" src="https://github.com/user-attachments/assets/2c98e808-7bdd-4a95-a266-1fb9f53b05f0" />

- IoT sensor monitoring: measurements, sensors, edge device, building, campus.
  
  <img width="512" height="320" alt="image" src="https://github.com/user-attachments/assets/01d2b796-8991-4891-b7fe-b1b8eb2f9969" />


Questions to ask when modeling:

- What business process is being modeled?

- What business objects or artifacts are used in the process? (e.g., a claim form or policy application)

- What's being analyzed? What transactions are being executed?

- Look at existing reports or the kinds of queries a business analyst might run.

Artifacts like claim forms or policy applications are rich sources of information for how to model a particular entity.

### High-level physical design

Physical Data Model – Tablespaces & Partitions – Short Summary

**Tablespaces** are storage locations for physically storing data (like a file in a server filesystem). They allow us to organize related tables or indexes and enable parallel operations. For example, put a table in one tablespace on one physical device and its index in another tablespace on another device, so writes can happen in parallel. Data within a tablespace is managed as a single unit (drop the tablespace, drop everything in it).

**Partitions** allow us to segment data within a very large table (like an IoT sensor table). Think of partitions almost like subtables. If data for a single sensor is in one partition, you only go to that partition.

Three ways to partition:

- **Time-based**: great for time series data (e.g., create a new partition every day).

- **List-based**: e.g., sales data from North America in one partition, Europe in another.

- **Hash partitioning**: use a hash function on a partition key (like product ID) to evenly distribute data across partitions when no logical partition makes sense.

**Caching** improves read performance, but we often turn to caching later (when building queries), whereas tablespaces and partitions are something we want to think about early in the design process.

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
<img width="400" height="200" alt="image" src="https://github.com/user-attachments/assets/ddba8247-80d0-4183-8c0c-1eff8d852bd9" />

### Identifying use cases for data
    
- Data use cases involve understanding the data lifecycle—how data is created, processed, analyzed, archived, reused, or deleted—and the workloads that describe how data is ingested, stored, and queried.
- Different use cases like sales transactions, equipment monitoring, and customer engagement have distinct data characteristics and access patterns, influencing database design.
- Workloads are multi-step and interdependent, involving various processes beyond just the database, such as services running in containers or cloud environments.
- This understanding is crucial for designing databases that are both scalable and highly available to meet diverse business needs.
<img width="500" height="140" alt="image" src="https://github.com/user-attachments/assets/97a81a2b-fe48-454f-ba80-f6aa399bdaa7" />

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
<img width="600" height="300" alt="image" src="https://github.com/user-attachments/assets/1d74cb7b-b3af-4dc6-a98e-320223ba228b" />


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

<img width="377" height="300" alt="image" src="https://github.com/user-attachments/assets/c07812ab-dd71-4ec3-936e-882c0eeb817f" />

## Data Ingestion
### Human and Machine Scale Data
When designing a scalable database, data ingestion is a key factor to consider early on. Ingestion is about getting data in as quickly and reliably as possible, keeping up with how the data is being generated.

There are two different scales of ingestion (think of them as ends of a spectrum, not hard distinctions):

**Human scale**

Data is created at the speed a human can generate it (typing, speaking, etc.).

Growth depends on the number of users.

This was the main concern for databases 20–30 years ago.

However, human scale can sometimes reach machine-scale levels if an app becomes very popular (e.g., millions of customers using a mobile claims processing app).

**Machine scale**

Data is generated by machines: IoT devices, infrastructure monitoring telemetry, set-top boxes, payment card swipes, browser activity tracking.

Growth depends on the number of devices, how frequently they're used, and how much data each device generates per operation.

Fortunately, many devices generate predictable data volumes per transaction (e.g., payment card devices produce highly structured data of roughly the same size). The main source of variation is how many devices are out there and how often they are used.

**Key takeaway:**
Your application will fall somewhere on the spectrum from human scale to machine scale. Depending on where it falls, you'll want to choose ingestion techniques that are appropriate for that place within the spectrum.

### Different data ingestion strategies
<img width="201" height="184" alt="image" src="https://github.com/user-attachments/assets/9405e0ae-15f9-4a64-b89e-a35659e4bb75" />

**Human scale ingestion:**

- Data is ingested directly by an application (e.g., via GUI or REST API).

- The application generating the data is tightly coupled with the database.

- Often "write once, read many times" (common in OLTP).

- Involves receiving, validating, processing, then writing to the database.

- Workflows require a mix of reads and writes at the same time.

**Machine scale ingestion:**

- Data is not written directly to the database. Instead, we ingest into a buffer or queue.
  
<img width="201" height="174" alt="image" src="https://github.com/user-attachments/assets/ba369807-58e3-4334-98e3-d75f2247c875" />


- This decouples ingestion from processing.

- Helps handle spikes in ingestion without subjecting the database to wide swings in performance demands.

- With time series data, the most recent data is often the most valuable (e.g., anomaly detection). We may process data before writing it to the database.

**Key takeaway:**

- Human scale: smaller amounts, direct write to DB, CRUD interfaces.

    Machine scale: large volumes arriving in very short periods. If the database can't keep up and there's a risk of losing data, use machine scale techniques (buffer/queue) to decouple ingestion from processing.

### Ingesting at human and machine scale

For human scale, we usually do synchronous ingestion. That means the app writes data to the database and waits for a response before continuing. User interfaces work this way a lot — you enter something, you get a confirmation, then you move on. But spikes can happen, like a flash sale. If we're doing synchronous writes and suddenly there's a huge spike in orders, we need to scale up the database to handle that peak because there's no buffer. We also need to think about payload sizes, average time to persist data, and all the resources needed for writing to tables and updating indexes.

For machine scale, we don't write directly to the database. Instead, we use a buffer or queue between the data source and the app. Devices send data to an ingestion endpoint, which does basic checks, then puts the data in a queue. The application pulls data from the queue (pull is better because the app stays in control). This decouples ingestion from processing and helps handle spikes without overwhelming the database.

When designing this, we need to figure out buffer size, infrastructure needs, average payload size, network latency, and how long database writes actually take. All of this matters if we want to meet service level agreements.

### Message queues to buffer ingested data

Message queues help decouple services when one service processes data faster than another can keep up. The slower service reads from the queue at its own pace. This doesn't speed things up, but it prevents data loss. Losing data is worse than processing it slowly. Queues are designed to ingest and write data with very low latency, much faster than a typical database.

Examples:

- **Apache Kafka** – open source, you manage it yourself. It's a streaming log that can be used as a queue. Supports re-reading messages, can set retention to infinite (use as a persistent store if you want). Uses consumer groups instead of subscriptions – different apps can read the same messages.

- **Google Cloud Pub/Sub** – managed service, scales globally. Supports push and pull subscriptions. Guarantees at-least-once delivery (exactly-once available only for pull). Messages not acknowledged go back to the queue – good for reliability. But messages may be out of order, so if ordering matters, you need something else like a stream processing platform (e.g., Dataflow, Flink).

**Key takeaway:** Queues buffer data to handle spikes without dropping data. Just be careful with duplicates (at-least-once) and message order if your application requires it.

### Data modeling for scale: Event sourcing

Event sourcing is an alternative to the usual CRUD pattern (create, read, update, delete). In CRUD, we update rows directly and use row locks to prevent conflicts. Locks work fine but can become a problem when we try to scale – they block operations and slow things down.

<img width="200" height="140" alt="image" src="https://github.com/user-attachments/assets/5bedee7b-97d0-4022-a15a-ec494fe677b3" />


Event sourcing avoids locks by separating writes from reads. Instead of updating data, we only append events to a log. Every change becomes a new event – claim created, policy verified, claim item added, etc. We never update or delete anything in the event log.

<img width="200" height="140" alt="image" src="https://github.com/user-attachments/assets/2b496f01-3973-405b-8d5c-6db861399910" />
<img width="200" height="140" alt="image" src="https://github.com/user-attachments/assets/4b4c4f75-f545-4cff-b309-87300685c4a6" />


So where do we read from? We use materialized views that consume the event log and build a current state (like a summary row for an insurance claim). Reads go to the materialized view, writes go to the event log. They're decoupled.

The trade-off? The materialized view might not always be perfectly up to date. If we add events faster than we refresh the view, there's a temporary inconsistency. But eventually, everything becomes consistent. That's called eventual consistency.

The value? We can ingest data very quickly without blocking reads. For applications with many updates to the same record, event sourcing helps scale by trading a bit of consistency for better performance.

### Command Query Responsibility Segregation (CQRS)

CQRS stands for Command Query Responsibility Segregation. The main idea is simple: separate read operations from write operations. Sounds similar to event sourcing, and yes, they work well together.

On the command side – that's writes. Commands change data: create an order, add an item, delete something. This side is optimized for write performance.

On the query side – that's reads. Queries read data, typically from a presentation model (like a materialized view). This model is built specifically for how people query data, so queries become much simpler – fewer joins, less complex logic.

The big benefit is that you can scale reads and writes independently. But there's no free lunch. CQRS adds complexity – more moving parts. It also brings eventual consistency, just like event sourcing. You have to tolerate that.

Because of the complexity, CQRS isn't for everything. Use it only for really complex domains that need high scalability. And keep it small – use it within bounded contexts (from Domain-Driven Design). Better to have two small CQRS implementations than one huge complicated one.

## Designing for Scalable Quirying

### Transactional vs. analytical queries

Transactional queries target a small number of rows but often need many columns. Think of looking up an employee record in an HR database – you want everything about that person. Row-oriented storage works well here because data for the same row is stored together on disk. Transactional queries also use indexes heavily and often involve complex joins.

Analytical queries are different. They scan a large number of rows but usually only need a small number of columns. For example, checking product sales across many stores over the last two quarters – you probably just want quantity sold and revenue, not every product attribute. Column-oriented storage is better for this because data from the same column across many rows is stored together.

For indexes – it depends. In relational databases (Postgres, Oracle), analytical queries still use indexes, especially with star schemas. But some analytical databases like BigQuery don't use traditional indexes at all.

So the choice between row vs. column storage, and how you handle indexes, really depends on whether your query pattern is transactional or analytical.

### Indexing for query performance

Indexes help queries run faster by reducing how much data we have to scan. They also can enforce unique constraints. But indexes aren't free – they add extra work for both reads and writes because we have to read and update the index along with the actual data.

B-tree indexes are the default in most databases. They work like a balanced tree – you start in the middle, go left or right depending on your value, and quickly find what you need. Search time grows slowly (logarithmically) as the table gets bigger. Great for most cases.

Bitmap indexes use bits (1s and 0s) to mark whether a row has a certain value. They work well when a column has only a few possible values (low cardinality). You can combine them with logical operations (AND, OR, NOT) very quickly. Good for read-heavy workloads, but updates are expensive. Postgres doesn't have persistent bitmap indexes (it builds them on the fly), Oracle does.

Hash indexes turn data into a fixed-size hash value. They only work for equality lookups – you can't use greater than or less than. Similar inputs can produce very different hashes. Good when you have many distinct values and just need exact matches.

Quick rule of thumb:

- Default choice → B-tree

- Few possible values, lots of reads → Bitmap

- Many distinct values, only equality checks → Hash

  <img width="200" height="140" alt="image" src="https://github.com/user-attachments/assets/534c6bdd-f685-4017-8509-5741c8773cca" />


  <img width="200" height="140" alt="image" src="https://github.com/user-attachments/assets/42f74114-2a2a-4761-a655-6288e485ec17" />

### Materialized views for transactional queries

A materialized view is basically the saved results of a query. You run a query once, store the results, and then others can read those stored results instead of running the same heavy query again.

This works well when you run the same query many times but only need to compute it once. It's a form of caching – you trade storage space for faster query performance.

When to use them:

- Long-running queries – run once, save, reuse.

- Complex queries that put heavy load on the CPU (lots of joins, etc.).

- Aggregates or derived data (averages, standard deviations, top K products).

- Patterns like event sourcing and CQRS.

Things to watch out for:

- Materialized views are eventually consistent – the data might not be perfectly fresh. You need to tolerate some level of staleness.

- Cost of updates – if you have to refresh the view every minute but only query it every 20 minutes, it's probably not worth it.

- Some databases block reads during updates. If an update takes a long time, you can't read it when you need it.

- Storage size – materialized views take up space and generate log data. Is the size justified?

Bottom line: Materialized views save time on repeated queries but cost storage and update effort. They work best when the same results are read many times and you can live with some delay in freshness.

### Using read replicas to improve query performance

A read replica is a copy of your primary database that handles read queries (SELECT statements) while the primary focuses on writes (INSERT, UPDATE, DELETE).

The problem: A single server handling both reads and writes can become a bottleneck. Too much data coming in, or too many users querying at the same time – it's hard to scale up forever.

The solution: Set up read replicas. The primary ingests data, processes it, writes it to disk, and then pushes copies to the replicas. Queries are sent to the replicas instead of the primary.

Benefits:
- Primary focuses on writes and ingestion.
- Replicas handle reads.
- You can add multiple replicas to handle many querying users.
- Great when you have way more reads than writes.

  <img width="300" height="160" alt="image" src="https://github.com/user-attachments/assets/05ee43bf-a7ca-44d4-bb20-e17f3926663d" />

One catch: With ACID transactions, a write transaction isn't complete until it's written to both the primary and the replica. This adds some transaction latency.

Bottom line: Read replicas help you scale reads separately from writes. Use them when you have a disproportionate number of read operations compared to writes.

### Understanding write ahead logging

A write-ahead log (WAL) is an append-only log that records atomic changes to the database. It helps implement ACID transactions (especially atomicity and durability) and is also used to create read replicas.

Why WAL exists:

Normally, writing to a database is slow – you have to position data correctly (row or column storage), update indexes, and do many steps. WAL avoids this by doing a fast sequential write to a log file. The data isn't in its final query-ready form, but it's safely stored in persistent storage very quickly.

Two main benefits of WAL:
1) Recovery – if the database crashes mid-transaction, WAL helps recover.
2) Read replicas – WAL files can be shipped to replicas.
   
   <img width="400" height="140" alt="image" src="https://github.com/user-attachments/assets/685ffb88-d1cd-4f3c-909a-b36cc7a107eb" />
   vs <img width="400" height="140" alt="image" src="https://github.com/user-attachments/assets/cb53fdc0-ba8d-4914-8f24-d6e7c6b3e2f4" />


Sync options when using WAL for replicas:
| Option | Write Performance | Data Loss Risk |
| :--- | :---: | :---: |
| Asynchronous write | Highest | Highest |
| Synchronous write | Medium | Medium |
| Synchronous apply | Lowest | Lowest |
- Async – data written to WAL on primary only. Fastest, but riskiest.

- Sync write – WAL written on both primary and replica. Data on replica not yet queryable, but safe.

- Sync apply – WAL written on both, and replica data is already structured and queryable. Safest but slowest.

Bottom line: WAL trades immediate query-readiness for fast writes. When using replicas, you choose sync options based on your tolerance for data loss vs. write performance.

### Denormalizing for analytical queries

**Normalization (OLTP)**

**Normalized data** models are standard for transaction processing systems. They typically use third normal form (3NF) – "the key, the whole key, and nothing but the key." Every column in a row must relate directly to the primary key.

Why normalize? To avoid data anomalies:

- Insertion anomalies (can't add data without a key)

- Update anomalies (redundant data causes inconsistencies)

- Deletion anomalies (losing data when deleting something else)

**Normalization** lets you model complex relationships (one-to-one, one-to-many, one-to-zero) and isolate data that changes at different rates. For example, a customer's name stays stable, but their address changes over time. Normalization handles this cleanly.

**The trade-off:** Normalization is accurate and safe, but can be slow for analytical queries that need to scan large volumes of data and join many tables.

**Denormalization for Analytics (OLAP)**

For analytical systems, we often denormalize. The classic pattern is the star schema.

Fact table:

- Large table, often millions or billions of rows

- Stores measures – quantifiable metrics like "products sold" or "average margin"

- Usually includes a foreign key to each dimension and a timestamp

**Dimension tables:**

- Smaller tables that provide context

- Examples: time dimension (date, day of week, month, quarter), geography dimension (country, region, store), product dimension, channel dimension

- Contain descriptive attributes that answer "where, when, what, who"

Why **star schema** performs better:

- Dimension tables only join to the fact table – not to each other

- Simple, predictable join patterns

- Database optimizers can be tuned specifically for star joins

- Some databases (like ClickHouse, BigQuery, Snowflake) have star-schema-specific optimizations

| When to use which | Normalized (3NF) | Star Schema (Denormalized) |
| :--- | :--- | :--- |
| **Best for** | Transaction processing (OLTP) | Analytics (OLAP) |
| **Goal** | Avoid anomalies, data integrity | Query speed on large volumes |
| **Join complexity** | Many-to-many, complex | Simple fact-to-dimension |
| **Storage** | Less redundant | More redundant |
| **Write performance** | Good | Slower (but analytics is read-heavy) |

**Bottom line:** **Normalize** for transactional systems where data integrity matters most. **Denormalize** into star schemas for analytical systems where query performance on large data volumes is the priority. You can't have both – it's a trade-off.


### Aggregation and sampling for analytical queries 

**Aggregation**

Great for time series data. Recent data is often needed in fine detail (seconds). Older data is still useful, but query patterns change – we usually want aggregates (minutes, hours, days) rather than raw detail.

If your use cases allow it, you can store only coarser aggregates over time. For example: keep seconds for a week, then minutes, then only days after a year. This reduces storage and speeds up reads because there's less data to scan.

You can also keep both raw and aggregated data if you need both detailed drill-downs and fast aggregate queries.

Trade-off: Aggregation gives faster reads at the cost of losing fine detail. Not suitable when you need raw data for ML training or investigating old anomalies.

**Sampling**

Instead of reading all data, read a representative sample. Like election polls – you don't ask every voter, just a good sample.

This is called approximate query processing. You trade accuracy for speed and compute resources. You might not get the exact number, but you get something very close.

Good when you don't need 2–3 decimal places of precision. Your action based on the result stays the same.

Implementation:

- Some databases have built-in approximate functions (BigQuery, ClickHouse – e.g., topK)

- Extensions to SQL with error tolerance and confidence intervals

Bottom line: Use aggregation to reduce data volume for older time series. Use sampling when you can accept near-enough answers for much faster performance. Both are trade-offs – accuracy/ detail vs. speed/resources.

## DevOps for Scalable Relational Databases
### Monitoring relational databases 

Database monitoring is crucial after your database is in production. It helps you detect problems and understand what's happening.

What to **monitor**:

<img width="300" height="280" alt="image" src="https://github.com/user-attachments/assets/6fa78470-6d67-4bb8-b9b2-21fa3d83be63" />
<img width="200" height="280" alt="image" src="https://github.com/user-attachments/assets/a6263204-f7b8-4a65-acbe-8c273978be81" />

- Resource consumption – CPU, memory, disk space, network. Track trends so you can add resources before you run out.

- Top queries – A small set of queries often consumes most resources. Identify and tune them. In Postgres, pg_stat_statements shows query frequency, execution time, and blocks read/written.

- Throughput – Work completed over time (e.g., transactions per second, active connections, queue length). Queue length indicates backlog – tells you where you need more resources.

- Changes to the database – Schema changes (migrations), unexpected data volume spikes, access control changes. Use schema migration scripts to apply changes consistently across environments.

- One-time changes – Merging databases, migrating from legacy systems. Monitor these carefully because they're unusual and may behave unexpectedly.

- Security changes – Role changes, permission changes. Use audit logs to track them.

**Metrics vs. logs:**

- Metrics tell you something is wrong (e.g., CPU spike, disk almost full). They don't tell you why.

- Logs tell you why. They have detailed event information from the DBMS, OS, and applications. For complex problems, you may need to look at multiple logs – consolidated logging helps.

**Dashboards:**

Tools like Grafana and Superset help visualize metrics – top queries, active connections, throughput, etc.

Bottom line: Metrics alert you to problems. Logs help you find the root cause. Both are essential.


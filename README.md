# Designing-Scalable-and-Available-SQL-DBs
[course link](https://www.linkedin.com/learning/designing-highly-scalable-and-highly-available-sql-databases)

author:  [Dan Sullivan](https://www.linkedin.com/in/dansullivanpdx/)

Data Architect, Author, and Instructor 


### Lecture Notes

#### Learning about business requirements for database scalibility

    Start by understanding the specific business requirements and use cases for the database, including what data you’ll work with and how it’s structured (structured, semi-structured, or unstructured).
    Consider data volume, ingestion rate, and expected growth over time to plan for scalability.
    Think about the data lifecycle, including how long data needs to be retained and compliance requirements like GDPR.
    Understand how the data will be used—whether for transactional processing with low latency needs or analytical decision-making with large queries.
    Identify key domain entities and their attributes, keeping in mind that data models may evolve as business needs change.
<img width="1257" height="750" alt="image" src="https://github.com/user-attachments/assets/ddba8247-80d0-4183-8c0c-1eff8d852bd9" />

#### Identifying use cases for data

    
    Data use cases involve understanding the data lifecycle—how data is created, processed, analyzed, archived, reused, or deleted—and the workloads that describe how data is ingested, stored, and queried.
    Different use cases like sales transactions, equipment monitoring, and customer engagement have distinct data characteristics and access patterns, influencing database design.
    Workloads are multi-step and interdependent, involving various processes beyond just the database, such as services running in containers or cloud environments.
    This understanding is crucial for designing databases that are both scalable and highly available to meet diverse business needs.
<img width="1132" height="219" alt="image" src="https://github.com/user-attachments/assets/97a81a2b-fe48-454f-ba80-f6aa399bdaa7" />

    
    

    

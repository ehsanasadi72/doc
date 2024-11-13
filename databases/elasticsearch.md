# **Introduction to Elasticsearch**
### Key Features and Benefits
-  **Distributed Architecture**: Elasticsearch can scale horizontally by adding more nodes, ensuring high availability and fault tolerance.
- **Real-Time Search and Analytics**: Provides near-instantaneous search and data analysis, making it ideal for applications requiring quick data retrieval.
- **Full-Text Search**: Supports complex queries, including fuzzy search, partial matching, and relevance scoring.
- **RESTful API**: Interact with Elasticsearch via simple HTTP requests, making integration with various applications easy.
- **Schema-Free**: Automatically detects the structure of JSON documents and indexes data accordingly, allowing for flexible data storage.
- **Built-in Aggregations**: Perform powerful data analysis using metrics and bucket aggregations for insights and reporting.
- Use Cases (e.g., search engines, logging, analytics)

# Concepts
### 1. Indexes

An index in Elasticsearch is a group of related documents stored together. It's similar to a database in traditional systems. Each index can hold different types of data and comes with specific features to organize and search that data efficiently.

#### Index Structure ==(coming soon)==
- Documents, 
- Fields
- Data Types
- Mapping
- Dynamic vs. Explicit Mapping.
#### What's happening in creating an Index Querying and Aggregations ==(coming soon)==


### 2. Sharding ==(coming soon)==

### 3. Replication ==(coming soon)==

### 4. Cluster node types

- **Master Node:** 
	Responsible for managing the cluster’s overall state. It controls other nodes, assigns tasks, and monitors the cluster. Every cluster must have at least one master node, but usually, three are set up to prevent issues if one fails.

- **Data Node:**
	Handles storing and searching data. It saves data in shards and performs search and analysis operations. Having more data nodes increases storage capacity and improves search performance.

- **Coordinating Node:**
	Acts as a middleman, receiving search and write requests from users and distributing them to the appropriate nodes. If a node doesn’t have a specific role, it acts as a coordinating node by default.

- **Ingest Node:**
	Pre-processes data before it’s stored in Elasticsearch. For example, it can filter, transform, or process the data before indexing.

- **Voting-only Node:**
	Only participates in master node elections. It doesn’t handle data storage or manage the cluster.

- **Machine Learning Node:**
    Processes machine learning tasks, usually for analyzing and making sense of the data.


### 5. Index Management

- ####  Index Lifecycle Management (ILM)
	1. **Hot:** In this phase, indexes are active, and both write and search operations are performed regularly.
	2. :**Warm::** In this phase, indexes are used less frequently and may be moved to nodes with fewer resources. Search operations are still possible, but no more data is written.
	3. :**Cold:**: In this phase, indexes are rarely accessed. The data is compressed and moved to nodes with minimal resources to reduce storage costs.
	4. :**Delete::** Finally, after a specified time, the indexes are no longer needed and are deleted to free up storage space.
    

- #### Snapshot Lifecycle Management (SLM)
  in Elasticsearch helps you automatically manage backups of your data. You can set up policies to take regular snapshots of your indexes, store them in a specified location, and automatically delete old snapshots to save space. This way, you can easily restore your data if needed, without manual intervention.
  
## 6. Fleet Architecture in Elasticsearch  ==(coming soon)==

 

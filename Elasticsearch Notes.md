
## What Is Elasticsearch ? 

- Elasticsearch is an open-source data search and analysis platform that enables you to perform data search, analysis, and visualization quickly and effectively. 
- Elasticsearch can be considered a fast and scalable database and search engine (full-text search) capable of storing large amounts of data in an organized manner.

## Advantages of Elasticsearch

**High Performance:**

- Using the Apache Lucene framework, Elasticsearch provides fast and accurate search results through reverse indexing and advanced search algorithms. It is faster than a typical SQL database.

**Near Real-Time Operations:**

- Elasticsearch operations, such as data reading or writing, are typically completed in less than a second. Therefore, Elasticsearch is beneficial for near real-time use cases like application monitoring and anomaly detection.

**Lots of Search Options:**

- Elasticsearch offers many features for search capabilities. You can get full-text search, auto-complete, instant search, and more. Autocompletion and instant search provide suggestions as you type, predicting based on search history or relevance. Even if there are spelling errors, users receive relevant search results.

**Distributed Approach:**

- Elasticsearch operates in a distributed architecture, enabling the processing of large amounts of data quickly. Indices are divided into shards, each functioning as a fully operational index. Each shard can have multiple replicas, which can be hosted anywhere within the Elasticsearch cluster.

**Cluster and Backup Support:**

- Elasticsearch can operate within a cluster composed of multiple nodes. This is important for providing high availability and preventing data loss. Additionally, it offers a comprehensive system for data backups.

**Plugins and Integrations:**

- Elasticsearch is highly compatible with plugins and integrations. Plugins are used to enhance functionality and customize searches. They assist in adding custom mappings, analyzers, and discoveries.

**RESTful API:**

- Elasticsearch’s simple REST-based APIs allow you to quickly start using the service and design applications suitable for various use cases.

**Security:**

- Elasticsearch supports security measures such as user authentication, access control, and data encryption.

**Easy Application Development:**

- It supports easy application development for many languages including Java, Python, PHP, JavaScript, Node.js, Ruby, and more.

## Terminology

- **Full Text Search**

	- In Elasticsearch, full text search refers to the capability to search for words and phrases across all fields in a document or a set of documents. It involves analyzing and indexing textual content in a way that allows efficient and accurate searching. Elasticsearch uses various techniques such as tokenization, stemming, and relevance scoring (using algorithms like BM25) to perform full text search effectively.
	
		Key aspects of full text search in Elasticsearch include:
		
		- **Tokenization:** Breaking down text into individual tokens (words or terms).
		- **Stemming:** Reducing words to their root form to improve matching (e.g., "running" to "run").
		- **Relevance Scoring:** Assigning scores to documents based on how well they match the search query.
		- **Phrase Matching:** Supporting searches for exact phrases as well as individual terms.
		- **Analysis:** Applying text analyzers to preprocess text data for indexing and searching.

- **Node:**
    
    - Each node in an Elasticsearch cluster can be configured to perform specific roles. For example:
        - **Master Node:** Manages the cluster and handles tasks such as creating or deleting indices, tracking which nodes are part of the cluster, and determining which shards should be allocated to which nodes.
        - **Data Node:** Stores data and executes data-related operations such as CRUD, search, and aggregations.
        - **Client Node (Coordinating Node):** Routes requests to the appropriate data nodes and consolidates results. These nodes do not hold data themselves.
- **Primary Shard:**
    
    - When an index is created, it can be split into a number of primary shards. For example, an index with 5 primary shards will distribute its data across these 5 shards. Each primary shard can reside on different nodes within the cluster. The primary shard handles the initial indexing operation and any subsequent updates to the documents.
- **Replica Shard:**
    
    - Each primary shard can have zero or more replicas. Replicas serve as backups for primary shards and also help distribute the search load. For example, if a primary shard has 2 replicas, there will be 2 additional copies of the data stored on different nodes. This ensures that if the node containing the primary shard goes down, the cluster can still function and serve data from the replicas.
- **Cluster:**
    
    - A cluster is the overarching system that coordinates the operations of multiple nodes. It provides fault tolerance and high availability by distributing data and requests across nodes. If a node fails, other nodes in the cluster can take over its responsibilities. The cluster state, which includes information about all nodes and shards, is managed by the master node. This ensures that the system operates seamlessly, even in the presence of node failures or changes in the cluster topology.
- **Index = Database:**
	
	- In Elasticsearch, an index is the unit where data is stored in an organized manner and typically represents a collection of related documents. For instance, in a library system, you could create a "books" index where all the books are stored. An index usually contains documents that are related to each other. For example:
```json
    {
        "id": 1,
        "title": "Java SE",
        "content":  "Java yazılım dili, platform bağımsız ilk yazılım dilidir."
    }
```

- **Document = Row:**

	- A document is a basic unit of information that can be indexed in Elasticsearch. It is a collection of fields, which are key-value pairs. Each document is a JSON object and can be thought of as a single record in an index.

- **Field = Column:**

	- A field is a key-value pair within a document. Each field has a name and a value, where the value can be of various data types like text, number, date, etc.

- **Data Stream:**

	- A data stream in Elasticsearch is a continuous, append-only collection of time-series data, typically used for logging, metrics, and other time-based data. It is designed to handle data that arrives continuously and is ingested into Elasticsearch in a time-ordered manner.
	    - **Time-Based Data:** Optimized for data with timestamps.
	    - **Write-Only Behavior:** Append-only, ensuring immutability.
	    - **Backing Indices:** Composed of multiple hidden indices.
	    - **Automatic Index Management:** Handles creation, rollover, and deletion of indices based on policies.
	    
- **Text Analyzing:**
	
	- Text analyzing in Elasticsearch involves processing text data to make it searchable and retrievable. It includes several steps to convert raw text into a format suitable for search and analysis.
	    - **Tokenization:** Breaking down text into individual terms or tokens. For example, "Java is great" becomes ["Java", "is", "great"].
	    - **Lowercasing:** Converting all tokens to lowercase to ensure case-insensitive search. For example, "Java" and "java" are treated the same.
	    - **Stemming/Lemmatization:** Reducing words to their root form. For example, "running" becomes "run".
	    - **Removing Stop Words:** Removing common words that do not contribute much to the search relevance, such as "is", "the", "and".
	    - **Synonyms:** Expanding terms to include synonyms to improve search matching. For example, "quick" and "fast" can be treated as equivalents.
	    - **Custom Analyzers:** Creating custom analyzers by combining different text processing steps tailored to specific use cases.

- **Inverted Index:**
	
	- An inverted index is the data structure used by Elasticsearch to make search operations fast and efficient. It maps terms to the documents that contain them, allowing for quick full-text searches.
	    - **Terms:** The individual words or tokens extracted from documents during text analysis.
	    - **Document IDs:** Unique identifiers for each document containing a given term.
	    - **Mapping Terms to Documents:** The inverted index stores a list of document IDs for each term, making it easy to find all documents that contain a specific term. For example, if the term "Java" appears in documents with IDs 1, 2, and 5, the inverted index entry for "Java" will point to [1, 2, 5].
	    - **Efficient Searches:** By looking up terms in the inverted index, Elasticsearch can quickly identify and retrieve relevant documents, significantly speeding up search queries compared to scanning all documents sequentially.

- **Mapping:**
	
	- Mapping in Elasticsearch defines how documents and their fields are stored and indexed. It specifies the data type of each field and how the field should be analyzed and indexed. Mapping allows Elasticsearch to understand the structure and properties of the data in each index.
	    - **Field Data Types:** Defines whether a field contains text, numbers, dates, or other types of data.
	    - **Analysis:** Specifies how text fields should be analyzed during indexing and searching (e.g., tokenization, stemming).
	    - **Index Options:** Controls whether and how a field is indexed for search purposes (e.g., analyzed, not_analyzed).
	    - **Mapping Properties:** Defines additional settings such as whether a field is searchable, aggregatable, or stored separately.
	    - **Dynamic Mapping:** Automatically detects field data types and applies default mappings based on the data inserted into Elasticsearch.
	    - **Explicit Mapping:** Allows users to explicitly define mappings for fields, providing more control over how data is indexed and searched. 
```json
PUT /product
{
  "mappings": {
    "properties": {
      "title": {
        "type": "text"
      },
      "description": {
        "type": "text"
      },
      "price": {
        "type": "float"
      },
      "stock_count": {
        "type": "integer"
      },
      "is_active": {
        "type": "boolean"
      },
      "created_at": {
        "type": "date"
      }
    }
  }
}
```

- **Relevancy**

	- In Elasticsearch, relevancy is a relationship score value. Search results are ranked from the most relevant to the least relevant. This score is determined using the Best Match 25 (BM25) relevancy algorithm.


## Document Management

**Creating Document**

```json
PUT customer/_doc/1
{
  "id" : 1,
  "name" : "deniz",
  "isActive" : true,
  "contact" : {
    "address" : "Istanbul",
    "phone" : "0555 555 55 55"
  }
}
```

**Update Document**

```json
POST customer/_update/1 
{
  "doc": {
    "contact" : {
      "phone" : "0555 777 77 77"
    }
    
  }
}
```

**Delete Document**

```json
DELETE musteri/_doc/1
```

**Get Document**

```json
GET musteri/_doc/1

GET musteri/_source/1 // without metadata
```

## Query Types

**Match Query**

Searches for a specific text term or query expression and returns matching documents.

```json
POST kibana_sample_data_ecommerce/_search
{
  "query": {
    "match": {
      "customer_first_name.keyword": {
        "value": "Deniz"
      }
    }
  }
}
```

**Prefix Query**

Used to search for terms starting with a specific prefix.

```json
POST kibana_sample_data_ecommerce/_search
{
  "query": {
    "prefix": {
      "customer_first_name.keyword": {
        "value": "Ja"
      }
    }
  }
}
```

**Range Query**

Checks if a field falls within a specified range.

```json
{
  "query": {
    "range": {
      "products.base_price": {
        "gte": 1,
        "lte": 1000
      }
    }
  }
}
```

**Wildcard Query**

Used to find terms matching a pattern using wildcard characters (* or ?).

```json
// wildcard
POST kibana_sample_data_ecommerce/_search
{
  "query": {
    "wildcard": {
      "customer_first_name.keyword": {
        "value": "*e"
      }
    }
  }
}
```

**Fuzzy Query**

Used to search for similar but not exact terms.

```json
POST kibana_sample_data_ecommerce/_search
{
  "query": {
    "fuzzy": {
      "customer_first_name.keyword": {
        "value": "ane",
        "fuzziness": 2
      }
    }
  }
}
```

**Pagination**

```java
POST kibana_sample_data_ecommerce/_search
{
  "size": 2, 
  "from": 0, 
  "query": {
    "prefix": {
      "customer_first_name.keyword": {
        "value": "Ja"
      }
    }
  }
}
```

**Sorting**

```java
// Sorting
POST kibana_sample_data_ecommerce/_search
{
 "sort": [
   {
     "create_date": {
       "order": "desc"
     }
   }
 ], 
  "query": {
    "prefix": {
      "customer_first_name.keyword": {
        "value": "Ja"
      }
    }
  }
}
```

### Full Text Query

Used to search for similar but not exact terms.

**Full Text Match Query**

```json
POST kibana_sample_data_ecommerce/_search
{
  "query": {
    "match": {
      "customer_full_name": "Diane Alvarez"
      
    }
  }
}
```

**Full Text Multi Match Query**

```java
POST kibana_sample_data_ecommerce/_search
{
  "query": {
    "multi_match": {
      "query": "ri",
      "fields": ["customer_first_name","customer_last_name"],
      "fuzziness": 2
    }
  }
}
```

**Full Text  Match Phrase Query**

```json
POST kibana_sample_data_ecommerce/_search
{
  "query": {
    "match_phrase": {
      "products.category": {
        "query": "Women's Clothing",
        "slop": 2 // araya gırılecek kelıme    
      }
    }
  }
}
```

**Full Text Match Boolean Prefix**

```json
POST kibana_sample_data_ecommerce/_search
{
  "query": {
    "match_bool_prefix": {
      "customer_full_name" : {
        "query" : "De"
      }
    }
  }
}
```

### Aggregations

Used to collect, group, and analyze data.

**Metric Aggregation**

```json
GET kibana_sample_data_ecommerce/_search
{
  "aggs": {
    "MAHMUT": { // can be everything,
      "stats": {
        "field": "products.base_unit_price"
      }
    }
  }
}
```


**Bucket Aggregation**

```json
GET kibana_sample_data_ecommerce/_search
{
  "aggs": {
    "BUCKET": { // can be everything,,
      "terms": {
        "field": "products.category.keyword",
        "order": {
          "_count": "desc"
        }
      }
      
    }
  }
}
```

**Global Aggregation**

```json
GET kibana_sample_data_ecommerce/_search
{
  "query": {
    "term": {
      "products.category.keyword": {
        "value": "Men's Clothing"
      }
    }
  },
  "aggs": {
    "all_docs": {
      "global": {},
      "aggs": {
        "avg_base_price": {
          "avg": {
            "field": "products.base_price"
          }
        }
      }
    },
    "active_men_avg_price" : {
      "avg": {
        "field": "products.base_price"
      }
    }
  }
}
```


## Difference Between Keyword And Text Types

- **Keyword Data Type:**

	 The "keyword" data type stores data in its original form without applying any analysis. This allows the data to be stored exactly as entered and is suitable for exact match queries (term queries). It is particularly useful for structured or key-based values such as email addresses, SKU numbers, country codes, etc.

- **Text Data Type:**

	The "text" data type applies text analysis to the data before indexing. It separates words or terms, converts them to lowercase, and removes special characters. Text fields enable word-based searches and can retrieve results without exact matches, making text content more searchable. It is suitable for fields where textual content needs to be searchable, such as article text or user description fields.

## Docker Install

```shell
docker run -d --name elastic --net elb-network -p 9200:9200 -p 9300:9300 -e "xpack.security.enabled=false" -e "xpack.security.transport.ssl.enabled=false" -e "xpack.security.enrollment.enabled=true" -e "discovery.type=single-node" -e "ELASTIC_USERNAME=admin" -e "ELASTIC_PASSWORD=admin" -e "ES_JAVA_OPTS=-Xms512m -Xmx1024m" elasticsearch:8.12.1

docker run -d --name kibana --net elb-network -p 5601:5601 -e "ELASTICSEARCH_HOSTS=http://elastic:9200" docker.elastic.co/kibana/kibana:8.12.1
```


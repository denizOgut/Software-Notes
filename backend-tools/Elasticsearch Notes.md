
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

![[Pasted image 20240620220310.png]]

- **Full Text Search**

	- In Elasticsearch, full text search refers to the capability to search for words and phrases across all fields in a document or a set of documents. It involves analyzing and indexing textual content in a way that allows efficient and accurate searching. Elasticsearch uses various techniques such as tokenization, stemming, and relevance scoring (using algorithms like BM25) to perform full text search effectively.
	
		Key aspects of full text search in Elasticsearch include:
		
		- **Tokenization:** Breaking down text into individual tokens (words or terms).
		- **Stemming:** Reducing words to their root form to improve matching (e.g., "running" to "run").
		- **Relevance Scoring:** Assigning scores to documents based on how well they match the search query.
		- **Phrase Matching:** Supporting searches for exact phrases as well as individual terms.
		- **Analysis:** Applying text analyzers to preprocess text data for indexing and searching.

- **Node:**
	- **Running instance of Elasticsearch**
    - Each node in an Elasticsearch cluster can be configured to perform specific roles. For example:
        - **Master Node:** Manages the cluster and handles tasks such as creating or deleting indices, tracking which nodes are part of the cluster, and determining which shards should be allocated to which nodes.
        - **Data Node:** Stores data and executes data-related operations such as CRUD, search, and aggregations.
        - **Client Node (Coordinating Node):** Routes requests to the appropriate data nodes and consolidates results. These nodes do not hold data themselves.

- **Shard**
	- Shard keeps documents. It is single Lucene instance, a low-level “worker” unit managed automatically by Elasticsearch. Shards types are **primary** and **replica**
        
	- **Primary Shard:**
	    
	    - When an index is created, it can be split into a number of primary shards. For example, an index with 5 primary shards will distribute its data across these 5 shards. Each primary shard can reside on different nodes within the cluster. The primary shard handles the initial indexing operation and any subsequent updates to the documents.
	    
	- **Replica Shard:**
	    
	    - Each primary shard can have zero or more replicas. Replicas serve as backups for primary shards and also help distribute the search load. For example, if a primary shard has 2 replicas, there will be 2 additional copies of the data stored on different nodes. This ensures that if the node containing the primary shard goes down, the cluster can still function and serve data from the replicas.
    
- **Cluster:**
    
    - A cluster is the overarching system that coordinates the operations of multiple nodes. It provides fault tolerance and high availability by distributing data and requests across nodes. If a node fails, other nodes in the cluster can take over its responsibilities. The cluster state, which includes information about all nodes and shards, is managed by the master node. This ensures that the system operates seamlessly, even in the presence of node failures or changes in the cluster topology.
    - **Contains of one or more nodes with the same cluster name.**
    
- **Index = table:**
	-  An index is a logical namespace that manages one or more primary shards and zero or more replica shards
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
	-  Inverted index is a form of a hashtable, where **key is a term** and value, in simplification, is a **list of documents**. Inverted index converts query into a list of matched documents
	
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

## Search
### Search Phases

- **Send query**
	- Send to any node (it should different node each time)
- **Distribute query**
	- Distribute query to all nodes that keep primary or replica shards of queried indices. Can be different set
	- of nodes each time (adaptive replica selection)
- **Process query**
	- Each node processes query separately in isolation from others
- **Return partial results**
	- Partial results are returned to the node that distributed the query
- **Merge results**
	- Merge partial results into single response, then sort, limit to the limit requested by user, highlight etc.)
- **Return response**
	- Return full response to the client

### General Search Rules

➔ **Send query to different node each time**
	Overall search performance is as fast as the slowest node involved in the process, so causing a heavy load on one node will slow down the cluster

➔ **Pagination is mandatory**
	Elasticsearch can query tons of data in ms, but returned data set must be small to keep the performance on a reasonable level
	
➔ Avoid querying with wildcards

## Difference Between Keyword And Text Types

- **Keyword Data Type:**
	- Used for sorting, aggregating and exact search. In most cases text without spaces can be treated as a not analyzed text.
	
	 - The "keyword" data type stores data in its original form without applying any analysis. This allows the data to be stored exactly as entered and is suitable for exact match queries (term queries). It is particularly useful for structured or key-based values such as email addresses, SKU numbers, country codes, etc.

- **Text Data Type:**
	- Used for full text search, like Google

	- The "text" data type applies text analysis to the data before indexing. It separates words or terms, converts them to lowercase, and removes special characters. Text fields enable word-based searches and can retrieve results without exact matches, making text content more searchable. It is suitable for fields where textual content needs to be searchable, such as article text or user description fields.

Elasticsearch doesn't know how users will query the document (which field and how will be used for searching), so **it applies two text data types to the single JSON field** by using the **multi-field notation**

## Query DSL

➔ **Leaf query clauses**
	Simple queries used to search for a specific value in a particular field or fields. They rely on search structures like Inverted index (but not only) to find matching documents. Queries can be used by them self.

➔ **Compound query clauses**
	Wrap other leaf or other compound queries. They are used to combine multiple queries in a logical fashion using operands AND, OR, NOT (such as **bool** query) or to alter their behavior (such as **constant_score** query).

## Query Types

➔ **Match All Query**
	Simplest query, matches all documents
➔ **Term level queries**
	Term Query, Terms Query, Range Query, Prefix Query, Wildcard Query, Regexp Query, Ids Query
➔ **Full text queries**
	Match Query, Match Phrase Query, Multi Match Query, Query String Query
➔ **Geo queries**
	GeoShape Query, Geo Bounding Box Query, Geo Distance Query
➔ **Specialized queries**
	Script Query, Percolate Query
➔ **Span queries**
	Span Term Query, Span Near Query, Span Containing Query, …
➔ **Joining queries**
	Nested Query, Has Child Query, Has Parent Query
➔ **Compound queries**
	Constant Score Query, Bool Query, Boosting Query

**Match Query**
	Simplest query, matches all documents
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

```java
GET mylogs-apache-v1-2022.08.10/_search
{
  "query": {
    "term": {
      "agent": {
        "value": "mozilla"
      }
    }
  }
}

GET mylogs-apache-v1-2022.08.10/_search
{
  "query": {
    "match": {
      "agent": {
        "query": "Mozilla"
      }
    }
  }
}

GET mylogs-apache-v1-2022.08.10/_search
{
  "query": {
    "match": {
      "agent": {
        "query": "Mozilla",
        "analyzer": "default"
      }
    }
  }
}

GET mylogs-apache-v1-2022.08.10/_search
{
  "query": {
    "match": {
      "agent": {
        "query": "Mozilla Gecko/45",
        "analyzer": "default"
      }
    }
  }
}

GET mylogs-apache-v1-2022.08.10/_search
{
  "query": {
    "match": {
      "agent": {
        "query": "Mozilla Gecko/45",
        "analyzer": "default",
        "operator": "and"
      }
    }
  }
}

GET mylogs-apache-v1-2022.08.10/_search
{
  "query": {
    "bool": {
      "must": [
        {
          "term": {
            "agent": {
              "value": "mozilla"
            }
          }
        },
        {
          "term": {
            "agent": {
              "value": "gecko"
            }
          }
        },
        {
          "term": {
            "agent": {
              "value": "45"
            }
          }
        }
      ]
    }
  }
}

{
  "query": {
    "bool": {
      "should": [
        {
          "term": {
            "agent": {
              "value": "mozilla"
            }
          }
        },
        {
          "term": {
            "agent": {
              "value": "gecko"
            }
          }
        },
        {
          "term": {
            "agent": {
              "value": "45"
            }
          }
        }
      ],
      "minimum_should_match": 2
    }
  }
}

{
  "query": {
    "match": {
      "agent": {
        "query": "Mozilla Gecko/45",
        "analyzer": "default",
        "operator": "or",
        "minimum_should_match": 2
      }
    }
  }
}

{
  "query": {
    "match": {
      "agent": {
        "query": "Maazilla Gucko",
        "analyzer": "default",
        "operator": "or",
        "minimum_should_match": 2,
        "fuzziness": 2
      }
    }
  }
}

GET mylogs-apache-v1-2022.08.10/_search
{
  "query": {
    "match": {
      "agent": {
        "query": "Maazilla Gucko",
        "analyzer": "default",
        "operator": "or",
        "minimum_should_match": 2,
        "fuzziness": "AUTO",
        "max_expansions": 10,
        "fuzzy_rewrite": "top_terms_blended_freqs_10",
        "fuzzy_transpositions" : true,
        "prefix_length" : 4
      }
    }
  }
}
```

**Term Query**

```json
GET /_search
{
  "query": {
    "term": {
      "agent": {
        "value": "mozilla",
        "boost": 1.0
      }
    }
  }
}


POST documents-books-v1/_search?explain=false
{
  "_source": ["description" , "title"], 
  "query": {
    "bool": {
      "must": [
        {
          "term": {
            "description": {
              "value": "javascript"
            }
          }
        },
        {
          "term": {
            "title": {
              "value": "javascript",
              "boost": 100
            }
          }
        }
        
      ]
    }
  }
}
```

**Bool Query**

```json
1.

POST documents-books-v1/_search?explain=false
{
  "query": {
    "bool": {
      "must": [
        {
          "term": {
            "description": {
              "value": "javascript"
            }
          }
        },
        {
          "term": {
            "subtitle": {
              "value": "web"
            }
          }
        }
      ],
      "filter": [
        {
          "range": {
            "published": {
              "gte": "2012-07-01T00:00:00.000Z",
              "lte": "2023-12-01T00:00:00.000Z"
            }
          }
        }
      ]
    }
  }
}

2.
POST documents-books-v1/_search?explain=false
{
  "query": {
    "bool": {
      "must": [
        {
          "term": {
            "description": {
              "value": "javascript"
            }
          }
        },
        {
          "term": {
            "subtitle": {
              "value": "web"
            }
          }
        }
      ],
      "filter": [
        {
          "range": {
            "published": {
              "gte": "2012-07-01T00:00:00.000Z",
              "lte": "2023-12-01T00:00:00.000Z"
            }
          }
        }
      ],
      "must_not": [
        {
          "term": {
            "description": {
              "value": "experience"
            }
          }
        }
      ],
         }
  }
}

3.
POST documents-books-v1/_search?explain=false
{
  "query": {
    "bool": {
      "must": [
        {
          "term": {
            "description": {
              "value": "javascript"
            }
          }
        },
        {
          "term": {
            "subtitle": {
              "value": "web"
            }
          }
        }
      ],
      "filter": [
        {
          "range": {
            "published": {
              "gte": "2012-07-01T00:00:00.000Z",
              "lte": "2023-12-01T00:00:00.000Z"
            }
          }
        }
      ],
      "must_not": [
        {
          "term": {
            "description": {
              "value": "experience"
            }
          }
        }
      ]
    }
  },
  "sort": [
    {
      "onstock": {
        "order": "desc"
      }
    },
    {
      "_score": {
        "order": "desc"
      }
    }
  ]
}

4.
POST documents-books-v1/_search?explain=false
{
  "query": {
    "bool": {
      "must": [
        {
          "term": {
            "description": {
              "value": "javascript"
            }
          }
        },
        {
          "term": {
            "subtitle": {
              "value": "web"
            }
          }
        }
      ],
      "filter": [
        {
          "range": {
            "published": {
              "gte": "2012-07-01T00:00:00.000Z",
              "lte": "2023-12-01T00:00:00.000Z"
            }
          }
        }
      ],
      "must_not": [
        {
          "term": {
            "description": {
              "value": "experience"
            }
          }
        }
      ],
      "should": [
        {
          "term": {
            "instock": {
              "value": "true",
              "boost": 200
            }
          }
        }
      ]
    }
  }
}

5.
POST documents-books-v1/_search?explain=false
{
  "query": {
    "bool": {
      "must": [
        {
          "term": {
            "description": {
              "value": "javascript"
            }
          }
        },
        {
          "term": {
            "subtitle": {
              "value": "web"
            }
          }
        }
      ],
      "filter": [
        {
          "range": {
            "published": {
              "gte": "2012-07-01T00:00:00.000Z",
              "lte": "2023-12-01T00:00:00.000Z"
            }
          }
        }
      ],
      "must_not": [
        {
          "term": {
            "description": {
              "value": "experience"
            }
          }
        }
      ],
      "should": [
        {
          "term": {
            "instock": {
              "value": "true",
              "boost": 200
            }
          }
        },
        {
          "term": {
            "title": {
              "value": "spiderman"
            }
          }
        }
      ],
      "minimum_should_match": 2
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

```json
GET mylogs-apache-v2*/_search
{
  "query": {
    "prefix": {
      "agent": {
        "value": "fire"
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

```json
POST mylogs-apache-v1*/_search
{
  "query": {
    "bool": {
      "filter": [
        {
          "range": {
            "bytes": {
              "gte": 4000,
              "lte": 5000
            }
          }
        }
      ]
    }
  }
}

POST mylogs-apache-v1*/_search
{
  "query": {
    "bool": {
      "filter": [
        {
          "range": {
            "bytes": {
              "gte": 4000,
              "lte": 5000
            }
          }
        },
        {
          "range": {
            "@timestamp": {
              "gte": "2022-08-10T21:47:01.000Z",
              "lte": "2022-08-10T21:57:01.000Z"
            }
          }
        }
      ]
    }
  }
}

POST mylogs-apache-v1*/_search
{
  "query": {
    "bool": {
      "filter": [
        {
          "range": {
            "bytes": {
              "gte": 4000,
              "lte": 5000
            }
          }
        },
        {
          "range": {
            "@timestamp": {
              "gte": "now-2y/d",
              "lte": "now/d"
            }
          }
        }
      ]
    }
  }
}

POST mylogs-apache-v2*/_search
{
  "query": {
    "bool": {
      "filter": [
        {
          "range": {
            "bytes": {
              "gte": 4000,
              "lte": 5000
            }
          }
        },
        {
          "range": {
            "@timestamp": {
              "gte": "now-1y/d",
              "lte": "now/d"
            }
          }
        },
        {
          "range": {
            "clientip": {
              "gte": "6.13.17.170",
              "lte": "6.13.80.255"
            }
          }
        }
      ]
    }
  }
}


POST mylogs-apache-v1*/_search
{
  "query": {
    "bool": {
      "filter": [
        {
          "range": {
            "@timestamp": {
              "gte": "2022-08-10T21:47:01.000Z",
              "lte": "2022-08-10T21:57:01.000Z",
              "format": "dd/MM/yyyy"
            }
          }
        }
      ]
    }
  }
}

PUT vacations-calendar-v1
{
  "mappings": {
    "properties": {
      "employee" : { "type": "text" },
      "vacation" : {
        "type": "date_range"
      }
    }
  }
}


POST vacations-calendar-v1/_doc
{
    "employee" : "Mat",
    "vacation" : {"gte":"2020-01-04", "lte":"2020-01-07"}
}

POST vacations-calendar-v1/_search
{
  "query": {
    "bool": {
      "filter": [
        {
          "range": {
            "vacation": {
              "gte": "2020-01-05",
              "lte": "2020-01-10",
              "relation" : "INTERSECTS"
            }
          }
        }
      ]
    }
  }
}


POST test-range-relation-v1/_search
{
  "query": {
    "bool": {
      "filter": [
        {
          "range": {
            "timestamp": {
              "gte": "2020-01-03",
              "lte": "2020-01-08",
              "relation" : "WITHIN"
            }
          }
        }
      ]
    }
  }
}


POST test-range-relation-v1/_search
{
  "query": {
    "bool": {
      "filter": [
        {
          "range": {
            "timestamp": {
              "gte": "2020-01-05",
              "lte": "2020-01-06",
              "relation" : "CONTAINS"
            }
          }
        }
      ]
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

```json
GET mylogs-apache-v2*/_search
{
  "query": {
    "wildcard": {
      "agent": {
        "value": "*ire?ox"
      }
    }
  }
}
```

**Regexp Query**

```json
POST _bulk
{ "index" : { "_index" : "browsers-v1"} }
{ "agent" : "Phoenix 0.5" }
{ "index" : { "_index" : "browsers-v1"} }
{ "agent" : "Opera 10.5" }
{ "index" : { "_index" : "browsers-v1"} }
{ "agent" : "Mozilla 9" }
{ "index" : { "_index" : "browsers-v1"} }
{ "agent" : "Firefox 15" }
{ "index" : { "_index" : "browsers-v1"} }
{ "agent" : "Chromium 2023" }
{ "index" : { "_index" : "browsers-v1"} }
{ "agent" : "Chrome 26" }

POST browsers-v1/_search
{
  "_source": ["agent"], 
  "query": {
    "regexp": {
      "agent": "chrom[ie]+.*|[a-z]{6}x"
    }
  }
}
```

**Query String Query**

```json
GET mylogs-apache-v1-*/_search
{
  "query": {
    "query_string": {
      "query": "Mozilla Gecko/45",
      "default_field": "agent"
    }
  }
}

GET mylogs-apache-v1-*/_search
{
  "query": {
    "query_string": {
      "query": "(Mozilla AND Gecko) KONG",
      "default_field": "agent"
    }
  }
}

GET mylogs-apache-v1-*/_search
{
  "query": {
    "bool": {
      "must": [
        {
          "term": {
            "agent": {
              "value": "mozilla"
            }
          }
        },
        {
          "term": {
            "agent": {
              "value": "gecko"
            }
          }
        }
      ],
      "should": [
        {
          "term": {
            "agent": {
              "value": "45"
            }
          }
        }
      ]
    }
  }
}

GET mylogs-apache-v1-*/_search
{
  "query": {
    "query_string": {
      "query": "(Mozilla AND Gecko) KONG",
      "fields" : ["agent", "geoip.city_name"]
    }
  }
}

GET mylogs-apache-v1-*/_search
{
  "query": {
    "query_string": {
      "query": "(*ozilla AND *ecko) *ONG",
      "fields" : ["agent", "geoip.city_name"],
      "allow_leading_wildcard": false
    }
  }
}

GET mylogs-apache-v1-*/_search
{
  "query": {
    "query_string": {
      "query": "\"KHTML like Gecko FxiOS 9.0n6194.0\"",
      "fields" : ["agent", "geoip.city_name"]
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

```json
GET mylogs-apache-v1-*/_search
{
  "query": {
    "fuzzy": {
      "agent": {
        "value": "mazilla",
        "fuzziness": 1
      }
    }
  }
}

DELETE sample-index-v1
POST sample-index-v1/_doc?refresh=true
{
  "agent" : "Mozilla"
}
POST sample-index-v1/_doc?refresh=true
{
  "agent" : "Mozillaz"
}
POST sample-index-v1/_doc?refresh=true
{
  "agent" : "Mazilla"
}
POST sample-index-v1/_doc?refresh=true
{
  "agent" : "Mayalla"
}
POST sample-index-v1/_doc?refresh=true
{
  "agent" : "Mzoilla"
}
POST sample-index-v1/_doc?refresh=true
{
  "agent" : "Moilla"
}
POST sample-index-v1/_doc?refresh=true
{
  "agent" : "Firefox"
}

GET sample-index-v1/_search
{
  "query": {
    "fuzzy": {
      "agent": {
        "value": "mozillazzz",
        "fuzziness": 2
      }
    }
  }
}

GET sample-index-v1/_search
{
  "query": {
    "fuzzy": {
      "agent": {
        "value": "mozilla",
        "fuzziness": 2,
        "prefix_length": 2
      }
    }
  }
}

GET sample-index-v1/_search
{
  "query": {
    "fuzzy": {
      "agent": {
        "value": "mozilla",
        "fuzziness": 1,
        "prefix_length": 0,
        "max_expansions": 50,
        "transpositions": false
      }
    }
  }
}

GET sample-index-v1/_search
{
  "query": {
    "fuzzy": {
      "agent": {
        "value": "firefox",
        "fuzziness": 50
      }
    }
  }
}
```

➔ **Uses Levenshtein distance algorithm** 
	Calculates the number of one-character changes that need to be made to one string to make it the same as another string. Algorithm defines **4 type of operations**, where each has a weight equal to 1. The distance is **sum of operations multiplied by their weights**.
	
➔ Maximum allowed distance is 2
	Terms with a distance **higher than 2 are not considered** for matching

➔ Use AUTO mode when possible
	Simply, short terms up to 2 characters need to be identical, but longer ones may have one or two changes to be considered equal.

**Span Query

SpanQuery helps us create queries that return more natural results, closer to natural language expectations. A simple rule is used here, score higher documents where matched terms are close to each other and filter out documents where they are not.

```json

POST test-documents-v1/_doc
{
"title" : "Market condition in USA",
"content" : "Current condition of the Market in USA is lorem ipsum dolor sit amet, consectetur adipiscing elit. Suspendisse fermentum nec lacus nec hendrerit. Pellentesque tristique mattis sagittis. Vestibulum nec vestibulum odio. Integer eu diam urna. Mauris condimentum sapien magna, ac vehicula orci vulputate eget. Sed aliquam sem ut ultricies volutpat. Nullam metus lectus, consequat eget suscipit quis, suscipit sed felis. Sed id turpis dictum erat pretium lobortis. Duis id nisi id nisl imperdiet convallis. Donec dignissim, lorem vel facilisis commodo, risus ligula euismod tellus, vitae porttitor justo odio vel turpis. Donec molestie vitae dolor sit amet imperdiet. Import of goods from China impact the domestic id sapien convallis, aliquam risus ac, aliquet dolor. Suspendisse dolor arcu, viverra eget erat eget, elementum dignissim dolor. Proin cursus bibendum diam sit amet vulputate. Mauris malesuada maximus lorem, sit amet cursus quam faucibus non. Fusce malesuada magna ac erat blandit, quis cursus nibh eleifend. Suspendisse malesuada quis nisl eget aliquam. Morbi felis elit, dignissim non pharetra in, volutpat a enim. Cras tempus leo in metus placerat, eget egestas ante sagittis. Proin pretium diam sed nisi tincidunt, sed tincidunt ligula dictum. Etiam auctor fermentum est eu luctus. Phasellus tincidunt erat non enim imperdiet mattis."
}

POST test-documents-v1/_search
{
  "query": {
    "bool": {
      "must": [
        {
          "match": {
            "content": {
              "query": "Market condition USA"
            }
          }
        }
      ]
    }
  }
}

POST test-documents-v1/_search
{
  "query": {
    "bool": {
      "must": [
        {
          "match": {
            "content": {
              "query": "Market condition China"
            }
          }
        }
      ]
    }
  }
}

POST test-documents-v1/_search
{
  "query": {
    "bool": {
      "must": [
        {
          "span_near": {
            "clauses": [
              {
                "span_term": {
                  "content": {
                    "value": "market"
                  }
                }
              },
              {
                "span_term": {
                  "content": {
                    "value": "condition"
                  }
                }
              },
              {
                "span_term": {
                  "content": {
                    "value": "usa"
                  }
                }
              }
            ],
            "slop": 12,
            "in_order": true
          }
        }
      ]
    }
  }
}



POST test-documents-v1/_search
{
  "query": {
    "bool": {
      "must": [
        {
          "term": {
            "content": {
              "value": "market"
            }
          }
        },
        {
          "term": {
            "content": {
              "value": "condition"
            }
          }
        },
        {
          "term": {
            "content": {
              "value": "usa"
            }
          }
        }
      ], 
      "should": [
        {
          "span_near": {
            "clauses": [
              {
                "span_term": {
                  "content": {
                    "value": "market"
                  }
                }
              },
              {
                "span_term": {
                  "content": {
                    "value": "condition"
                  }
                }
              },
              {
                "span_term": {
                  "content": {
                    "value": "usa"
                  }
                }
              }
            ],
            "slop": 12,
            "in_order": false
          }
        }
      ],
      "minimum_should_match": 0
    }
  }
}
```

➔ **Search for terms that are close to each other**
	Define the **maximum number of different terms between** your search terms. Specify whether the **order of the terms** matters or not. Such queries are most commonly used to implement very specific queries on legal documents, PDF extracted text, HTML pages, patents etc.

**Geo Query**

```json
PUT /locations-v1/
{
  "mappings": {
    "properties": {
      "location" : {
        "type": "geo_point"
      }
    }
  }
}

POST /locations-v1/_doc
{
  "location": "POINT (21.0182 52.2471)",
  "name": "Restarurant #1"
}


POST /locations-v1/_doc
{
  "location": {
    "lat": 52.2471,
    "lon": 21.0182
  },
  "name": "Restarurant #1"
}


POST /locations-v1/_doc
{
  "location": [21.0182, 52.2471],
  "name": "Restarurant #1"
}

GET locations-v1/_search

POST mylogs-apache-v2*/_search
{
  "query": {
    "geo_distance": {
      "distance": "2km",
      "geoip.location": {
        "lat": 52.237049,
        "lon": 21.017532
      }
    }
  }
}

GET mylogs-apache-v2*/_search
{
  "query": {
    "bool": {
      "must": {
        "match_all": {}
      },
      "filter": {
        "geo_bounding_box": {
          "geoip.location": {
            "top_left": {
              "lat": 52.24,
              "lon": 21.01
            },
            "bottom_right": {
              "lat": 52.23,
              "lon": 21.02
            }
          }
        }
      }
    }
  }
}
```

**Nested Query**

```json
POST /sample-book-v1/_doc
{
  "title": "The great Elasticsearch",
  "publisher" : {
    "name" : "Manning Publications",
    "date" : "2022"
  },
  "author": [
    {
      "firstname": "Mike",
      "lastname": "Thomson"
    },
    {
      "firstname": "Joe",
      "lastname": "Black",
      "biography": "An American author of over 100 technical books"
    }
  ]
}

POST /sample-book-v1/_search
{
  "query": {
    "bool": {
      "must": [
        {
          "term": {
            "author.firstname": {
              "value": "mike"
            }
          }
        },
        {
          "term": {
            "author.lastname": {
              "value": "black"
            }
          }
        }
      ]
    }
  }
}

GET /sample-book-v1/_mapping

PUT /sample-book-v2/
{
  "mappings": {
    "properties": {
      "author": {
        "type": "nested",
        "properties": {
          "firstname": {
            "type": "text"
          },
          "lastname": {
            "type": "text",
            "fields": {
              "keyword": {
                "type": "keyword",
                "ignore_above": 256
              }
            }
          },
          "biography": {
            "type": "text"
          }
        }
      },
      "publisher": {
        "properties": {
          "date": {
            "type": "text"
          },
          "name": {
            "type": "text"
          }
        }
      },
      "title": {
        "type": "text"
      }
    }
  }
}

POST /_reindex?wait_for_completion=true
{
  "conflicts" : "proceed",
  "source": {
    "index": "sample-book-v1"
  },
  "dest": {
    "index": "sample-book-v2"
  }
}

POST /sample-book-v2/_search
{
  "query": {
    "nested": {
      "path": "author",
      "query": {
        "bool": {
          "must": [
            {
              "term": {
                "author.firstname": {
                  "value": "mike"
                }
              }
            },
            {
              "term": {
                "author.lastname": {
                  "value": "black"
                }
              }
            }
          ]
        }
      }
    }
  }
}

POST /sample-book-v2/_search
{
  "query": {
    "nested": {
      "path": "author",
      "query": {
        "bool": {
          "must": [
            {
              "term": {
                "author.firstname": {
                  "value": "joe"
                }
              }
            },
            {
              "term": {
                "author.lastname": {
                  "value": "black"
                }
              }
            }
          ]
        }
      }
    }
  },
  "sort": [
    {
      "author.lastname.keyword": {
        "order": "asc"
      }
    }
  ]
}

POST /sample-book-v2/_search
{
  "query": {
    "nested": {
      "path": "author",
      "query": {
        "bool": {
          "must": [
            {
              "term": {
                "author.firstname": {
                  "value": "joe"
                }
              }
            },
            {
              "term": {
                "author.lastname": {
                  "value": "black"
                }
              }
            }
          ]
        }
      }
    }
  },
  "sort": [
    {
      "author.lastname.keyword": {
             "order" : "asc",
             "nested": {
                "path": "author"
             }
          }
    }
  ]
}
```

➔ **No concept of nested objects in Lucene**
	By default, documents with **nested documents are flattened** by Elasticsearch. Flattening preserves all values **except information about relationships** between these values.
	
➔ **Special mapping required**
	Nested objects require defining field as a "nested" in the mapping, as well using special “nested” queries. This complicates building queries a little bit and makes them less understandable,
	
➔ **Hidden nested documents are stored together with root document**
	All of them are visible as a **single ID** and **counted as a single document** in the index statistics. They are stored in the same shard and accessed by **path equal to the field name**.

➔ **Nested query can cause performance issues**
	Support for nested documents is build on the top of the Lucene, so use it wisely. Only use nested data type when **relationships are really important** to your search use cases

**Reverse Search Query**

```json
POST _bulk
{ "index" : { "_index" : "alerts-ip-v1"} }
{ "ip" : "105.178.122.203", "comment": "Potentail fraud bot"}
{ "index" : { "_index" : "alerts-ip-v1"} }
{ "ip" : "141.82.136.83", "comment": "Alert!, Immediate action to Administrators"}


DELETE alerts-ip-v1

PUT /alerts-ip-v1
{
  "mappings": {
    "properties": {
      "comment": {
        "type": "text"
      },
      "clientip" : {
        "type": "ip"
      },
      "query": {
        "type": "percolator"
      }
    }
  }
}

POST alerts-ip-v1/_doc
{
  "query": {
    "term": {
      "clientip": {
        "value": "105.178.122.203"
      }
    }
  },
  "comment": "Potentail fraud bot"
}

POST alerts-ip-v1/_doc
{
  "query": {
    "term": {
      "clientip": {
        "value": "141.82.136.83"
      }
    }
  },
  "comment": "Alert!, Immediate action to Administrators"
}

GET alerts-ip-v1/_search


GET /alerts-ip-v1/_search
{
  "query": {
    "percolate": {
      "field": "query",
      "document": {
        "agent": "Mozilla",
        "verb": "POST",
        "bytes": 5082,
        "clientip": "23.235.12.45"
      }
    }
  }
}

GET /alerts-ip-v1/_search
{
  "query": {
    "percolate": {
      "field": "query",
      "document": {
        "agent": "Chrome",
        "verb": "GET",
        "bytes": 3564,
        "clientip": "141.82.136.83"
      }
    }
  }
}
```

➔ **Percolate Query is used for reverse search**

➔ **Special mapping is required**
	Fields where queries are indexed must be defined in the mapping as a special type: **percolator**

➔ **Decreased indexing throughput (in comparison to simple pooling solutions)**
	But, it reduces cluster load and allows defining unlimited and complex queries. Percolation against millions of complex queries is really fast and you don't have to create complex logic in your application or bash script.

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

Compute metrics on a set of documents. Most of them are equivalent of SUM, AVG, COUNT, MIN or MAX functions from the SQL world

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

```json
GET mylogs-apache-v2-2022.08.10/_search
{
  "query": {
    "bool": {
      "filter": [
        {
          "range": {
            "@timestamp": {
              "gte": "2022-08-10T15:00:00.000Z",
              "lte": "2022-08-10T15:10:00.000Z"
            }
          }
        }
      ]
    }
  }
}

GET mylogs-apache-v2-2022.08.10/_search
{
  "query": {
    "bool": {
      "filter": [
        {
          "range": {
            "@timestamp": {
              "gte": "2022-08-10T15:00:00.000Z",
              "lte": "2022-08-10T15:10:00.000Z"
            }
          }
        }
      ]
    }
  },
  "aggs": {
    "NAME": {
      "avg": {
        "field": "bytes"
      }
    }
  }
}

GET mylogs-apache-v2-2022.08.10/_search?size=0
{
  "query": {
    "bool": {
      "filter": [
        {
          "range": {
            "@timestamp": {
              "gte": "2022-08-10T15:00:00.000Z",
              "lte": "2022-08-10T15:10:00.000Z"
            }
          }
        }
      ]
    }
  },
  "aggs": {
    "NAME1": {
      "min": {
        "field": "bytes"
      }
    },
    "NAME2": {
      "max": {
        "field": "bytes"
      }
    },
    "NAME3": {
      "avg": {
        "field": "bytes"
      }
    }
  }
}

GET mylogs-apache-v2-2022.08.10/_search?size=0
{
  "query": {
    "bool": {
      "filter": [
        {
          "range": {
            "@timestamp": {
              "gte": "2022-08-10T15:00:00.000Z",
              "lte": "2022-08-10T16:10:00.000Z"
            }
          }
        }
      ]
    }
  },
  "aggs": {
    "NAME1": {
      "min": {
        "field": "bytes"
      }
    },
    "NAME2": {
      "max": {
        "field": "bytes"
      }
    },
    "NAME3": {
      "avg": {
        "field": "bytes"
      }
    },
    "NAME4": {
      "value_count": {
        "field": "bytes"
      }
    }
  }
}

POST _bulk
{ "index" : { "_index" : "transactions-books-v1"} }
{ "title" : "Elasticsearch in action", "payment" : "card", "type": "sale", "amount": 10.99 }
{ "index" : { "_index" : "transactions-books-v1"} }
{ "title" : "Fairy tales for all", "payment" : "cash", "type": "sale", "amount": 8.49 }
{ "index" : { "_index" : "transactions-books-v1"} }
{ "title" : "JavaScript", "payment" : "cash", "type": "sale", "amount": 11.00 }
{ "index" : { "_index" : "transactions-books-v1"} }
{ "title" : "Cooking for dummies", "payment" : "cash", "type": "refund", "amount": 5.99 }
{ "index" : { "_index" : "transactions-books-v1"} }
{ "title" : "Elasticsearch", "payment" : "cash", "type": "sale", "amount": 5.99 }
{ "index" : { "_index" : "transactions-books-v1"} }
{ "title" : "Query DSL", "payment" : "cash", "type": "sale", "amount": 8.99 }

POST transactions-books-v1/_search?size=0
{
    "query" : {
        "match_all" : {}
    },
    "aggs": {
        "profit": {
            "scripted_metric": {
                "init_script" : "state.transactions = []", 
                "map_script" : "state.transactions.add(doc['type.keyword'].value == \u0027sale\u0027 ? doc.amount.value : -1 * doc.amount.value)",
                "combine_script" : "double profit = 0; for (t in state.transactions) { profit += t } return profit",
                "reduce_script" : "double profit = 0; for (a in states) { profit += a } return profit"
            }
        }
    }
}

GET transactions-books-v1/_search?size=0
{
  "runtime_mappings": {
    "diff": {
      "type": "double",
      "script": {
        "source": "emit(doc['type.keyword'].value == \u0027sale\u0027 ? doc['amount'].value : -1 * doc['amount'].value)"
      }
    }
  },
  "aggs": {
    "NAME": {
      "sum": {
        "field": "diff"
      }
    }
  }
}


---------------------------------------------

POST /mylogs-apache-v2*/_search?size=0
{
  "query": {
    "match_all": {}
  },
  "aggs": {
    "NAME": {
      "terms": {
        "field": "verb"
      }
    }
  }
}

POST /mylogs-apache-v2*/_search?size=0
{
  "query": {
    "match_all": {}
  },
  "aggs": {
    "NAME": {
      "terms": {
        "field": "verb",
        "size": 10,
	      "order": { "_key": "asc" }
      }
    }
  }
}

GET mylogs-apache-v2-2022.08.10/_search?size=0
{
  "query": {
    "bool": {
      "filter": [
        {
          "range": {
            "@timestamp": {
              "gte": "2022-08-10T15:00:00.000Z",
              "lte": "2022-08-10T16:10:00.000Z"
            }
          }
        }
      ]
    }
  },
  "aggs": {
    "NAME": {
      "terms": {
        "field": "verb",
        "size": 10
      },
      "aggs": {
        "NAME1": {
          "min": {
            "field": "bytes"
          }
        },
        "NAME2": {
          "max": {
            "field": "bytes"
          }
        },
        "NAME3": {
          "avg": {
            "field": "bytes"
          }
        },
        "NAME4": {
          "value_count": {
            "field": "bytes"
          }
        }
      }
    }
  }
}

GET mylogs-apache-v2*/_search?size=0
{
  "query": {
    "match_all": {}
  },
  "aggs": {
    "NAME": {
      "histogram": {
        "field": "bytes",
        "interval": 50
      }
    }
  }
}

GET mylogs-apache-v2*/_search?size=0
{
  "query": {
    "match_all": {}
  },
  "aggs": {
    "NAME": {
      "histogram": {
        "field": "bytes",
        "interval": 200,
        "missing": 0,
        "offset": 2,
        "extended_bounds": {
          "min": 0,
          "max": 6000
        }
      }
    }
  }
}

GET mylogs-apache-v2*/_search?size=0
{
  "query": {
    "match_all": {}
  },
  "aggs": {
    "NAME": {
      "histogram": {
        "field": "bytes",
        "interval": 200,
        "missing": 0,
        "offset": 200,
        "hard_bounds": {
          "min": 4700,
          "max": 6000
        }
      }
    }
  }
}

GET mylogs-apache-v2*/_search?size=0
{
  "query": {
    "match_all": {}
  },
  "aggs": {
    "NAME": {
      "histogram": {
        "field": "bytes",
        "interval": 200,
        "missing": 0,
        "offset": 200,
        "hard_bounds": {
          "min": 4700,
          "max": 6000
        },
        "min_doc_count": 50,
        "keyed": true
      }
    }
  }
}

GET mylogs-apache-v2*/_search?size=0
{
  "query": {
    "match_all": {}
  },
  "aggs": {
    "NAME": {
      "date_histogram": {
        "field": "@timestamp",
        "interval": "10m"
      }
    }
  }
}

GET mylogs-apache-v2*/_search?size=0
{
  "query": {
    "match_all": {}
  },
  "aggs": {
    "NAME": {
      "geohash_grid": {
        "field": "geoip.location",
        "precision": 2,
        "bounds": {
          "top_left": "POINT (-121.7352672 49.9858749)",
          "bottom_right": "POINT (-64.5674731 33.8081914)"
        }
      }
    }
  }
}

GET mylogs-apache-v2*/_search?size=0
{
  "query": {
    "bool": {
      "filter": [
        {
          "term": {
            "geoip.country_name": "United States"
          }
        }
      ]
    }
  },
  "aggs": {
    "NAME": {
      "geohash_grid": {
        "field": "geoip.location",
        "precision": 4,
        "bounds": {
          "top_left": "POINT (-121.7352672 49.9858749)",
          "bottom_right": "POINT (-64.5674731 33.8081914)"
        }
      }
    }
  }
}


PUT /_bulk?refresh
{ "index" : { "_index" : "flight-routes-v1" } }
{ "origin": "NewYork", "destinations": ["Paris", "Amsterdam", "Boston", "London"]}
{ "index" : { "_index" : "flight-routes-v1" } }
{ "origin": "Paris", "destinations": ["London"]}
{ "index" : { "_index" : "flight-routes-v1" } }
{ "origin": "Amsterdam", "destinations": ["London", "Paris"]}
{ "index" : { "_index" : "flight-routes-v1" } }
{ "origin": "Boston", "destinations": ["NewYork"]}
{ "index" : { "_index" : "flight-routes-v1" } }
{ "origin": "London", "destinations": ["NewYork", "Barcelona"]}
{ "index" : { "_index" : "flight-routes-v1" } }
{ "origin": "Barcelona", "destinations": ["London","Amsterdam"]}

GET flight-routes-v1/_search?size=0
{
  "aggs": {
    "NAME": {
      "terms": {
        "field": "destinations.keyword",
        "size": 10
      }
    }
  }
}
          
GET /flight-routes-v1/_search?pretty
{
  "size": 0,
  "aggs" : {
    "interactions" : {
      "adjacency_matrix" : {
        "filters" : {
          "flights_to_NewYork" : { "term" : { "destinations.keyword" : "NewYork" }},
          "flights_to_Barcelona" : { "term" : { "destinations.keyword" : "Barcelona" }}
        }
      }
    }
  }
}

GET /flight-routes-v1/_search?pretty
{
  "size": 0,
  "aggs" : {
    "interactions" : {
      "adjacency_matrix" : {
        "filters" : {
          "flights_to_NewYork" : { "term" : { "destinations.keyword" : "NewYork" }},
          "flights_to_Barcelona" : { "term" : { "destinations.keyword" : "Barcelona" }}
        }
      },"aggs": {
        "NAME": {
          "top_hits": {
            "size": 10,
            "_source": {
              "includes": "origin"
            }
          }
        }
      }
    }
  }
}


PUT /_bulk?refresh
{ "index" : { "_index" : "access-rights-v1" } }
{ "user": "Alan", "service": ["apache"]}
{ "index" : { "_index" : "access-rights-v1" } }
{ "user": "Be", "service": ["ssh", "apache"]}
{ "index" : { "_index" : "access-rights-v1" } }
{ "user": "Celi", "service": ["sendmail"]}
{ "index" : { "_index" : "access-rights-v1" } }
{ "user": "Dan", "service": ["ssh"]}
{ "index" : { "_index" : "access-rights-v1" } }
{ "user": "Eli", "service": ["sendmail"]}
{ "index" : { "_index" : "access-rights-v1" } }
{ "user": "Fin", "service": ["apache","sendmail","ssh"]}

GET access-rights-v1/_search?size=0
{
  "aggs": {
    "NAME": {
      "terms": {
        "field": "service.keyword",
        "size": 10
      }
    }
  }
}

GET /access-rights-v1/_search?pretty
{
  "size": 0,
  "aggs" : {
    "interactions" : {
      "adjacency_matrix" : {
        "filters" : {
          "apache" : { "term" : { "service" : "apache" }},
          "ssh" : { "term" : { "service" : "ssh" }},
          "sendmail" : { "term" : { "service" : "sendmail" }}
        }
      }
    }
  }
}

GET /access-rights-v1/_search?pretty
{
  "size": 0,
  "aggs" : {
    "interactions" : {
      "adjacency_matrix" : {
        "filters" : {
          "apache" : { "term" : { "service" : "apache" }},
          "ssh" : { "term" : { "service" : "ssh" }},
          "sendmail" : { "term" : { "service" : "sendmail" }}
        }
      },"aggs": {
        "NAME": {
          "top_hits": {
            "size": 10,
            "_source": {
              "includes": "user"
            }
          }
        }
      }
    }
  }
}


-----------------------------------------------------------------------------
GET mylogs-apache-v2*/_search?size=0
{
  "size": 0,
  "aggs": {
    "NAME1": {
      "date_histogram": {
        "field": "@timestamp",
        "calendar_interval": "day"
      },
      "aggs": {
        "NAME2": {
          "max": {
            "field": "bytes"
          }
        }
      }
    },
    "summary_bytes_min": {
      "min_bucket": {
        "buckets_path": "NAME1>NAME2.value",
        "gap_policy": "skip"
      }
    }
  }
}

GET mylogs-apache-v2*/_search?size=0
{
  "size": 0,
  "aggs": {
    "NAME1": {
      "date_histogram": {
        "field": "@timestamp",
        "calendar_interval": "day",
        "min_doc_count": 100000
      },
      "aggs": {
        "NAME2": {
          "max": {
            "field": "bytes"
          }
        }
      }
    },
    "summary_bytes_min": {
      "min_bucket": {
        "buckets_path": "NAME1>NAME2.value",
        "gap_policy": "skip"
      }
    }
  }
}

GET mylogs-apache-v2*/_search?size=0
{
  "query": {
    "match_all": {}
  },
  "aggs": {
    "NAME1": {
      "date_histogram": {
        "field": "@timestamp",
        "interval": "day",
        "min_doc_count": 100000
      },
      "aggs": {
        "NAME2": {
          "avg": {
            "field": "bytes"
          }
        }
      }
    },
    "summary_bytes_avg": {
      "avg_bucket": {
        "buckets_path": "NAME1>NAME2",
        "gap_policy": "skip"
      }
    }
  }
}

GET mylogs-apache-v2*/_search?size=0
{
  "size": 0,
  "aggs": {
    "NAME1": {
      "date_histogram": {
        "field": "@timestamp",
        "calendar_interval": "hour"
      },
      "aggs": {
        "max_bytes": {
          "max": {
            "field": "bytes"
          }
        },
        "the_difference_with_prev": {
          "derivative": {
            "buckets_path": "max_bytes"
          }
        }
      }
    }
  }
}
```

**Bucket Aggregation**

Group documents with the same criteria into buckets. Criterion can be the same field value, the same time range etc.

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

```json
GET mylogs-apache-v2-2022.08.10/_search
{
  "query": {
    "bool": {
      "filter": [
        {
          "range": {
            "@timestamp": {
              "gte": "2022-08-10T15:00:00.000Z",
              "lte": "2022-08-10T15:10:00.000Z"
            }
          }
        }
      ]
    }
  }
}

GET mylogs-apache-v2-2022.08.10/_search
{
  "query": {
    "bool": {
      "filter": [
        {
          "range": {
            "@timestamp": {
              "gte": "2022-08-10T15:00:00.000Z",
              "lte": "2022-08-10T15:10:00.000Z"
            }
          }
        }
      ]
    }
  },
  "aggs": {
    "NAME": {
      "avg": {
        "field": "bytes"
      }
    }
  }
}

GET mylogs-apache-v2-2022.08.10/_search?size=0
{
  "query": {
    "bool": {
      "filter": [
        {
          "range": {
            "@timestamp": {
              "gte": "2022-08-10T15:00:00.000Z",
              "lte": "2022-08-10T15:10:00.000Z"
            }
          }
        }
      ]
    }
  },
  "aggs": {
    "NAME1": {
      "min": {
        "field": "bytes"
      }
    },
    "NAME2": {
      "max": {
        "field": "bytes"
      }
    },
    "NAME3": {
      "avg": {
        "field": "bytes"
      }
    }
  }
}

GET mylogs-apache-v2-2022.08.10/_search?size=0
{
  "query": {
    "bool": {
      "filter": [
        {
          "range": {
            "@timestamp": {
              "gte": "2022-08-10T15:00:00.000Z",
              "lte": "2022-08-10T16:10:00.000Z"
            }
          }
        }
      ]
    }
  },
  "aggs": {
    "NAME1": {
      "min": {
        "field": "bytes"
      }
    },
    "NAME2": {
      "max": {
        "field": "bytes"
      }
    },
    "NAME3": {
      "avg": {
        "field": "bytes"
      }
    },
    "NAME4": {
      "value_count": {
        "field": "bytes"
      }
    }
  }
}

POST _bulk
{ "index" : { "_index" : "transactions-books-v1"} }
{ "title" : "Elasticsearch in action", "payment" : "card", "type": "sale", "amount": 10.99 }
{ "index" : { "_index" : "transactions-books-v1"} }
{ "title" : "Fairy tales for all", "payment" : "cash", "type": "sale", "amount": 8.49 }
{ "index" : { "_index" : "transactions-books-v1"} }
{ "title" : "JavaScript", "payment" : "cash", "type": "sale", "amount": 11.00 }
{ "index" : { "_index" : "transactions-books-v1"} }
{ "title" : "Cooking for dummies", "payment" : "cash", "type": "refund", "amount": 5.99 }
{ "index" : { "_index" : "transactions-books-v1"} }
{ "title" : "Elasticsearch", "payment" : "cash", "type": "sale", "amount": 5.99 }
{ "index" : { "_index" : "transactions-books-v1"} }
{ "title" : "Query DSL", "payment" : "cash", "type": "sale", "amount": 8.99 }

POST transactions-books-v1/_search?size=0
{
    "query" : {
        "match_all" : {}
    },
    "aggs": {
        "profit": {
            "scripted_metric": {
                "init_script" : "state.transactions = []", 
                "map_script" : "state.transactions.add(doc['type.keyword'].value == \u0027sale\u0027 ? doc.amount.value : -1 * doc.amount.value)",
                "combine_script" : "double profit = 0; for (t in state.transactions) { profit += t } return profit",
                "reduce_script" : "double profit = 0; for (a in states) { profit += a } return profit"
            }
        }
    }
}

GET transactions-books-v1/_search?size=0
{
  "runtime_mappings": {
    "diff": {
      "type": "double",
      "script": {
        "source": "emit(doc['type.keyword'].value == \u0027sale\u0027 ? doc['amount'].value : -1 * doc['amount'].value)"
      }
    }
  },
  "aggs": {
    "NAME": {
      "sum": {
        "field": "diff"
      }
    }
  }
}


---------------------------------------------

POST /mylogs-apache-v2*/_search?size=0
{
  "query": {
    "match_all": {}
  },
  "aggs": {
    "NAME": {
      "terms": {
        "field": "verb"
      }
    }
  }
}

POST /mylogs-apache-v2*/_search?size=0
{
  "query": {
    "match_all": {}
  },
  "aggs": {
    "NAME": {
      "terms": {
        "field": "verb",
        "size": 10,
	      "order": { "_key": "asc" }
      }
    }
  }
}

GET mylogs-apache-v2-2022.08.10/_search?size=0
{
  "query": {
    "bool": {
      "filter": [
        {
          "range": {
            "@timestamp": {
              "gte": "2022-08-10T15:00:00.000Z",
              "lte": "2022-08-10T16:10:00.000Z"
            }
          }
        }
      ]
    }
  },
  "aggs": {
    "NAME": {
      "terms": {
        "field": "verb",
        "size": 10
      },
      "aggs": {
        "NAME1": {
          "min": {
            "field": "bytes"
          }
        },
        "NAME2": {
          "max": {
            "field": "bytes"
          }
        },
        "NAME3": {
          "avg": {
            "field": "bytes"
          }
        },
        "NAME4": {
          "value_count": {
            "field": "bytes"
          }
        }
      }
    }
  }
}

GET mylogs-apache-v2*/_search?size=0
{
  "query": {
    "match_all": {}
  },
  "aggs": {
    "NAME": {
      "histogram": {
        "field": "bytes",
        "interval": 50
      }
    }
  }
}

GET mylogs-apache-v2*/_search?size=0
{
  "query": {
    "match_all": {}
  },
  "aggs": {
    "NAME": {
      "histogram": {
        "field": "bytes",
        "interval": 200,
        "missing": 0,
        "offset": 2,
        "extended_bounds": {
          "min": 0,
          "max": 6000
        }
      }
    }
  }
}

GET mylogs-apache-v2*/_search?size=0
{
  "query": {
    "match_all": {}
  },
  "aggs": {
    "NAME": {
      "histogram": {
        "field": "bytes",
        "interval": 200,
        "missing": 0,
        "offset": 200,
        "hard_bounds": {
          "min": 4700,
          "max": 6000
        }
      }
    }
  }
}

GET mylogs-apache-v2*/_search?size=0
{
  "query": {
    "match_all": {}
  },
  "aggs": {
    "NAME": {
      "histogram": {
        "field": "bytes",
        "interval": 200,
        "missing": 0,
        "offset": 200,
        "hard_bounds": {
          "min": 4700,
          "max": 6000
        },
        "min_doc_count": 50,
        "keyed": true
      }
    }
  }
}

GET mylogs-apache-v2*/_search?size=0
{
  "query": {
    "match_all": {}
  },
  "aggs": {
    "NAME": {
      "date_histogram": {
        "field": "@timestamp",
        "interval": "10m"
      }
    }
  }
}

GET mylogs-apache-v2*/_search?size=0
{
  "query": {
    "match_all": {}
  },
  "aggs": {
    "NAME": {
      "geohash_grid": {
        "field": "geoip.location",
        "precision": 2,
        "bounds": {
          "top_left": "POINT (-121.7352672 49.9858749)",
          "bottom_right": "POINT (-64.5674731 33.8081914)"
        }
      }
    }
  }
}

GET mylogs-apache-v2*/_search?size=0
{
  "query": {
    "bool": {
      "filter": [
        {
          "term": {
            "geoip.country_name": "United States"
          }
        }
      ]
    }
  },
  "aggs": {
    "NAME": {
      "geohash_grid": {
        "field": "geoip.location",
        "precision": 4,
        "bounds": {
          "top_left": "POINT (-121.7352672 49.9858749)",
          "bottom_right": "POINT (-64.5674731 33.8081914)"
        }
      }
    }
  }
}


PUT /_bulk?refresh
{ "index" : { "_index" : "flight-routes-v1" } }
{ "origin": "NewYork", "destinations": ["Paris", "Amsterdam", "Boston", "London"]}
{ "index" : { "_index" : "flight-routes-v1" } }
{ "origin": "Paris", "destinations": ["London"]}
{ "index" : { "_index" : "flight-routes-v1" } }
{ "origin": "Amsterdam", "destinations": ["London", "Paris"]}
{ "index" : { "_index" : "flight-routes-v1" } }
{ "origin": "Boston", "destinations": ["NewYork"]}
{ "index" : { "_index" : "flight-routes-v1" } }
{ "origin": "London", "destinations": ["NewYork", "Barcelona"]}
{ "index" : { "_index" : "flight-routes-v1" } }
{ "origin": "Barcelona", "destinations": ["London","Amsterdam"]}

GET flight-routes-v1/_search?size=0
{
  "aggs": {
    "NAME": {
      "terms": {
        "field": "destinations.keyword",
        "size": 10
      }
    }
  }
}
          
GET /flight-routes-v1/_search?pretty
{
  "size": 0,
  "aggs" : {
    "interactions" : {
      "adjacency_matrix" : {
        "filters" : {
          "flights_to_NewYork" : { "term" : { "destinations.keyword" : "NewYork" }},
          "flights_to_Barcelona" : { "term" : { "destinations.keyword" : "Barcelona" }}
        }
      }
    }
  }
}

GET /flight-routes-v1/_search?pretty
{
  "size": 0,
  "aggs" : {
    "interactions" : {
      "adjacency_matrix" : {
        "filters" : {
          "flights_to_NewYork" : { "term" : { "destinations.keyword" : "NewYork" }},
          "flights_to_Barcelona" : { "term" : { "destinations.keyword" : "Barcelona" }}
        }
      },"aggs": {
        "NAME": {
          "top_hits": {
            "size": 10,
            "_source": {
              "includes": "origin"
            }
          }
        }
      }
    }
  }
}


PUT /_bulk?refresh
{ "index" : { "_index" : "access-rights-v1" } }
{ "user": "Alan", "service": ["apache"]}
{ "index" : { "_index" : "access-rights-v1" } }
{ "user": "Be", "service": ["ssh", "apache"]}
{ "index" : { "_index" : "access-rights-v1" } }
{ "user": "Celi", "service": ["sendmail"]}
{ "index" : { "_index" : "access-rights-v1" } }
{ "user": "Dan", "service": ["ssh"]}
{ "index" : { "_index" : "access-rights-v1" } }
{ "user": "Eli", "service": ["sendmail"]}
{ "index" : { "_index" : "access-rights-v1" } }
{ "user": "Fin", "service": ["apache","sendmail","ssh"]}

GET access-rights-v1/_search?size=0
{
  "aggs": {
    "NAME": {
      "terms": {
        "field": "service.keyword",
        "size": 10
      }
    }
  }
}

GET /access-rights-v1/_search?pretty
{
  "size": 0,
  "aggs" : {
    "interactions" : {
      "adjacency_matrix" : {
        "filters" : {
          "apache" : { "term" : { "service" : "apache" }},
          "ssh" : { "term" : { "service" : "ssh" }},
          "sendmail" : { "term" : { "service" : "sendmail" }}
        }
      }
    }
  }
}

GET /access-rights-v1/_search?pretty
{
  "size": 0,
  "aggs" : {
    "interactions" : {
      "adjacency_matrix" : {
        "filters" : {
          "apache" : { "term" : { "service" : "apache" }},
          "ssh" : { "term" : { "service" : "ssh" }},
          "sendmail" : { "term" : { "service" : "sendmail" }}
        }
      },"aggs": {
        "NAME": {
          "top_hits": {
            "size": 10,
            "_source": {
              "includes": "user"
            }
          }
        }
      }
    }
  }
}


-----------------------------------------------------------------------------
GET mylogs-apache-v2*/_search?size=0
{
  "size": 0,
  "aggs": {
    "NAME1": {
      "date_histogram": {
        "field": "@timestamp",
        "calendar_interval": "day"
      },
      "aggs": {
        "NAME2": {
          "max": {
            "field": "bytes"
          }
        }
      }
    },
    "summary_bytes_min": {
      "min_bucket": {
        "buckets_path": "NAME1>NAME2.value",
        "gap_policy": "skip"
      }
    }
  }
}

GET mylogs-apache-v2*/_search?size=0
{
  "size": 0,
  "aggs": {
    "NAME1": {
      "date_histogram": {
        "field": "@timestamp",
        "calendar_interval": "day",
        "min_doc_count": 100000
      },
      "aggs": {
        "NAME2": {
          "max": {
            "field": "bytes"
          }
        }
      }
    },
    "summary_bytes_min": {
      "min_bucket": {
        "buckets_path": "NAME1>NAME2.value",
        "gap_policy": "skip"
      }
    }
  }
}

GET mylogs-apache-v2*/_search?size=0
{
  "query": {
    "match_all": {}
  },
  "aggs": {
    "NAME1": {
      "date_histogram": {
        "field": "@timestamp",
        "interval": "day",
        "min_doc_count": 100000
      },
      "aggs": {
        "NAME2": {
          "avg": {
            "field": "bytes"
          }
        }
      }
    },
    "summary_bytes_avg": {
      "avg_bucket": {
        "buckets_path": "NAME1>NAME2",
        "gap_policy": "skip"
      }
    }
  }
}

GET mylogs-apache-v2*/_search?size=0
{
  "size": 0,
  "aggs": {
    "NAME1": {
      "date_histogram": {
        "field": "@timestamp",
        "calendar_interval": "hour"
      },
      "aggs": {
        "max_bytes": {
          "max": {
            "field": "bytes"
          }
        },
        "the_difference_with_prev": {
          "derivative": {
            "buckets_path": "max_bytes"
          }
        }
      }
    }
  }
}
```

**Global Aggregation**

Compute metrics on results produced from other aggregations

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

```java
GET mylogs-apache-v2-2022.08.10/_search
{
  "query": {
    "bool": {
      "filter": [
        {
          "range": {
            "@timestamp": {
              "gte": "2022-08-10T15:00:00.000Z",
              "lte": "2022-08-10T15:10:00.000Z"
            }
          }
        }
      ]
    }
  }
}

GET mylogs-apache-v2-2022.08.10/_search
{
  "query": {
    "bool": {
      "filter": [
        {
          "range": {
            "@timestamp": {
              "gte": "2022-08-10T15:00:00.000Z",
              "lte": "2022-08-10T15:10:00.000Z"
            }
          }
        }
      ]
    }
  },
  "aggs": {
    "NAME": {
      "avg": {
        "field": "bytes"
      }
    }
  }
}

GET mylogs-apache-v2-2022.08.10/_search?size=0
{
  "query": {
    "bool": {
      "filter": [
        {
          "range": {
            "@timestamp": {
              "gte": "2022-08-10T15:00:00.000Z",
              "lte": "2022-08-10T15:10:00.000Z"
            }
          }
        }
      ]
    }
  },
  "aggs": {
    "NAME1": {
      "min": {
        "field": "bytes"
      }
    },
    "NAME2": {
      "max": {
        "field": "bytes"
      }
    },
    "NAME3": {
      "avg": {
        "field": "bytes"
      }
    }
  }
}

GET mylogs-apache-v2-2022.08.10/_search?size=0
{
  "query": {
    "bool": {
      "filter": [
        {
          "range": {
            "@timestamp": {
              "gte": "2022-08-10T15:00:00.000Z",
              "lte": "2022-08-10T16:10:00.000Z"
            }
          }
        }
      ]
    }
  },
  "aggs": {
    "NAME1": {
      "min": {
        "field": "bytes"
      }
    },
    "NAME2": {
      "max": {
        "field": "bytes"
      }
    },
    "NAME3": {
      "avg": {
        "field": "bytes"
      }
    },
    "NAME4": {
      "value_count": {
        "field": "bytes"
      }
    }
  }
}

POST _bulk
{ "index" : { "_index" : "transactions-books-v1"} }
{ "title" : "Elasticsearch in action", "payment" : "card", "type": "sale", "amount": 10.99 }
{ "index" : { "_index" : "transactions-books-v1"} }
{ "title" : "Fairy tales for all", "payment" : "cash", "type": "sale", "amount": 8.49 }
{ "index" : { "_index" : "transactions-books-v1"} }
{ "title" : "JavaScript", "payment" : "cash", "type": "sale", "amount": 11.00 }
{ "index" : { "_index" : "transactions-books-v1"} }
{ "title" : "Cooking for dummies", "payment" : "cash", "type": "refund", "amount": 5.99 }
{ "index" : { "_index" : "transactions-books-v1"} }
{ "title" : "Elasticsearch", "payment" : "cash", "type": "sale", "amount": 5.99 }
{ "index" : { "_index" : "transactions-books-v1"} }
{ "title" : "Query DSL", "payment" : "cash", "type": "sale", "amount": 8.99 }

POST transactions-books-v1/_search?size=0
{
    "query" : {
        "match_all" : {}
    },
    "aggs": {
        "profit": {
            "scripted_metric": {
                "init_script" : "state.transactions = []", 
                "map_script" : "state.transactions.add(doc['type.keyword'].value == \u0027sale\u0027 ? doc.amount.value : -1 * doc.amount.value)",
                "combine_script" : "double profit = 0; for (t in state.transactions) { profit += t } return profit",
                "reduce_script" : "double profit = 0; for (a in states) { profit += a } return profit"
            }
        }
    }
}

GET transactions-books-v1/_search?size=0
{
  "runtime_mappings": {
    "diff": {
      "type": "double",
      "script": {
        "source": "emit(doc['type.keyword'].value == \u0027sale\u0027 ? doc['amount'].value : -1 * doc['amount'].value)"
      }
    }
  },
  "aggs": {
    "NAME": {
      "sum": {
        "field": "diff"
      }
    }
  }
}


---------------------------------------------

POST /mylogs-apache-v2*/_search?size=0
{
  "query": {
    "match_all": {}
  },
  "aggs": {
    "NAME": {
      "terms": {
        "field": "verb"
      }
    }
  }
}

POST /mylogs-apache-v2*/_search?size=0
{
  "query": {
    "match_all": {}
  },
  "aggs": {
    "NAME": {
      "terms": {
        "field": "verb",
        "size": 10,
	      "order": { "_key": "asc" }
      }
    }
  }
}

GET mylogs-apache-v2-2022.08.10/_search?size=0
{
  "query": {
    "bool": {
      "filter": [
        {
          "range": {
            "@timestamp": {
              "gte": "2022-08-10T15:00:00.000Z",
              "lte": "2022-08-10T16:10:00.000Z"
            }
          }
        }
      ]
    }
  },
  "aggs": {
    "NAME": {
      "terms": {
        "field": "verb",
        "size": 10
      },
      "aggs": {
        "NAME1": {
          "min": {
            "field": "bytes"
          }
        },
        "NAME2": {
          "max": {
            "field": "bytes"
          }
        },
        "NAME3": {
          "avg": {
            "field": "bytes"
          }
        },
        "NAME4": {
          "value_count": {
            "field": "bytes"
          }
        }
      }
    }
  }
}

GET mylogs-apache-v2*/_search?size=0
{
  "query": {
    "match_all": {}
  },
  "aggs": {
    "NAME": {
      "histogram": {
        "field": "bytes",
        "interval": 50
      }
    }
  }
}

GET mylogs-apache-v2*/_search?size=0
{
  "query": {
    "match_all": {}
  },
  "aggs": {
    "NAME": {
      "histogram": {
        "field": "bytes",
        "interval": 200,
        "missing": 0,
        "offset": 2,
        "extended_bounds": {
          "min": 0,
          "max": 6000
        }
      }
    }
  }
}

GET mylogs-apache-v2*/_search?size=0
{
  "query": {
    "match_all": {}
  },
  "aggs": {
    "NAME": {
      "histogram": {
        "field": "bytes",
        "interval": 200,
        "missing": 0,
        "offset": 200,
        "hard_bounds": {
          "min": 4700,
          "max": 6000
        }
      }
    }
  }
}

GET mylogs-apache-v2*/_search?size=0
{
  "query": {
    "match_all": {}
  },
  "aggs": {
    "NAME": {
      "histogram": {
        "field": "bytes",
        "interval": 200,
        "missing": 0,
        "offset": 200,
        "hard_bounds": {
          "min": 4700,
          "max": 6000
        },
        "min_doc_count": 50,
        "keyed": true
      }
    }
  }
}

GET mylogs-apache-v2*/_search?size=0
{
  "query": {
    "match_all": {}
  },
  "aggs": {
    "NAME": {
      "date_histogram": {
        "field": "@timestamp",
        "interval": "10m"
      }
    }
  }
}

GET mylogs-apache-v2*/_search?size=0
{
  "query": {
    "match_all": {}
  },
  "aggs": {
    "NAME": {
      "geohash_grid": {
        "field": "geoip.location",
        "precision": 2,
        "bounds": {
          "top_left": "POINT (-121.7352672 49.9858749)",
          "bottom_right": "POINT (-64.5674731 33.8081914)"
        }
      }
    }
  }
}

GET mylogs-apache-v2*/_search?size=0
{
  "query": {
    "bool": {
      "filter": [
        {
          "term": {
            "geoip.country_name": "United States"
          }
        }
      ]
    }
  },
  "aggs": {
    "NAME": {
      "geohash_grid": {
        "field": "geoip.location",
        "precision": 4,
        "bounds": {
          "top_left": "POINT (-121.7352672 49.9858749)",
          "bottom_right": "POINT (-64.5674731 33.8081914)"
        }
      }
    }
  }
}


PUT /_bulk?refresh
{ "index" : { "_index" : "flight-routes-v1" } }
{ "origin": "NewYork", "destinations": ["Paris", "Amsterdam", "Boston", "London"]}
{ "index" : { "_index" : "flight-routes-v1" } }
{ "origin": "Paris", "destinations": ["London"]}
{ "index" : { "_index" : "flight-routes-v1" } }
{ "origin": "Amsterdam", "destinations": ["London", "Paris"]}
{ "index" : { "_index" : "flight-routes-v1" } }
{ "origin": "Boston", "destinations": ["NewYork"]}
{ "index" : { "_index" : "flight-routes-v1" } }
{ "origin": "London", "destinations": ["NewYork", "Barcelona"]}
{ "index" : { "_index" : "flight-routes-v1" } }
{ "origin": "Barcelona", "destinations": ["London","Amsterdam"]}

GET flight-routes-v1/_search?size=0
{
  "aggs": {
    "NAME": {
      "terms": {
        "field": "destinations.keyword",
        "size": 10
      }
    }
  }
}
          
GET /flight-routes-v1/_search?pretty
{
  "size": 0,
  "aggs" : {
    "interactions" : {
      "adjacency_matrix" : {
        "filters" : {
          "flights_to_NewYork" : { "term" : { "destinations.keyword" : "NewYork" }},
          "flights_to_Barcelona" : { "term" : { "destinations.keyword" : "Barcelona" }}
        }
      }
    }
  }
}

GET /flight-routes-v1/_search?pretty
{
  "size": 0,
  "aggs" : {
    "interactions" : {
      "adjacency_matrix" : {
        "filters" : {
          "flights_to_NewYork" : { "term" : { "destinations.keyword" : "NewYork" }},
          "flights_to_Barcelona" : { "term" : { "destinations.keyword" : "Barcelona" }}
        }
      },"aggs": {
        "NAME": {
          "top_hits": {
            "size": 10,
            "_source": {
              "includes": "origin"
            }
          }
        }
      }
    }
  }
}


PUT /_bulk?refresh
{ "index" : { "_index" : "access-rights-v1" } }
{ "user": "Alan", "service": ["apache"]}
{ "index" : { "_index" : "access-rights-v1" } }
{ "user": "Be", "service": ["ssh", "apache"]}
{ "index" : { "_index" : "access-rights-v1" } }
{ "user": "Celi", "service": ["sendmail"]}
{ "index" : { "_index" : "access-rights-v1" } }
{ "user": "Dan", "service": ["ssh"]}
{ "index" : { "_index" : "access-rights-v1" } }
{ "user": "Eli", "service": ["sendmail"]}
{ "index" : { "_index" : "access-rights-v1" } }
{ "user": "Fin", "service": ["apache","sendmail","ssh"]}

GET access-rights-v1/_search?size=0
{
  "aggs": {
    "NAME": {
      "terms": {
        "field": "service.keyword",
        "size": 10
      }
    }
  }
}

GET /access-rights-v1/_search?pretty
{
  "size": 0,
  "aggs" : {
    "interactions" : {
      "adjacency_matrix" : {
        "filters" : {
          "apache" : { "term" : { "service" : "apache" }},
          "ssh" : { "term" : { "service" : "ssh" }},
          "sendmail" : { "term" : { "service" : "sendmail" }}
        }
      }
    }
  }
}

GET /access-rights-v1/_search?pretty
{
  "size": 0,
  "aggs" : {
    "interactions" : {
      "adjacency_matrix" : {
        "filters" : {
          "apache" : { "term" : { "service" : "apache" }},
          "ssh" : { "term" : { "service" : "ssh" }},
          "sendmail" : { "term" : { "service" : "sendmail" }}
        }
      },"aggs": {
        "NAME": {
          "top_hits": {
            "size": 10,
            "_source": {
              "includes": "user"
            }
          }
        }
      }
    }
  }
}


-----------------------------------------------------------------------------
GET mylogs-apache-v2*/_search?size=0
{
  "size": 0,
  "aggs": {
    "NAME1": {
      "date_histogram": {
        "field": "@timestamp",
        "calendar_interval": "day"
      },
      "aggs": {
        "NAME2": {
          "max": {
            "field": "bytes"
          }
        }
      }
    },
    "summary_bytes_min": {
      "min_bucket": {
        "buckets_path": "NAME1>NAME2.value",
        "gap_policy": "skip"
      }
    }
  }
}

GET mylogs-apache-v2*/_search?size=0
{
  "size": 0,
  "aggs": {
    "NAME1": {
      "date_histogram": {
        "field": "@timestamp",
        "calendar_interval": "day",
        "min_doc_count": 100000
      },
      "aggs": {
        "NAME2": {
          "max": {
            "field": "bytes"
          }
        }
      }
    },
    "summary_bytes_min": {
      "min_bucket": {
        "buckets_path": "NAME1>NAME2.value",
        "gap_policy": "skip"
      }
    }
  }
}

GET mylogs-apache-v2*/_search?size=0
{
  "query": {
    "match_all": {}
  },
  "aggs": {
    "NAME1": {
      "date_histogram": {
        "field": "@timestamp",
        "interval": "day",
        "min_doc_count": 100000
      },
      "aggs": {
        "NAME2": {
          "avg": {
            "field": "bytes"
          }
        }
      }
    },
    "summary_bytes_avg": {
      "avg_bucket": {
        "buckets_path": "NAME1>NAME2",
        "gap_policy": "skip"
      }
    }
  }
}

GET mylogs-apache-v2*/_search?size=0
{
  "size": 0,
  "aggs": {
    "NAME1": {
      "date_histogram": {
        "field": "@timestamp",
        "calendar_interval": "hour"
      },
      "aggs": {
        "max_bytes": {
          "max": {
            "field": "bytes"
          }
        },
        "the_difference_with_prev": {
          "derivative": {
            "buckets_path": "max_bytes"
          }
        }
      }
    }
  }
}
```

## Search API Special Features

### Highlighting

➔ Unified highlighter
	Uses the Lucene Unified Highlighter. It breaks the text into sentences and uses the BM25 algorithm to score individual sentences. **==Best suited for highlighting multiple fields in many documents matched by complex queries==**.
	==**Cons: it is most universal one, so can be slower than other highlighters**==

➔ Plain highlighter
	The plain highlighter uses the standard Lucene highlighter. It attempts to reflect the query matching logic in terms of understanding word importance and any word positioning criteria in phrase queries. **==Best suited for highlighting simple query that match single field==**.
	==**Cons: higher memory footprint**==

➔ Fast vector highlighter
	The ``fvh`` highlighter uses the Lucene Fast Vector highlighter and requires special mapping. Fields used
	for highlighting must have the “``term_vector``” attribute set to “``with_positions_offsets``”. **==Best suited for**==
	==**highlighting multiple fields in many documents matched by complex queries.==**
	==**Cons: larger shards (more information and statistics about terms in fields for each indexed document)**==

```java
POST test-documents-v1/_doc
{
"title" : "Market condition in USA",
"content" : "Current condition of the Market in USA is lorem ipsum dolor sit amet, consectetur adipiscing elit. Suspendisse fermentum nec lacus nec hendrerit. Pellentesque tristique mattis sagittis. Vestibulum nec vestibulum odio. Integer eu diam urna. Mauris condimentum sapien magna, ac vehicula orci vulputate eget. Sed aliquam sem ut ultricies volutpat. Nullam metus lectus, consequat eget suscipit quis, suscipit sed felis. Sed id turpis dictum erat pretium lobortis. Duis id nisi id nisl imperdiet convallis. Donec dignissim, lorem vel facilisis commodo, risus ligula euismod tellus, vitae porttitor justo odio vel turpis. Donec molestie vitae dolor sit amet imperdiet. Import of goods from China impact the domestic id sapien convallis, aliquam risus ac, aliquet dolor. Suspendisse dolor arcu, viverra eget erat eget, elementum dignissim dolor. Proin cursus bibendum diam sit amet vulputate. Mauris malesuada maximus lorem, sit amet cursus quam faucibus non. Fusce malesuada magna ac erat blandit, quis cursus nibh eleifend. Suspendisse malesuada quis nisl eget aliquam. Morbi felis elit, dignissim non pharetra in, volutpat a enim. Cras tempus leo in metus placerat, eget egestas ante sagittis. Proin pretium diam sed nisi tincidunt, sed tincidunt ligula dictum. Etiam auctor fermentum est eu luctus. Phasellus tincidunt erat non enim imperdiet mattis."
}

POST /test-documents-v1/_search
{
    "query": {
        "query_string": {
            "query": "market in china",
            "fields": ["content"]
        }
    }
}

POST /test-documents-v1/_search
{
    "query": {
        "query_string": {
            "query": "market in china",
            "fields": ["content"]
        }
    },
    "highlight": {
        "order": "score",
        "pre_tags" : ["<b>"],
        "post_tags" : ["</b>"],
        "fields": {
            "content": {
                "type" : "unified",
                "fragment_size": 20,
                "number_of_fragments": 10
            }
        }
    }
}

POST /test-documents-v1/_search
{
  "_source": {
    "excludes": "content"
  }, 
  "query": {
      "query_string": {
          "query": "market in china",
          "fields": ["content"]
      }
  },
  "highlight": {
      "order": "score",
      "pre_tags" : ["<b>"],
      "post_tags" : ["</b>"],
      "fields": {
          "content": {
              "type" : "unified",
              "fragment_size": 20,
              "number_of_fragments": 10
          }
      }
  }
}

POST /test-documents-v1/_search
{
    "query": {
        "query_string": {
            "query": "market in china",
            "fields": ["content"]
        }
    },
    "highlight": {
        "order": "score",
        "pre_tags" : ["<b>"],
        "post_tags" : ["</b>"],
        "fields": {
            "content": {
                "type" : "plain",
                "fragment_size": 20,
                "number_of_fragments": 10
            }
        }
    }
}

PUT test-documents-v2
{
  "mappings": {
    "properties": {
      "content" : {
        "type": "text",
        "term_vector": "with_positions_offsets"
      }
    }
  }
}

POST /_reindex?wait_for_completion=true
{
  "conflicts" : "proceed",
  "source": {
    "index": "test-documents-v1"
  },
  "dest": {
    "index": "test-documents-v2"
  }
}

GET /test-documents-v2/_termvectors/<id goes here>

POST /test-documents-v2/_search
{
    "query": {
        "query_string": {
            "query": "market in china",
            "fields": ["content"]
        }
    },
    "highlight": {
        "order": "score",
        "pre_tags" : ["<b>"],
        "post_tags" : ["</b>"],
        "fields": {
            "content": {
                "type" : "fvh",
                "fragment_size": 20,
                "number_of_fragments": 10
            }
        }
    }
}


POST /sample-book-v2/_search
{
  "query": {
    "nested": {
      "path": "author",
      "query": {
        "query_string": {
          "default_field": "author.biography",
          "query": "technical"
        }
      },
      "inner_hits": { 
        "_source": {
          "excludes": ["author.firstname", "author.biography", "author.lastname"]
        },
        "highlight": {
           "fields": { 
             "author.biography": {}
           }
        }
      }
    }
  }
}
```

➔ **Keep hits[] array small** 
	Return reasonable number of documents in the hits[] array. Elasticsearch by design is optimized for pagination, and using high “size” value should be avoided, because it negatively impacts on performance. Such fact is especially important when using highlighting, because coordinating node applies highlighting for all documents in the “hits[]” array.

### Suggestion And Spell Correction

Suggesters provide **did you mean (spelling correction)** feature and **auto-complete (type-ahead)** feature. Automatic correction of the user’s spelling mistakes and typos improve the overall search experience.

➔ **Term suggester**
	Similar terms based on the edit distance (Levenshtein, Jaro-Winkler, ngram algorithms)
	
➔ **Phrase suggester**
	Same as term, but taking into account a whole phrase

➔ **Completion suggester**
	**Optimized for speed**, because auto-complete feature should be as fast as user types. Note that cost is memory - **suggestions are build and stored in-memory**

➔ **Context suggester**
	Same as completion, but with suggestions filtering and/or boosting features (**category** and **geo** types)

```java
POST /mylogs-apache-v2*/_search?pretty
{
  "suggest": {
    "text": "Mazilla developed the Forefax",
    "simple_phrase": {
      "phrase": {
        "field": "agent",
        "size": 1,
        "gram_size": 3,
        "direct_generator": [ {
          "field": "agent",
          "suggest_mode": "always"
        } ],
        "highlight": {
          "pre_tag": "<em>",
          "post_tag": "</em>"
        }
      }
    }
  }
}

POST /mylogs-apache-v2*/_search?pretty
{
  "suggest": {
    "text": "Mazilla developed the Forefax",
    "simple_phrase": {
      "phrase": {
        "field": "geoip.country_name",
        "size": 1,
        "gram_size": 3,
        "direct_generator": [ {
          "field": "geoip.country_name",
          "suggest_mode": "always"
        } ],
        "highlight": {
          "pre_tag": "<em>",
          "post_tag": "</em>"
        }
      }
    }
  }
}

---------------------------------------------------

PUT countries-list-v2
{
  "settings": {
    "max_ngram_diff" : 5,
    "analysis": {
      "analyzer": {
        "country_analyzer": {
          "tokenizer": "country_tokenizer",
          "filter" : ["lowercase"]
        }
      },
      "tokenizer": {
        "country_tokenizer": {
          "type": "edge_ngram",
          "min_gram": 1,
          "max_gram": 6
        }
      }
    }
  },
  "mappings": {
    "properties": {
      "country" : {
        "type" : "text",
        "analyzer": "country_analyzer"
      }  
    }
  }
}

POST countries-list-v2/_analyze
{
  "text": "Panama",
  "analyzer": "country_analyzer"
}

PUT countries-list-v3
{
  "mappings": {
    "properties": {
      "country" : {
        "type" : "completion"
      }  
    }
  }
}

POST /_reindex?wait_for_completion=true
{
  "conflicts" : "proceed",
  "source": {
    "index": "countries-list-v1"
  },
  "dest": {
    "index": "countries-list-v2"
  }
}

POST /_reindex?wait_for_completion=true
{
  "conflicts" : "proceed",
  "source": {
    "index": "countries-list-v1"
  },
  "dest": {
    "index": "countries-list-v3"
  }
}

POST /countries-list-v1/_search
{
  "query": {
    "prefix": {
      "country": {
        "value": "pa"
      }
    }
  }
}

POST countries-list-v2/_search
{
  "query": {
    "term": {
      "country": {
        "value": "pa"
      }
    }
  }
}

POST countries-list-v2/_search
{
  "query": {
    "fuzzy": {
      "country": {
        "value": "penam"
      }
    }
  }
}

POST /countries-list-v3/_search?pretty
{
  "suggest": {
    "country-suggest": {
      "prefix": "pa",
      "completion": {
        "field": "country",
        "size": 10
      }
    }
  }
}
```

![[Pasted image 20240620234409.png]]

## Docker Install

```shell
docker run -d --name elastic --net elb-network -p 9200:9200 -p 9300:9300 -e "xpack.security.enabled=false" -e "xpack.security.transport.ssl.enabled=false" -e "xpack.security.enrollment.enabled=true" -e "discovery.type=single-node" -e "ELASTIC_USERNAME=admin" -e "ELASTIC_PASSWORD=admin" -e "ES_JAVA_OPTS=-Xms512m -Xmx1024m" elasticsearch:8.12.1

docker run -d --name kibana --net elb-network -p 5601:5601 -e "ELASTICSEARCH_HOSTS=http://elastic:9200" docker.elastic.co/kibana/kibana:8.12.1
```


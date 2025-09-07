# Knowledge Graph Discovery System Design Document

## 1. System Architecture

### 1.1 Overview

The Knowledge Graph Discovery System follows a modular, agent-based architecture designed to efficiently transform unstructured web content into a structured knowledge graph. The system consists of several specialized agents, each responsible for a specific part of the knowledge graph discovery process.

![System Architecture](https://example.com/system-architecture.png)

### 1.2 Core Components

The system is organized into the following core components:

#### 1.2.1 Data Ingestion Layer

- **RobotsAnalyzer**: Parses and interprets robots.txt files to determine crawling permissions.
- **URLHistoryTracker**: Maintains history of processed URLs to avoid duplicate processing.
- **PDFExtractor**: Identifies and extracts content from PDF documents.
- **EnhancedDataIngestionAgent**: Coordinates the data collection process, respecting robots.txt rules and implementing section-based crawling.

#### 1.2.2 Knowledge Extraction Layer

- **InformationExtractionAgent**: Applies NLP techniques to extract entities, relationships, and attributes from text.
- **SchemaDiscoveryAgent**: Analyzes extracted information to discover a coherent schema.

#### 1.2.3 Graph Construction Layer

- **GraphConstructionAgent**: Builds a knowledge graph from extracted triples based on the discovered schema.
- **NetworkXHandler**: Implements graph operations using the NetworkX library.
- **Neo4jHandler**: Provides integration with the Neo4j graph database.

#### 1.2.4 Graph Enhancement Layer

- **GraphEnrichmentAgent**: Enhances the knowledge graph with additional context and inferences.

### 1.3 System Flow

1. The system begins with the analysis of robots.txt to determine crawling permissions.
2. The EnhancedDataIngestionAgent collects web content from allowed sections, tracking history to avoid duplicates.
3. The InformationExtractionAgent processes the collected text to extract structured information.
4. The SchemaDiscoveryAgent analyzes the extracted information to discover a schema.
5. The GraphConstructionAgent builds a knowledge graph based on the extracted information and schema.
6. The graph is visualized and/or imported into Neo4j for advanced querying.
7. The GraphEnrichmentAgent enhances the graph with additional context and inferences.

## 2. Component Design

### 2.1 Data Ingestion Layer

#### 2.1.1 RobotsAnalyzer

**Purpose**: Parse and interpret robots.txt files to determine crawling permissions.

**Key Methods**:
- `analyze(target_url, robots_txt_path)`: Analyzes robots.txt and returns allowed/disallowed paths.
- `is_url_allowed(url)`: Checks if a specific URL is allowed for crawling.

**Inputs**:
- Target URL
- Path to robots.txt file

**Outputs**:
- Dictionary with allowed paths, disallowed paths, sitemaps, and PDF-specific rules

#### 2.1.2 URLHistoryTracker

**Purpose**: Maintain history of processed URLs to avoid duplicate processing.

**Key Methods**:
- `load_history()`: Load URL history from file.
- `save_history()`: Save URL history to file.
- `is_url_processed(url)`: Check if URL has been processed before.
- `add_url(url, section, metadata)`: Add URL to history.
- `get_section_counts()`: Get count of URLs by section.
- `clear_history()`: Clear URL history.

**Inputs**:
- URL to check/add
- Section information
- Optional metadata

**Outputs**:
- Boolean indicating if URL is in history
- Dictionary of processed URLs and metadata

#### 2.1.3 PDFExtractor

**Purpose**: Identify and extract content from PDF documents.

**Key Methods**:
- `find_pdf_links(html_content, base_url)`: Find links to PDF documents in HTML content.
- `download_pdf(url)`: Download a PDF from a URL.
- `extract_links_from_financial_page(url)`: Extract PDF links from a financial reporting page.

**Inputs**:
- HTML content for link extraction
- Base URL for resolving relative links
- URL of financial reporting page

**Outputs**:
- Extracted text from PDF documents
- List of PDF links found
- Path to downloaded PDF files

#### 2.1.4 EnhancedDataIngestionAgent

**Purpose**: Coordinate the data collection process, respecting robots.txt rules and implementing section-based crawling.

**Key Methods**:
- `load_robots_txt(url, local_path)`: Load robots.txt from URL or local file.
- `get_url_section(url)`: Determine which section a URL belongs to.
- `should_process_url(url)`: Determine if a URL should be processed based on rules and history.
- `is_pdf_url(url)`: Check if URL points to a PDF file.
- `process_url(url, depth)`: Process a single URL and return extracted content.
- `crawl_sections(base_url)`: Crawl specific sections of the website with limits.
- `get_collected_data()`: Get collected text and metadata.

**Inputs**:
- Settings dictionary with configuration parameters
- History file path for URL tracking

**Outputs**:
- Dictionary with collected texts and metadata
- Crawling statistics including pages crawled, PDFs extracted, and pages skipped

### 2.2 Knowledge Extraction Layer

#### 2.2.1 InformationExtractionAgent

**Purpose**: Apply NLP techniques to extract entities, relationships, and attributes from text.

**Key Methods**:
- `extract_triples(texts)`: Extract subject-predicate-object triples from text.
- `extract_entities(texts)`: Extract named entities from text.

**Inputs**:
- List of text documents

**Outputs**:
- List of triples (subject, predicate, object)
- Dictionary of entities by type

#### 2.2.2 SchemaDiscoveryAgent

**Purpose**: Analyze extracted information to discover a coherent schema.

**Key Methods**:
- `discover_schema(triples, entities)`: Discover schema from extracted triples and entities.

**Inputs**:
- List of triples
- Dictionary of entities by type

**Outputs**:
- Schema dictionary with entity types and relationship types

### 2.3 Graph Construction Layer

#### 2.3.1 GraphConstructionAgent

**Purpose**: Build a knowledge graph from extracted triples based on the discovered schema.

**Key Methods**:
- `construct_graph(triples, schema)`: Construct a graph from triples and schema.
- `get_graph_statistics(graph)`: Get statistics about the graph.
- `save_graph(graph, filename)`: Save the graph to a file.

**Inputs**:
- List of triples
- Schema dictionary
- Graph handler instance

**Outputs**:
- NetworkX graph object
- Graph statistics

#### 2.3.2 NetworkXHandler

**Purpose**: Implement graph operations using the NetworkX library.

**Key Methods**:
- `create_graph()`: Create a new empty graph.
- `add_node(graph, node_id, attributes)`: Add a node to the graph.
- `add_edge(graph, source, target, attributes)`: Add an edge to the graph.
- `save_graph(graph, filename)`: Save the graph to a file.
- `load_graph(filename)`: Load a graph from a file.
- `visualize_graph(graph, output_path)`: Visualize the graph and save to file.

**Inputs**:
- NetworkX graph object
- Node and edge information

**Outputs**:
- Updated NetworkX graph object
- Visualization image file

#### 2.3.3 Neo4jHandler

**Purpose**: Provide integration with the Neo4j graph database.

**Key Methods**:
- `test_connection()`: Test connection to Neo4j.
- `import_networkx_graph(graph)`: Import NetworkX graph into Neo4j.
- `get_database_statistics()`: Get statistics about the Neo4j database.
- `generate_example_queries()`: Generate example Cypher queries.

**Inputs**:
- Neo4j connection parameters
- NetworkX graph object

**Outputs**:
- Database statistics
- Example queries

### 2.4 Graph Enhancement Layer

#### 2.4.1 GraphEnrichmentAgent

**Purpose**: Enhance the knowledge graph with additional context and inferences.

**Key Methods**:
- `enrich_graph(graph)`: Enrich the graph with additional information.

**Inputs**:
- NetworkX graph object

**Outputs**:
- Enhanced NetworkX graph object

## 3. Data Models

### 3.1 URL History Entry

```json
{
  "url": "https://example.com/page",
  "timestamp": 1626782400,
  "hash": "md5_hash_of_url",
  "section": "about",
  "metadata": {
    "title": "Page Title",
    "content_type": "text/html",
    "status_code": 200,
    "content_length": 12345
  }
}
```

### 3.2 Triple

```python
(subject, predicate, object)
```

Example: `("Verizon", "is headquartered in", "New York")`

### 3.3 Schema

```json
{
  "entity_types": {
    "Company": ["name", "industry", "founded_year"],
    "Person": ["name", "position", "company"],
    "Product": ["name", "category", "price"]
  },
  "relationships": {
    "works_for": [["Person", "Company"]],
    "owns": [["Company", "Product"]],
    "founded": [["Person", "Company"]]
  }
}
```

### 3.4 Knowledge Graph

The knowledge graph is represented using NetworkX's graph data structure:

- Nodes represent entities with attributes
- Edges represent relationships with attributes

## 4. Interfaces

### 4.1 Web Scraping Interface

- Uses requests for HTTP requests
- Uses trafilatura for HTML content extraction
- Uses selenium for JavaScript-heavy pages

### 4.2 NLP Interface

- Uses spaCy for entity recognition and syntactic parsing
- Uses custom rule-based extractors for triple extraction

### 4.3 Graph Database Interface

- Uses Neo4j Python driver for database operations
- Uses Cypher for graph queries

## 5. Error Handling

### 5.1 Network Errors

- Retry mechanism for transient network errors
- Graceful degradation for persistent network issues

### 5.2 Parsing Errors

- Fallback strategies for content extraction
- Logging of parsing failures for review

### 5.3 Database Errors

- Transaction rollback for database operation failures
- Connection pooling for efficient database usage

## 6. Performance Considerations

### 6.1 Crawling Efficiency

- Respect robots.txt and implement polite delays
- Track URL history to avoid duplicate processing
- Limit crawling depth and pages per section

### 6.2 Processing Efficiency

- Batch processing of documents for NLP operations
- Parallel processing where appropriate

### 6.3 Graph Efficiency

- Efficient graph algorithms for large graphs
- Index usage in Neo4j for query performance

## 7. Security Considerations

### 7.1 Web Scraping Ethics

- Respect robots.txt rules
- Use appropriate user agent identification
- Implement polite delays between requests

### 7.2 Data Storage

- Secure storage of extracted data
- Proper handling of sensitive information

### 7.3 Database Access

- Secure Neo4j credentials
- Limited database access permissions

## 8. Testing Strategy

### 8.1 Unit Testing

- Test individual components in isolation
- Mock external dependencies

### 8.2 Integration Testing

- Test interactions between components
- Verify data flow through the system

### 8.3 End-to-End Testing

- Test complete knowledge graph discovery process
- Verify output quality and accuracy

## 9. Deployment Strategy

### 9.1 Environment Setup

- Conda environment with required packages
- Configuration for different deployment scenarios

### 9.2 Execution

- Command-line interface for system operation
- Jupyter notebook interface for interactive usage

### 9.3 Monitoring

- Logging of system operation
- Progress tracking and reporting

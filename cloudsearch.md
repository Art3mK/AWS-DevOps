# Cloudsearch

Amazon CloudSearch is a fully-managed service in the AWS Cloud that makes it easy to set up, manage, and scale a search solution for your website or application.

### Q: What is a search domain and how do I create one?

A search domain is a data container and a set of services that make the data searchable. These services include:
- A document service that allows you upload data to your domain for indexing.
- A search service that allows you to perform search requests against your indexed data.
- A configuration service for controlling your domain's behavior (including relevance ranking).

### Q: Do my documents need to be in a particular format?

To make your data searchable, you need to format your data in JSON or XML.  Each item that you want to be able to receive as a search result is represented as a document. Every document has a unique document ID and one or more fields that contain the data that you want to search and return in results. Amazon CloudSearch generates a search index from your document data according to the index fields configured for the domain. As your data changes, you submit updates to add or delete documents from your index.

### Q: What is a search instance?

A search instance is a single search engine in the cloud that indexes documents and responds to search requests. It has a finite amount of RAM and CPU resources for indexing data and processing requests.
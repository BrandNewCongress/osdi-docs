#Queries
A query is a collection of resources that fit a set of criteria
* Queries are nonarbitrary: a resource's inclusion in the collection is based on attributes intrinsic to that resource
* Queries may be static or dynamic: A dynamic query will return the resources which match its criteria at the moment the query is retrieved. A static query will contain the resources which matched its criteria at the time the query was created
* Queries may only be created, deleted and edited on the content provider's native system; OSDI does not support 
* Query metadata may be updated via the API, but query criteria may only be modified and queries may only be created or deleted via the content provider's system
* Queries are unique collections of resources: a resource may match a query only once

### Query attributes:
* identifier
* description: plaintext describing the query's function
* dynamic: boolean reflecting whether the query is dynamic or static
* created_at
* modified_at
* summary  //name
* url
* total_items

### Query collections:
* Resources: the collection of resources which match the query's criteria at the time of the query's creation in static queries or at the time of retrieval in dynamic queries

### Query operations:

* Retrieve a query with matching resources

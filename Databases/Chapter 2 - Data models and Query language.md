> The Limits of my language means the limits of my world.

Relational database management systems (RDBMs) were first thought out to die within a few years of its time, but surprisingly that little son of a gun managed to stick around for a lot longer period in the tech industry. 

- Even though we have NoSQL and other various database technologies, Relational Databases continues to be used alongside those broad variety of non-relational databases, this is called **Polygot persistence**  
- But, the data stored in the relational tables requires an awkward transition layer between the objects of the application layer and the storage layer. This disconnection between the models is referred to as **impedance mismatch**
## Many-to-Many and Many-to-One Relationships
![[Chapter 2 - Data models and Query language-1778396943732.jpeg]]
the `region_id` and `industry_id` are given as IDs instead of plain texts, why?
- if the user interface has free-text fields for entering the region and industry values, it would make sense to store them as plain-text IDs
But, there are advantages to storing them as IDs instead of plain texts
1. Consistent style and spelling across references
2. Avoiding ambiguity (Avoids several cities with similar names)
3. Ease of updating in one singular place
4. Better search.
### Whether we store a value as an ID or text is a question of duplication.
Anything that is meaningful to humans are prone to change, so its better to centralize the place of change and make everything else refer to it to avoid inconsistency and redundancy.
***
## CODASYL - The Network Model
==**Really a legacy technology that's in the attic NOW**==
Standardized by the **Conference of Data Systems Language**
- CODASYL is a generalization of the hierarchical model wherein unlike a strict tree that allows records to have only one parent, records here can have multiple parent
- it allows for many-to-many and many-to-one relationships

Navigation uses physical pointers instead of foreign keys. So to read the data, developers had to manually follow chains of links from a root record. (similar to traversing a linked list)
##### Advantage: It was highly-efficient for the systems of 1970s
##### Disadvantages: Extremely complex and rigid. Changing the data-models or access-paths meant a complete re-write of application's query code!
## SQL - The Relational Model
==**The Standard that laid all the data in the open**==
A relation (table) is just simply a collection of tuples (rows)
- Navigation requires no manual access paths. You simply read rows that match an arbitrary condition or designate specific columns as a key to match on.
- A **query optimizer** automatically decides the best execution order and which indexes to use, effectively generating the access path on the fly so the developer doesn't have to.
##### Advantage: Highly flexible. You can add new indexes and query data in entirely new ways without needing to rewrite your application's queries, and the general-purpose optimizer benefits all applications.
##### Disadvantages: The query optimizers themselves are complicated beasts that require years of research and development to build (though application developers rarely need to worry about this).
## Document Databases
==**A modern approach with a nod to the hierarchical past**== 
Document databases revert to the hierarchical model in one specific way. They store nested records (one-to-many relationships) directly within the parent record rather than in separate tables.
- For many-to-one and many-to-many relationships, they operate similar to relational databases. They use unique identifiers called **document references** instead of foreign keys.
- They completely avoid the rigid, manual access paths of CODASYL.
- identifiers are simply resolved dynamically at read time via joins or follow-up queries.
##### Advantage: Keeps nested, one-to-many relationship data cleanly stored within a single parent record without the navigation nightmare of the network model.
##### Disadvantages: Related items in many-to-one or many-to-many relationships still require the database to resolve references at read time through joins or secondary queries.
***
## Which data model leads to simpler application code?
If the data in our application has a document-like structure where the tree of one-to-many relationships where typically the entire tree is loaded. Then use **==Document-based models==**
- Do note that document based datamodels have poor support for joins and complex relationships
	It is possible to reduce the many-to-many relationships by using de-normalization, but then
	1. the application code needs to do heavy-lifting to keep the data consistent at different places by make multiple changes
	2. Joins can be emulated within the application code but then again that increases the complexities and is inefficient than the joins performed by the specialized code within the database

For highly interconnected data, a relational model is acceptable and graph models are natural at it.
## Schema Flexibility 
Document databases are sometimes referred to as schema-less databases which is misleading. 
- The schema is implicit and not enforced by the database
- A more proper term would be `schema-on-read` as their structure is evaluated when the data is read.
- similar to dynamic (run-time) type checking
##### Advantages
- `schema-on-read` maybe advantageous if the item in the collection dont' have same structure for some reason
	1. The structure of the data is determined by external systems over which we have no control and which may change at any time
	2. There are greatly varying types of objects and it wouldn't make sense to put each type of object in its own table
In those condition, having a schema might hurt more than it helps and schema-less databases might be a natural fit.

By that notion, then relational databases can be referred to as `schema-on-write`
- The schema is explicit and is enforced by the database
- where the database ensures all the written data conforms to it
- similar to static (compile-time) type checking

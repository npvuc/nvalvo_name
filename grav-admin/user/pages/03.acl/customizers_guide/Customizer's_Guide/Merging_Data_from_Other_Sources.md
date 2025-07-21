

---

# Configuring_for_Data_Merge

# Configuring for Data Merge

To merge data, one or more data merge configuration ( .dmf ) files must be created defining the queries, and one or more document type .dcf files must be modified to specify the appropriate .dmf file(s) and available queries.



---

# Data_Merging_Overview

# Data Merging Overview

Arbortext Editor lets you incorporate references to external data sources in a document, and to then periodically resolve those references. A reference to external data is called a query and the result is called merged data .

The information in this chapter is an abbreviated overview of configuring Arbortext Editor 's data merging capabilities. Customizing data merging capabilities at your site may require that you contact Arbortext Consulting Services.



---

# Merging_Data_with_Arbortext_Editor

# Merging Data with Arbortext Editor

Authors of document with merged data can perform the following actions:

A query result contains the data retrieved and a namespaced element surrounding the data, preserving the query information for later identification and update.

Queries are of two types:

- • Fielded queries — The query result contains one or more name and value pairs. Each pair can be inserted independently into various locations in a document.

- • Content queries — The query result is a data chunk which can be as simple as a string or as complex as an entire document. Often, as when a result is derived from executing a query against a database, the result will be in tabular form. The data merging framework enforces no limitations on the format of a query result.



---

# Notes_and_Limitations

# Notes and Limitations

Be aware of the following issues when using merged data with Arbortext Editor :

- • The capability to merge data is deprecated and not an encouraged best practice supported by PTC.

- • Since there is no namespace support in SGML, all namespaced elements for datamerge markups are converted to PIs in SGML documents.



---

# Query_Definitions

# Query Definitions

A query refers to a query definition. The query definition is one of many definitions stored in a data merge (xml) configuration file. A query definition consists of a UI component and a formal definition.

The query definition UI component includes:

- • The name of the query definition. This name links a document's query to a query definition.

- • The parameters that must be passed to the query. The parameters must be given values at the time of inserting a query.

- • The query result type: document content, or name-value pairs.

- • A representative top level tag for quick context verification if document content is returned.

The query definition formal definition includes:

- • A source stage. This may be any program that generates a DOM node. The actual source may be a database, a file, a URL, or some external process. The program is responsible for presenting the result as a node, perhaps using some simple markup to represent name value pairs.

- • One or more transformation stages. These stages take a DOM node as input and generates a new DOM node as output.

- • A description of the order in which the stages are to be applied, starting with the source.

- • For each stage, a mapping of UI parameters to actual parameters for the stage.
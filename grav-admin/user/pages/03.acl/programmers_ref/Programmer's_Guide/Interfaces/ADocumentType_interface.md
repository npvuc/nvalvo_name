

---

# doctypeName_attribute

If there is an associated DTD or Schema file then this is the basename of that file. For example, if the associated DTD is axdocbook.dtd , then this attribute would be "axdocbook" .

For a freeform document, this is the local name of the root element.

If the document was structured but the DTD or Schema was not available then this will be the same as the DocumentType.name attribute.

If the document was opened as non-structured then this will be "ascii" .



---

# doctypeURI_attribute

The absolute URI of the document type directory associated with this DocumentType or null if undefined, for example, for free-form XML or untagged documents.



---

# tableModelCells_method

Returns a list containing the name of each tag that is allowed as a cell tag for a table of the specified table model in a document using this DocumentType .



---

# tableModelRow_method

Returns the name of the tag that is allowed as the row tag for a table of the specified table model in a document using this DocumentType .



---

# tableModels_attribute

Returns a list of all the table models valid in a document using this DocumentType .



---

# tableModelSupport_method

Tests whether a given table model supports a specified feature in documents created using this DocumentType . The same table model may support different features in different documents.



---

# tableModelTables_method

Returns a list containing the name of each tag that is allowed as a table (root) tag for a table of the specified table model in a document using this DocumentType .



---

# tableModelTableTitle_method

Returns the name of the tag that is allowed as the title (or caption) tag for a table of the specified table model in a document using this DocumentType .



---

# tableModelTags_method

Returns a list containing the name of all the tags used in the specified table model in a document using this DocumentType .



---

# tableModelWrappers_method

Returns a list containing the name of each tag that is allowed as a wrapper tag for a table of the specified table model in a document using this DocumentType .
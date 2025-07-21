

---

# clearAttributes_method

Resets all of the attributes for this object to their default values and clears the corresponding table markup.



---

# deleteAttribute_method

Delete an attribute.



---

# deletePrivateColspecs_method

All colspec tags within thead or tfoot tags are deleted, and every entry tag in the table is adjusted to refer to the colspec tags that are children of the tgroup element. Applied to the TableGrid containing the table object or all TableGrid s in the TableSet or TableTilePlex as appropriate.



---

# deleteSpanspecs_method

Deletes spanspec tags and updates entry tags to refer to colspec tags. If the document type does not allow namest or nameend attributes on entry elements, deleteSpanSpecs does nothing. This is applied to the TableGrid containing the table object or all TableGrid s in the TableSet or TableTilePlex as appropriate.



---

# Direction_enumeration

A direction.

The Direction enumeration has the following constants of type unsigned short .



---

# document_attribute

The document containing this table object.



---

# element_attribute

The Element for the markup associated with this table object.



---

# ExamineWhatColspec_enumeration

Parameter to renameColspec indicating what colspec tags are to be examined.

The ExamineWhatColspec enumeration has the following constants of type unsigned short .



---

# getAttribute_method

Returns the value of an attribute given the ID of the attribute.



---

# grid_attribute

The TableGrid containing this table object.



---

# minimizeAttributes_method

Scans the TableSet containing the object and reorganizes the attributes of the various table tags to minimize the number of attributes required to describe the table.



---

# modifiable_attribute

True if this table object is not read only.



---

# Orientation_enumeration

The orientation of a rule or row/column.

The Orientation enumeration has the following constants of type unsigned short .



---

# renameColspec_method

Renames a single colspec tag by updating the tag's colname attribute and adjusting all spanspec and entry tags to refer to the colspec tag by its the new value for the colname attribute. This is applied to the TableGrid containing the table object or all TableGrid s in the TableSet or TableTilePlex as appropriate.



---

# renameColumns_method

Updates the colname attribute of every colspec tag in a table. This is applied to the TableGrid containing the table object or all TableGrid s in the TableSet or TableTilePlex as appropriate.



---

# renameSpanspec_method

Renames a single spanspec tag by adjusting the tag's spanname attribute and modifying every entry tag that refers to it. This is applied to the TableGrid containing the table object or all TableGrid s in the TableSet or TableTilePlex as appropriate.



---

# set_attribute

The TableSet containing this table object.



---

# setAttribute_method

Set an attribute.



---

# tableModel_attribute

The name of the table model that manages this object. In some cases, for example if the object is a TableObjectStore , the table model can not be determined and unknown will be returned.



---

# toid_attribute

The TOID of this table object, which is mainly useful for calling ACL routines.



---

# type_attribute

The TableObject.Type (set, grid, row, column, cell, rule, and so on) of this table object.



---

# Type_enumeration

An integer indicating which type of table object this is.

The Type enumeration has the following constants of type short .
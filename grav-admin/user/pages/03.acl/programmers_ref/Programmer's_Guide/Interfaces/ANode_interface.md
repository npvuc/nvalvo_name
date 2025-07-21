

---

# ATIElementAttributeSelector_enumeration

Passed as the selector parameter to the getElementsByAttribute method.

The ATIElementAttributeSelector enumeration has the following constants of type unsigned short .



---

# CMSObject_attribute

Represents the CMSObject associated with this Node (may be null ).

This can be accessed for a Document Node or for any other Node type which has an associated OID.

Use the enclosingObject attribute on the returned object to obtain any enclosing objects.



---

# collapse_method

Collapses the parent CMS object that contains this node. Can optionally operate on all references to the parent CMS object.



---

# contentModel_attribute

Returns the content model as specified in the DTD or schema associated with the owner document of this Node as a DOMString . The content model has syntax similar to the element definition in a DTD. For example, in a DTD definition, <!Element book (title | chapter*)> . The content model for the element book is (title|chapter*).



---

# contextPath_method

contextPath returns a DOMStringList that contains possible context paths to make the target Node valid at the point indicated by this Node . If one of the paths returned is an empty string, the target Node can be inserted without any Node being added.



---

# dialog_attribute

Returns the Window for the XUI dialog associated with this Node , if any. This will exist only if there is a DCF file entry associating a XUI dialog with this element in the document.



---

# distanceTo_method

Finds the distance from this Node to another specified Node .

distanceTo is intended to measure progress through a document in a reasonably linear manner. "Distance" is defined as the number of nodes between the nodes. Such measurements can be used for time estimates, progress dialog boxes, and so on.

If the target node is null, distanceTo calculates the distance to the end of the document. If the target node is not null, distanceTo calculates the distance to just before the target. Therefore, the sum of the distance between an arbitrary set of targets equals the total document distance, as long as each target is after the previous one.



---

# enclosingCell_attribute

The table cell this node is in, if any.



---

# enclosingCMSObject_attribute

Represents the innermost CMSObject which contains this Node (may be null ).

Use the enclosingObject attribute on the returned object to obtain any enclosing objects.



---

# expand_method

Expands the parent CMS object that contains this node. Can optionally operate on all references to the parent CMS object.



---

# firstOID_attribute

A string value that can be spliced into an ACL command or function to indicate the first ACL OID represented by Node .

This attribute will normally have the same OID as lastOID and will always be the same for Element type nodes. They will be different, however, for Text nodes that represent more than one text fragment in the document.



---

# getGraphicPath_method

If this Node represents a graphic tag, returns the full path (if found) to the referenced graphic.



---

# icon2_attribute

Used to get or set the name of a second display icon that appears to the left of this Node (if any). The icons appear in the Document Map and also appear in the Edit window whenever element tags are set to full or partial display. If this Node has no icon, this returns the string "None" .

If an invalid display icon is set, it will act as if it were set to "None".

The value may be the case-sensitive name of a built-in icon or a full or relative path to a .bmp file. When setting this attribute, if a relative path is given, it will be looked for in the search path given by Application.getOption("graphicspath") . If the .bmp file is not found, it will act as if it were set to the built-in icon “None”.

Built-in icon names are case sensitive and are listed in the following table.



---

# icon_attribute

Used to get or set the name of the display icon that appears to the left of this Node (if any). The icons appear in the Document Map and also appear in the Edit window whenever element tags are set to full or partial display. If this Node has no icon, this returns the string "None" .

If an invalid display icon is set, it will act as if it were set to "None".

The value may be the case-sensitive name of a built-in icon or a full or relative path to a .bmp file. When setting this attribute, if a relative path is given, it will be looked for in the search path given by Application.getOption("graphicspath") . If the .bmp file is not found, it will act as if it were set to the built-in icon “None”.

Built-in icon names are case sensitive and are listed in the following table.



---

# insertTable_method

Insert a table as a child of this Node .



---

# lastOID_attribute

A string value that can be spliced into an ACL command or function to indicate the last ACL OID represented by Node .

This attribute will normally have the same OID as firstOID and will always be the same for Element type nodes. They will be different, however, for Text nodes that represent more than one text fragment in the document.



---

# setCMSObject_method

Associates this Node with the given CMSObject. If this Node is already associated with an object then the new object will be associated with all Nodes in that object's Range. Thus, this might affect other Nodes.

This can be called for a Document or for any other Node type which has an associated OID.



---

# tableNoDelete_attribute

Returns true if the node is managed by a table model and the table model indicates the node should be protected from deletion.



---

# tableObject_attribute

Returns the deepest table object (a cell, row, grid, or set) that fully contains the specified node . If the specified node is not inside table markup, it returns a null pointer.



---

# userDataKeys_attribute

A DOMStringList of all keys that have data associated to this node by previous calls to setUserData . This is null if no user data exists for the node.
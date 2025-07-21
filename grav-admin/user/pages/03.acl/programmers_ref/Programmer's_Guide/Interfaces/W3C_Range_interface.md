

---

# cloneContents_method

Duplicates the contents of a Range



---

# cloneRange_method

Produces a new Range whose boundary-points are equal to the boundary-points of the Range.



---

# collapse_method

Collapse a Range onto one of its boundary-points



---

# collapsed_attribute

TRUE if the Range is collapsed



---

# commonAncestorContainer_attribute

The deepest common ancestor container of the Range's two boundary-points.



---

# compareBoundaryPoints_method

Compare the boundary-points of two Ranges in a document.



---

# CompareHow_enumeration

Passed as a parameter to the compareBoundaryPoints method.

The CompareHow enumeration has the following constants of type unsigned short .



---

# deleteContents_method

Removes the contents of a Range from the containing document or document fragment without returning a reference to the removed content.



---

# detach_method

Called to indicate that the Range is no longer in use and that the implementation may relinquish any resources associated with this Range. Subsequent calls to any methods or attribute getters on this Range will result in a DOMException being thrown with an error code of INVALID_STATE_ERR .



---

# endContainer_attribute

Node within which the Range ends



---

# endOffset_attribute

Offset within the ending node of the Range.



---

# extractContents_method

Moves the contents of a Range from the containing document or document fragment to a new DocumentFragment.



---

# insertNode_method

Inserts a node into the Document or DocumentFragment at the start of the Range. If the container is a Text node, this will be split at the start of the Range (as if the Text node's splitText method was performed at the insertion point) and the insertion will occur between the two resulting Text nodes. Adjacent Text nodes will not be automatically merged. If the node to be inserted is a DocumentFragment node, the children will be inserted rather than the DocumentFragment node itself.



---

# selectNode_method

Select a node and its contents



---

# selectNodeContents_method

Select the contents within a node



---

# setEnd_method

Sets the attributes describing the end of a Range.



---

# setEndAfter_method

Sets the end of a Range to be after a node



---

# setEndBefore_method

Sets the end position to be before a node.



---

# setStart_method

Sets the attributes describing the start of the Range.



---

# setStartAfter_method

Sets the start position to be after a node



---

# setStartBefore_method

Sets the start position to be before a node



---

# startContainer_attribute

Node within which the Range begins



---

# startOffset_attribute

Offset within the starting node of the Range.



---

# surroundContents_method

Reparents the contents of the Range to the given node and inserts the node at the position of the start of the Range.



---

# toString_method

Returns the contents of a Range as a string. This string contains only the data characters, not any markup.
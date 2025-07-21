

---

# isElementContentWhitespace_attribute

Returns whether this text node contains element content whitespace, often abusively called "ignorable whitespace". The text node is determined to contain whitespace in element content during the load of the document or if validation occurs while using Document.normalizeDocument() .



---

# replaceWholeText_method

Replaces the text of the current node and all logically-adjacent text nodes with the specified text. All logically-adjacent text nodes are removed including the current node unless it was the recipient of the replacement text.

This method returns the node which received the replacement text. The returned node is:

- • null , when the replacement text is the empty string;

- • the current node, except when the current node is read-only;

- • a new Text node of the same type ( Text or CDATASection ) as the current node inserted at the location of the replacement.



---

# splitText_method

Breaks this node into two nodes at the specified offset , keeping both in the tree as siblings. After being split, this node will contain all the content up to the offset point. A new node of the same type, which contains all the content at and after the offset point, is returned. If the original node had a parent node, the new node is inserted as the next sibling of the original node. When the offset is equal to the length of this node, the new node has no data.



---

# wholeText_attribute

Returns all text of Text nodes logically-adjacent text nodes to this node, concatenated in document order.
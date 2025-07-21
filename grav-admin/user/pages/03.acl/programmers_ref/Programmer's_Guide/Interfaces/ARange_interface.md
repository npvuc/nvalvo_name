

---

# allowedInsertElements_attribute

Elements that can be inserted into the Document or DocumentFragment at the start of the Range such that the result will be compliant with VAL_SCHEMA validity type. If the start container is a Text node it will be assumed to be split into two text nodes and the list of elements valid between them will be returned.



---

# allowedSurroundElements_attribute

Elements that can surround the Range such that the result will be compliant with VAL_SCHEMA validity type.



---

# canInsertNode_method

This method indicates whether a Node can be inserted at a position specified by the start of this Range such that the result is compliant with VAL_SCHEMA validity type. If the container is a text node, it will be considered to have been split and the test will be made between the two resulting text nodes.



---

# canInsertNodeWithFixup_method

This method indicates whether a Node can be inserted at a position specified by the start of this Range such that the result is compliant with VAL_SCHEMA validity type. This test considers adding required ancestors or descendents to make context valid.



---

# contextString_attribute

This function returns a DOMString describing the context of the start of this Range . This string consists of a list of element names and parentheses, such as: doc(body(chapter(title()para0(title()para( The left parenthesis following an element name represents a start tag, and the right parenthesis represents the end tag for the corresponding unmatched start tag. If this Range is before the opening start tag or if context checking is not relevant for the current document, a null string will be returned.



---

# endOID_attribute

The end OID of the Range . Note that the OID indicated by the endOID is not necessarily the same as the ending OID for the node indicated by the endNode .



---

# endPos_attribute

The end position (in ACL) of the Range . Note that the position indicated by the endPos is not necessarily equal to the value of endOffset .



---

# insertNodeWithFixup_method

This method inserts a Node to the position specified by the start of this Range . It will try to add required ancestors or descendents to make context compliant with VAL_SCHEMA validity type. If the start container of the range is a text node it will be split and the node will be inserted between the two resulting text nodes.



---

# insertParsedString_method

Parses text and inserts the resulting DOM objects into a document at the location indicated by the start of the Range .



---

# MarkupFlags_enumeration

The MarkupFlags enumerated type is used to construct the flags parameter to the toMarkupStringEx method by ORing any of the following options:

The MarkupFlags enumeration has the following constants of type int .



---

# startOID_attribute

The start OID of the Range . Note that the OID indicated by the startOID is not necessarily the same as the starting OID for the node indicated by the startNode .



---

# toMarkupString_method

Returns the contents of a Range as a string. This string contains the character data and markup representing the entire contents of the range.



---

# toMarkupStringEx_method

Returns the contents of a Range as a string, with control over the markup. This string contains the character data and markup representing the entire contents of the range.
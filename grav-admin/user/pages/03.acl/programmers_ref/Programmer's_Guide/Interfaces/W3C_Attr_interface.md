

---

# isId_attribute

Returns whether this attribute is known to be of type ID (i.e. to contain an identifier for its owner element) or not. When it is and its value is unique, the ownerElement of this attribute can be retrieved using the method Document.getElementById . The implementation could use several ways to determine if an attribute node is known to contain an identifier:

- • If validation occurred using an XML Schema [ XML Schema Part 1 ] while loading the document or while invoking Document.normalizeDocument() , the post-schema-validation infoset contributions (PSVI contributions) values are used to determine if this attribute is a schema-determined ID attribute using the schema-determined ID definition in [ XPointer ].

- • If validation occurred using a DTD while loading the document or while invoking Document.normalizeDocument() , the infoset [type definition] value is used to determine if this attribute is a DTD-determined ID attribute using the DTD-determined ID definition in [ XPointer ].

- • from the use of the methods Element.setIdAttribute() , Element.setIdAttributeNS() , or Element.setIdAttributeNode() , i.e. it is an user-determined ID attribute;

- • using mechanisms that are outside the scope of this specification, it is then an externally-determined ID attribute . This includes using schema languages different from XML schema and DTD.

If validation occurred while invoking Document.normalizeDocument() , all user-determined ID attributes are reset and all attribute nodes ID information are then reevaluated in accordance to the schema used. As a consequence, if the Attr.schemaTypeInfo attribute contains an ID type, isId will always return true.



---

# name_attribute

Returns the name of this attribute.



---

# ownerElement_attribute

The Element node this attribute is attached to or null if this attribute is not in use.



---

# schemaTypeInfo_attribute

The type information associated with this attribute. While the type information contained in this attribute is guarantee to be correct after loading the document or invoking Document.normalizeDocument() , schemaTypeInfo may not be reliable if the node was moved.



---

# specified_attribute

If this attribute was explicitly given a value in the original document, this is true ; otherwise, it is false . Note that the implementation is in charge of this attribute, not the user. If the user changes the value of the attribute (even if it ends up having the same value as the default value) then the specified flag is automatically flipped to true . To re-specify the attribute as the default value from the DTD, the user must delete the attribute. The implementation will then make a new attribute available with specified set to false and the default value (if one exists).

In summary:

- • If the attribute has an assigned value in the document then specified is true , and the value is the assigned value.

- • If the attribute has no assigned value in the document and has a default value in the DTD, then specified is false , and the value is the default value in the DTD.

- • If the attribute has no assigned value in the document and has a value of #IMPLIED in the DTD, then the attribute does not appear in the structure model of the document.

- • If the ownerElement attribute is null (i.e. because it was just created or was set to null by the various removal and cloning operations) specified is true .



---

# value_attribute

On retrieval, the value of the attribute is returned as a string. Character and general entity references are replaced with their values. See also the method getAttribute on the Element interface.

On setting, this creates a Text node with the unparsed contents of the string. I.e. any characters that an XML processor would recognize as markup are instead treated as literal text. See also the method setAttribute on the Element interface.